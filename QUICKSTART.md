# QuickStart — local setup for Heavy Rental

This guide sets up **local development** for:

1. The three DevContainer packs in [heavy-rental-devcontainer-configuration](https://github.com/Heavy-Rental/heavy-rental-devcontainer-configuration)
2. The **Android** app in [heavy-rental-mobile](https://github.com/Heavy-Rental/heavy-rental-mobile) (Android Studio, **Java JDK 17**, and **npm** + Mockoon on port **8081**)

| Pack / project | Runtime | Host ports |
|----------------|---------|------------|
| `Heavy-Rental-REST-API/` | Spring Boot + PostgreSQL 17 | **8080** (API), **5432** (primary), **5433** (optional replica) |
| `Haystack-Fast-API/` | FastAPI / Haystack + Postgres+pgvector + Neo4j | **8000** (API), **5434** (DB), **7474** / **7687** (Neo4j), **8089** (populate) |
| `Heavy-Rental-Web-Portal/` | React / Vite | **5173** |
| `heavy-rental-mobile` | Android (Kotlin, Compose) + Mockoon CLI | Emulator → host **8080** (Spring) or **8081** (Mockoon) |

The Android app is **not** a DevContainer pack. Build it in Android Studio. Default Retrofit target is Spring at `http://10.0.2.2:8080/` (emulator). Set `USE_MOCK_SERVER = true` to use Mockoon at `http://10.0.2.2:8081/`.

Source architecture: [ARCHITECTURE.md](https://github.com/Heavy-Rental/heavy-rental-devcontainer-configuration/blob/develop/ARCHITECTURE.md). Setup videos live in that repository’s `videos/` folder (not copied here).

---

## 1. Prerequisites

| Need | Notes |
|------|--------|
| [Docker](https://docs.docker.com/get-docker/) | Engine running (DevContainer packs) |
| [Visual Studio Code](https://code.visualstudio.com/) | Desktop IDE for DevContainers |
| **Remote Development** | Extension ID `ms-vscode-remote.vscode-remote-extensionpack` |
| **Container Tools** | Extension ID `ms-azuretools.vscode-containers` |
| [Android Studio](https://developer.android.com/studio) | Android IDE (Ladybug / latest). SDK **API 35**, emulator |
| **Java JDK 17** | Required by the Android Gradle `jvmTarget` / `JavaVersion.VERSION_17`. Temurin 17 is a good default |
| **Node.js 18+** and **npm** | Mockoon CLI (`npm run mock:mockoon`) in `heavy-rental-mobile` |
| Git | Clone the configuration repo and product sources |
| Disk / RAM | Three Compose stacks; replica pack adds a second Postgres; emulator needs extra RAM |

Install the two VS Code extensions **on the host** before opening a folder in a container. Android Studio, JDK 17, and Node/npm are **host** installs (section 9).

---

## 2. Clone the configuration repository

```bash
git clone https://github.com/Heavy-Rental/heavy-rental-devcontainer-configuration.git
cd heavy-rental-devcontainer-configuration
git checkout develop
```

You should see:

```text
heavy-rental-devcontainer-configuration/
├── Heavy-Rental-REST-API/
├── Haystack-Fast-API/
├── Heavy-Rental-Web-Portal/
├── ARCHITECTURE.md
└── README.md
```

Application **source** for each service is typically mounted from its own clone (`heavy-rental-spring-rest-api`, `haystack-fast-api`, `heavy-rental-react-web-portal`). Keep those clones on `develop` as well.

---

## 3. Create the shared Docker network

All packs attach to an **external** network. Create it once on the host:

```bash
docker network create heavy-rental-network
```

If it already exists, Docker prints an error and you can ignore it.

```bash
docker network ls | grep heavy-rental-network
```

Without this network, containers cannot resolve peers (`heavy-rental-rest-api`, `postgres-primary`, `postgres-haystack`, `neo4j`).

Video in the source repo: `Creating.new.docker.network.heavy-rental-network.mp4`.

---

## 4. Recommended bring-up order

1. Network (step 3)
2. **REST API** pack — OLTP primary must be healthy before Haystack sync
3. **Haystack** pack — pull-merge and Neo4j populate
4. **Web Portal** pack — UI talks to Spring only
5. **Android** (section 9) — JDK 17 + Android Studio; optional Mockoon on `:8081` if you are not using Spring

Minimum for UI + CRUD: steps 1, 2, 4.  
Minimum for recommend / graph: steps 1–3, then 4.  
Minimum for Android against Spring: steps 1–2, then 9.  
Minimum for Android against Mockoon only: JDK 17 + Android Studio + Node/npm (section 9); no DevContainers required.

---

## 5. Spring Boot REST API pack

### 5.1 Choose a profile and promote `.devcontainer`

VS Code looks for `.devcontainer` at the **root of the folder you open**. The REST pack ships **two** nested profiles. Move one up:

```bash
cd Heavy-Rental-REST-API

# Option A — primary + streaming replica (host 5433)
mv "Spring Boot REST API devcontainer with PostgreSQL Read Replica/.devcontainer" ./.devcontainer

# Option B — primary only
# mv "Spring Boot REST API devcontainer without read replica/.devcontainer" ./.devcontainer
```

Layout after promote:

```text
Heavy-Rental-REST-API/
  .devcontainer/     ← active
  README.md
```

Both profiles use JDBC `jdbc:postgresql://db-primary:5432/heavy_rental`. The replica is for read experiments; Spring still writes the primary.

### 5.2 Open in a container

1. Open VS Code
2. Command Palette → **Dev Containers: Open Folder in Container…**
3. Select `Heavy-Rental-REST-API` (the folder that now contains `.devcontainer`)
4. Trust the folder when prompted
5. Wait for image build; click **Connecting to Dev Container (show log)** if you want logs

### 5.3 Extensions expected inside the container

- Spring Boot Extension Pack (`vmware.vscode-boot-dev-pack`)
- Extension Pack for Java (`vscjava.vscode-java-pack`)
- PostgreSQL (`ms-ossdata.vscode-pgsql`)

### 5.4 Verify

```bash
docker exec postgres-primary pg_isready -U postgres -d heavy_rental

# With-replica pack only
docker exec postgres-replica-one pg_isready -U postgres -d heavy_rental

curl -s http://localhost:8080/actuator/health
```

Local DB credentials (dev only): user `postgres` / password `postgres` / database `heavy_rental`.

Stripe CLI is installed in the REST app image. Container `postStartCommand` can run `stripe listen --forward-to http://localhost:8080/api/payments/webhook` after `stripe login` or `STRIPE_API_KEY`. Product repo helper: `./scripts/dev-with-webhooks.sh` in `heavy-rental-spring-rest-api`.

Source videos: `End.to.End.Installation.for.Java.REST.API.Project.mp4`.

---

## 6. Haystack + FastAPI pack

Preconditions: network exists; REST primary is up if you want a **live** fleet mirror (`FLEET_BACKEND=sql`). The Haystack container still starts without the primary (sync **skips** cycles by default).

### 6.1 Open in a container

1. Command Palette → **Dev Containers: Open Folder in Container…**
2. Select `Haystack-Fast-API`
3. Trust the folder; wait for Compose (`haystack-fast-api`, `postgres-haystack`, `postgres-haystack-sync`, `neo4j`, `neo4j-populate`)

### 6.2 Extensions expected

- Python (`ms-python.python`)
- Pylance (`ms-python.vscode-pylance`)
- Python Debugger (`ms-python.debugpy`)
- autopep8 (`ms-python.autopep8`)

### 6.3 Configure and start the API

From the **product** workspace (`haystack-fast-api`), not only the pack:

```bash
cp .env.example .env
uv sync --all-groups
uv run uvicorn app.main:app --host 0.0.0.0 --port 8000 --reload
```

| Check | URL |
|-------|-----|
| Health | http://localhost:8000/health |
| OpenAPI | http://localhost:8000/docs |

**Live compose** (quote `equipment.id` = `assets.id`): set `POSTGRES_HOSTNAME=postgres-haystack` (not `db`), `FLEET_BACKEND=sql`, `PRICING_SCHEMA=public`. Fastest smoke: `NEED_DECOMPOSER=stub`, `FLEET_BACKEND=fake` (seed ids `AST-*`).

Haystack **never** writes `postgres-primary`. Sync direction is primary → `postgres-haystack` (poll ~60s), then optional `POST` to `neo4j-populate:8089/v1/populate`.

Source video: `End.to.End.Project.Setup.Video.for.Haystack.Fast.API.Project.mp4`. Product smoke: [haystack-fast-api QUICKSTART](https://github.com/Heavy-Rental/haystack-fast-api/blob/develop/QUICKSTART.md).

---

## 7. React Web Portal pack

Preconditions: network exists. The portal container starts without Spring; API calls fail until REST is healthy.

### 7.1 Open in a container

1. Command Palette → **Dev Containers: Open Folder in Container…**
2. Select `Heavy-Rental-Web-Portal`
3. Trust the folder; wait for the Node image

### 7.2 Run the app (product workspace)

In `heavy-rental-react-web-portal`:

```bash
npm install
npm run dev:api    # proxy to Spring at localhost:8080
# npm run dev:mock # mock API at 127.0.0.1:4010
```

Open http://localhost:5173.

The portal MUST call **Spring REST only**. It does not talk to Haystack, Postgres, or Neo4j for product flows.

Source video: `End.to.End.Project.Setup.Video.for.Heavy.Rental.Web.Portal.mp4`.

---

## 8. Ports and Docker DNS

### Host-published ports

| Port | Service | Pack |
|------|---------|------|
| 5173 | Vite | Web Portal |
| 8080 | Spring REST | REST API |
| 8081 | Mockoon / Prism (mobile mocks) | Android host (`npm run mock:mockoon`) |
| 5432 | Postgres primary | REST API |
| 5433 | Postgres replica | REST API (with-replica only) |
| 5434 | Postgres Haystack | Haystack |
| 7474 | Neo4j Browser | Haystack |
| 7687 | Neo4j Bolt | Haystack |
| 8000 | FastAPI | Haystack (app) |
| 8089 | neo4j-populate | Haystack |

### Names on `heavy-rental-network`

| Hostname | Purpose |
|----------|---------|
| `heavy-rental-web-portal` | Portal container |
| `heavy-rental-rest-api` | Spring HTTP |
| `postgres-primary` / `db-primary` | OLTP |
| `postgres-replica-one` / `db-replica-one` | Standby reads |
| `postgres-haystack` | Haystack local DB |
| `haystack-fast-api` | FastAPI |
| `neo4j` | Bolt 7687 |
| `neo4j-populate` | Admin HTTP 8089 |

From **another container**, call Spring at `http://heavy-rental-rest-api:8080`. From the **host browser**, use `http://localhost:8080`.

---

## 9. Android mobile (Android Studio, JDK 17, npm / Mockoon)

The Android app lives in [heavy-rental-mobile](https://github.com/Heavy-Rental/heavy-rental-mobile). It is **not** one of the three DevContainer packs.

| Item | Value |
|------|--------|
| Application id | `com.heavyrental` |
| Language | Kotlin, JVM **17** |
| UI | Jetpack Compose, Material 3 |
| SDK | `minSdk` 26, `compileSdk` / `targetSdk` **35** |
| Default API | Spring `http://10.0.2.2:8080/` (`USE_MOCK_SERVER = false`) |
| Mock API | Mockoon / Prism `http://10.0.2.2:8081/` (`USE_MOCK_SERVER = true`) |
| Dev login | `admin@localhost` / `admin1234` |

Full QA walkthrough: [specification/testing-guide.md](https://github.com/Heavy-Rental/heavy-rental-mobile/blob/develop/specification/testing-guide.md).

### 9.1 Install Java JDK 17

The Gradle module sets `sourceCompatibility` / `targetCompatibility` / `jvmTarget` to **17**. Use a JDK 17 for Gradle even if Android Studio’s embedded JBR is newer.

**Check what you already have:**

```bash
java -version
# Expect a 17.x line, for example: openjdk version "17.0.x"
```

**Linux (Debian / Ubuntu) — Temurin 17:**

```bash
sudo apt-get update
sudo apt-get install -y wget apt-transport-https gnupg
wget -qO - https://packages.adoptium.net/artifactory/api/gpg/key/public | sudo gpg --dearmor -o /usr/share/keyrings/adoptium.gpg
echo "deb [signed-by=/usr/share/keyrings/adoptium.gpg] https://packages.adoptium.net/artifactory/deb $(. /etc/os-release && echo $VERSION_CODENAME) main" | sudo tee /etc/apt/sources.list.d/adoptium.list
sudo apt-get update
sudo apt-get install -y temurin-17-jdk
sudo update-alternatives --config java   # pick 17 if several JDKs exist
```

**macOS (Homebrew):**

```bash
brew install --cask temurin@17
```

**Windows:** download **Eclipse Temurin 17 (LTS) JDK** from [adoptium.net](https://adoptium.net/temurin/releases/?version=17), run the MSI, and tick “Set JAVA_HOME”.

**Optional `JAVA_HOME` (Linux / macOS):**

```bash
# typical Temurin path — adjust if yours differs
export JAVA_HOME=/usr/lib/jvm/temurin-17-jdk-amd64
export PATH="$JAVA_HOME/bin:$PATH"
```

On Windows, set **JAVA_HOME** to the Temurin 17 install directory (Settings → System → About → Advanced system settings → Environment Variables).

### 9.2 Install Node.js 18+ and npm (Mockoon CLI)

Mock servers are started with **npm scripts** in `heavy-rental-mobile/package.json` (`@mockoon/cli`). You need **Node.js 18 or newer**; npm is bundled with Node.

**Check:**

```bash
node -v    # v18.x or higher (project also verified with newer Node)
npm -v
```

**Linux (NodeSource 20 LTS example):**

```bash
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt-get install -y nodejs
```

**macOS:** `brew install node@20`

**Windows:** installer from [nodejs.org](https://nodejs.org/) (LTS). Confirm **npm** is on PATH.

Do **not** use the portal DevContainer’s Node for this — run npm on the **host** so Mockoon can bind `0.0.0.0:8081` for the emulator.

### 9.3 Install Android Studio (Android IDE)

1. Download [Android Studio](https://developer.android.com/studio) for your OS and complete the installer.
2. First-run **Setup Wizard**:
   - Standard install
   - Accept SDK licenses
   - Let it install **Android SDK**, **Android SDK Platform-Tools**, and **Android Emulator**
3. **SDK Manager** (More Actions → SDK Manager, or Settings → Languages & Frameworks → Android SDK):
   - **SDK Platforms:** Android 15.0 (**API 35**) — required (`compileSdk` / `targetSdk` 35)
   - **SDK Tools:** Android SDK Build-Tools, Android Emulator, Intel x86 Emulator Accelerator (HAXM) **or** Android Emulator hypervisor (Windows/Linux KVM)
4. **Gradle JDK 17** (Settings → Build, Execution, Deployment → Build Tools → Gradle):
   - **Gradle JDK** = JDK 17 (Temurin 17 from 9.1, or “jbr-17” if Studio ships it)
   - Do not leave this on JDK 11
5. **Device Manager** → Create Device:
   - Phone (Pixel 6 or similar)
   - System image **API 26 or higher** (app `minSdk` is 26). API 35 is a good match for compileSdk
   - Finish and start the AVD once to confirm the emulator boots

Hardware: enable virtualization (Intel VT-x / AMD SVM / Windows Hyper-V / Linux KVM) or the emulator will be very slow.

### 9.4 Clone the mobile repository

```bash
git clone https://github.com/Heavy-Rental/heavy-rental-mobile.git
cd heavy-rental-mobile
git checkout develop
```

You should see `app/`, `specification/`, `mocks/`, `package.json`, and `gradlew`.

**Open in Android Studio:** File → Open… → select the `heavy-rental-mobile` folder → Trust the project → wait for Gradle sync.

If sync fails with a Java version error, go back to 9.3 step 4 and set Gradle JDK to 17, then File → Sync Project with Gradle Files.

### 9.5 Install npm packages and start Mockoon

From the **mobile repo root** (`heavy-rental-mobile/`), on the host:

```bash
npm install
```

This installs `@mockoon/cli`, `@stoplight/prism-cli`, and `yaml` (see `package.json`). It does **not** build the Android APK.

**Start Mockoon** (leave this terminal open):

```bash
npm run mock:mockoon
```

That regenerates mocks from OpenAPI (`mock:prepare`) and serves `mocks/mockoon/heavy-rental.environment.json` on **`0.0.0.0:8081`**.

**Smoke check** (second terminal, mock still running):

```bash
npm run mock:verify

curl -s http://127.0.0.1:8081/api/auth/getBearerToken
curl -s http://127.0.0.1:8081/api/deliveries
curl -s http://127.0.0.1:8081/api/returns
```

Expect a plain-text interim JWT and JSON arrays for deliveries/returns.

| Script | What it does |
|--------|----------------|
| `npm run mock:prepare` | Regenerates Mockoon env + bundled OpenAPI (do not hand-edit outputs) |
| `npm run mock:mockoon` | Prepare + start Mockoon CLI on **8081** |
| `npm run mock:prism` | Alternative mock (same port, OpenAPI via Prism) |
| `npm run mock:verify` | GET/PATCH smoke against `:8081` |

**Optional Mockoon desktop:** `npm run mock:prepare`, then Open environment → `mocks/mockoon/heavy-rental.environment.json`, port **8081**, start.

Do not edit `mocks/mockoon/` or `mocks/.generated/` by hand. Change `specification/api/heavyrental-openapi.yaml` or `specification/api/examples/*`, then re-run `npm run mock:prepare`.

**Mockoon vs Spring:** Mockoon does **not** check passwords (canned 200). Use real Spring (`:8080`) for credential negatives.

### 9.6 Point the app at Spring or Mockoon

In `app/src/main/java/com/heavyrental/network/dto/RetrofitInstance.kt` (path may vary slightly under `network/`):

| `USE_MOCK_SERVER` | Emulator base URL | Host process |
|-------------------|-------------------|--------------|
| `false` (default) | `http://10.0.2.2:8080/` | Spring REST (section 5) |
| `true` | `http://10.0.2.2:8081/` | `npm run mock:mockoon` |

Never use `localhost` from the emulator — that is the emulator itself, not your PC. Physical device: use `http://<host-LAN-IP>:8080/` or `:8081/` and allow that IP in cleartext network security if needed.

### 9.7 Run the app

1. Start the emulator (Device Manager) **or** plug in a device with USB debugging.
2. If using Mockoon: keep `npm run mock:mockoon` running. If using Spring: REST pack healthy on **8080**.
3. Android Studio: select the app configuration → **Run** (green triangle), or:

```bash
./gradlew :app:assembleDebug
./gradlew :app:installDebug
```

4. Login with `admin@localhost` / `admin1234` (staff Home) or a `ROLE_USER` seed account for customer bookings.

**Logcat filters:** `OkHttp`, `API_ERROR`, `AUTH_ERROR`. Successful Mockoon traffic looks like `--> GET http://10.0.2.2:8081/api/deliveries`.

### 9.8 Android URL map

| Client | Spring (default) | Mockoon / Prism |
|--------|------------------|-----------------|
| Emulator → host | `http://10.0.2.2:8080/` | `http://10.0.2.2:8081/` |
| Host curl / Postman | `http://localhost:8080/` | `http://localhost:8081/` |
| Physical device | `http://<host-lan-ip>:8080/` | `http://<host-lan-ip>:8081/` |

---

## 10. End-to-end smoke

```bash
# REST health
curl -s http://localhost:8080/actuator/health

# Interim JWT → login
INTERIM=$(curl -s http://localhost:8080/api/auth/getBearerToken)
curl -s -X POST http://localhost:8080/api/auth/login \
  -H "Authorization: Bearer $INTERIM" \
  -H "Content-Type: application/json" \
  -d '{"email":"admin@localhost","password":"admin1234"}'

# Haystack health (if pack is up)
curl -s http://localhost:8000/health

# Mockoon (if npm run mock:mockoon is running)
curl -s http://127.0.0.1:8081/api/deliveries
```

Portal: sign in at http://localhost:5173 with a seed user (for example `alex.tan@example.sg` / `customer123` against live Spring).

Android emulator: login `admin@localhost` / `admin1234`. Confirm Logcat hits `10.0.2.2:8080` (Spring) or `:8081` (Mockoon).

---

## 11. Troubleshooting

| Symptom | What to check |
|---------|----------------|
| Containers cannot resolve each other | `docker network ls` — create `heavy-rental-network` |
| VS Code does not offer “Reopen in Container” | REST pack: `.devcontainer` not promoted to `Heavy-Rental-REST-API/` |
| Portal API errors | Spring not on 8080; CORS origins default to `http://localhost:5173` |
| Haystack quotes `AST-*` ids | `FLEET_BACKEND=fake`; live path needs `sql` + `postgres-haystack` |
| Haystack hostname `db` | Use `postgres-haystack` on this network |
| Sync does nothing | REST primary down — default is **skip** cycle, not wipe local DB |
| Recommend 503 / 504 from portal | Spring circuit breaker / Haystack down; CRUD still works |
| Stripe deposit never completes | Webhook not forwarded (`stripe listen` or `./scripts/dev-with-webhooks.sh`) |
| Replica `pg_is_in_recovery()` is `f` | You opened the without-replica pack, or replica did not bootstrap |
| Gradle sync: unsupported class file / wrong JDK | Gradle JDK is not 17 — Settings → Build Tools → Gradle → JDK 17 |
| `java -version` is 11 or 21 only | Install Temurin 17 and set `JAVA_HOME` (section 9.1) |
| `npm: command not found` | Install Node.js 18+ on the **host** (section 9.2) |
| Mockoon connection refused | Run `npm run mock:mockoon` from `heavy-rental-mobile/`; confirm port **8081** |
| Postman works, emulator login fails | App used `localhost` — emulator must use `10.0.2.2` |
| Empty Delivery List + error banner | Mock/Spring down, or `USE_MOCK_SERVER` does not match the process you started |
| Port 8081 already in use | Stop the other mock/Prism, or set `MOCK_PORT` and align the app URL |
| Login succeeds with a bad password | Expected on Mockoon (canned auth). Use Spring for real 401s |

---

## 12. What this pack does not set up

| Concern | Where |
|---------|--------|
| AWS Academy VPC / ALB / RDS | [heavy-rental-project-instructure-and-cloud-deploy](https://github.com/Heavy-Rental/heavy-rental-project-instructure-and-cloud-deploy) `OPERATOR-GUIDE.md` |
| GitHub Actions CI / image CD | [heavy-rental-project-pipeline-development](https://github.com/Heavy-Rental/heavy-rental-project-pipeline-development) |
| Full system design | [`DOCUMENTATION.md`](DOCUMENTATION.md) |

Local credentials (`postgres`/`postgres`, Neo4j `neo4j`/`heavyrental`) are **dev only**.
