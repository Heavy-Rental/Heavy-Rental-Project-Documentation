<!-- Improved compatibility of back to top link: See: https://github.com/othneildrew/Best-README-Template/pull/73 -->
<a name="readme-top"></a>
<!--
*** Heavy Rental — System Design and Documentation
*** Submission pack for the Heavy Rental multi-repository platform.
-->



<!-- PROJECT SHIELDS -->
<!--
*** I'm using markdown "reference style" links for readability.
*** Reference links are enclosed in brackets [ ] instead of parentheses ( ).
*** See the bottom of this document for the declaration of the reference variables
*** for contributors-url, forks-url, etc. This is an optional, concise syntax you may use.
*** https://www.markdownguide.org/basic-syntax/#reference-style-links
-->
[![Contributors][contributors-shield]][contributors-url]
[![Forks][forks-shield]][forks-url]
[![Stargazers][stars-shield]][stars-url]
[![Issues][issues-shield]][issues-url]
[![MIT License][license-shield]][license-url]
[![LinkedIn][linkedin-shield]][linkedin-url]



<!-- PROJECT LOGO -->
<br />
<div align="center">
  <a href="https://github.com/Heavy-Rental/Heavy-Rental-Project-Documentation">
    <img src="images/logo.png" alt="Logo" width="80" height="80">
  </a>

<h3 align="center">Heavy Rental — System Design and Documentation</h3>

  <p align="center">
    Submission documentation for a heavy-equipment rental platform: Android ops app, React portal, Spring REST API, Haystack recommender, DevContainers, CI/CD, and AWS Academy infra.
    <br />
    <a href="DOCUMENTATION.md"><strong>Explore the docs »</strong></a>
    <br />
    <br />
    <a href="DOCUMENTATION.md">View Documentation</a>
    ·
    <a href="QUICKSTART.md">QuickStart</a>
    ·
    <a href="https://github.com/Heavy-Rental/Heavy-Rental-Project-Documentation/issues">Report Bug</a>
    ·
    <a href="https://github.com/Heavy-Rental/Heavy-Rental-Project-Documentation/issues">Request Feature</a>
  </p>
</div>



<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#about-the-project">About The Project</a>
      <ul>
        <li><a href="#built-with">Built With</a></li>
      </ul>
    </li>
    <li>
      <a href="#getting-started">Getting Started</a>
      <ul>
        <li><a href="#prerequisites">Prerequisites</a></li>
        <li><a href="#installation">Installation</a></li>
      </ul>
    </li>
    <li><a href="#usage">Usage</a></li>
    <li><a href="#roadmap">Roadmap</a></li>
    <li><a href="#contributing">Contributing</a></li>
    <li><a href="#license">License</a></li>
    <li><a href="#contact">Contact</a></li>
    <li><a href="#acknowledgments">Acknowledgments</a></li>
  </ol>
</details>



<!-- ABOUT THE PROJECT -->
## About The Project

[![Product Name Screen Shot][product-screenshot]](DOCUMENTATION.md)

**Heavy Rental** is a multi-repository platform for hiring construction equipment (excavators, boom lifts, scissors lifts, fork lifts). Customers browse fleet, build rental plans, pay a 30% Stripe deposit, and receive AI equipment quotes from a project specification. Field operators mobilise deliveries and complete returns from Android. Admins manage users and utilisation.

This repository is the **system design and documentation pack** for project submission. It does not contain application source. It documents all product and supporting Git repositories with:

| Artifact | Role |
|----------|------|
| [`DOCUMENTATION.md`](DOCUMENTATION.md) | Main submission document: features, architecture, sequence / use case / ERD / class / state / deployment diagrams (Mermaid **and** PlantUML) |
| [`QUICKSTART.md`](QUICKSTART.md) | DevContainer setup for REST API, Haystack FastAPI, and React Web Portal |
| [`openspec/`](openspec/) | Platform OpenSpec (behavior SoT) |
| [`spdd/`](spdd/) | OpenSPDD REASONS canvases (how / not-how) |
| [`adr/`](adr/) | Architecture Decision Records (why) |
| [`repositories/`](repositories/) | Per-repository OpenSpec, OpenSPDD, and ADR |
| [`docs/diagrams/`](docs/diagrams/) | PlantUML `.puml` sources used in the main document |

### Product repositories

| Repository | Role | Stack |
|------------|------|--------|
| [heavy-rental-mobile](https://github.com/Heavy-Rental/heavy-rental-mobile) | Android operations app (today’s deliveries and returns) | Kotlin, Jetpack Compose, Retrofit |
| [heavy-rental-spring-rest-api](https://github.com/Heavy-Rental/heavy-rental-spring-rest-api) | Authenticated business API and OLTP source of truth | Java 21, Spring Boot, PostgreSQL, Stripe |
| [heavy-rental-react-web-portal](https://github.com/Heavy-Rental/heavy-rental-react-web-portal) | Customer, admin, and employee web UI | React 19, TypeScript, Vite, Tailwind |
| [haystack-fast-api](https://github.com/Heavy-Rental/haystack-fast-api) | ML / Haystack recommender (ingest, quote, knowledge Q&A) | Python 3.12, FastAPI, Haystack, Neo4j |

### Supporting repositories

| Repository | Role |
|------------|------|
| [heavy-rental-devcontainer-configuration](https://github.com/Heavy-Rental/heavy-rental-devcontainer-configuration) | Local DevContainer + Compose packs on `heavy-rental-network` |
| [heavy-rental-project-pipeline-development](https://github.com/Heavy-Rental/heavy-rental-project-pipeline-development) | GitHub Actions CI, image release, and Academy CD callers |
| [heavy-rental-project-instructure-and-cloud-deploy](https://github.com/Heavy-Rental/heavy-rental-project-instructure-and-cloud-deploy) | Terraform + Ansible for AWS Academy / Vocareum |

**Trust boundary:** the browser and the Android app call **Spring REST only**. Spring dual-hops to Haystack for recommendations. Haystack **pulls** fleet rows from the REST primary; it never writes the OLTP database.

<p align="right">(<a href="#readme-top">back to top</a>)</p>



### Built With

* [![Kotlin][Kotlin]][Kotlin-url]
* [![Spring Boot][SpringBoot]][SpringBoot-url]
* [![React][React.js]][React-url]
* [![FastAPI][FastAPI]][FastAPI-url]
* [![PostgreSQL][PostgreSQL]][PostgreSQL-url]
* [![Neo4j][Neo4j]][Neo4j-url]
* [![Docker][Docker]][Docker-url]
* [![Terraform][Terraform]][Terraform-url]
* [![AWS][AWS]][AWS-url]

Documentation tooling used in this pack:

* **OpenSpec** — behavior contracts (`SHALL` + scenarios)
* **OpenSPDD** — REASONS Canvas implementation contracts
* **ADR (MADR-short)** — durable architectural decisions
* **Mermaid** — diagrams rendered on GitHub
* **PlantUML** — UML sources in markdown fences and `docs/diagrams/*.puml`

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- GETTING STARTED -->
## Getting Started

This repository is documentation only. To read the submission pack, clone it and open `DOCUMENTATION.md`. To run the product locally, follow [`QUICKSTART.md`](QUICKSTART.md) (DevContainers) and the product repos listed above.

### Prerequisites

To **read** this pack:

* A Markdown viewer that renders GitHub-flavoured Mermaid (GitHub, VS Code Markdown preview)
* Optional: [PlantUML](https://plantuml.com/) or the VS Code PlantUML extension for `.puml` files under `docs/diagrams/`

To **run** the product (see [`QUICKSTART.md`](QUICKSTART.md)):

* [Docker](https://docs.docker.com/get-docker/)
* [Visual Studio Code](https://code.visualstudio.com/)
* VS Code extensions: Remote Development (`ms-vscode-remote.vscode-remote-extensionpack`), Container Tools (`ms-azuretools.vscode-containers`)
* [Android Studio](https://developer.android.com/studio), **Java JDK 17**, and **Node.js 18+ / npm** (Android app + Mockoon on port 8081)
* Git

### Installation

1. Clone this documentation repository
   ```sh
   git clone https://github.com/Heavy-Rental/Heavy-Rental-Project-Documentation.git
   cd Heavy-Rental-Project-Documentation
   ```
2. Open [`DOCUMENTATION.md`](DOCUMENTATION.md) for the full system design (use cases, sequences, ERD).
3. Open [`QUICKSTART.md`](QUICKSTART.md) to create Docker network `heavy-rental-network` and start the three DevContainer packs.
4. Clone the product repositories when you are ready to run code:
   ```sh
   git clone https://github.com/Heavy-Rental/heavy-rental-spring-rest-api.git
   git clone https://github.com/Heavy-Rental/heavy-rental-react-web-portal.git
   git clone https://github.com/Heavy-Rental/haystack-fast-api.git
   git clone https://github.com/Heavy-Rental/heavy-rental-mobile.git
   git clone https://github.com/Heavy-Rental/heavy-rental-devcontainer-configuration.git
   ```

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- USAGE EXAMPLES -->
## Usage

| Need | Start here |
|------|------------|
| Project submission overview, UML, ERD | [`DOCUMENTATION.md`](DOCUMENTATION.md) |
| Local DevContainer setup | [`QUICKSTART.md`](QUICKSTART.md) |
| How OpenSpec / OpenSPDD / ADR fit together | [`docs/spec-governance.md`](docs/spec-governance.md) |
| Platform behavior contracts | [`openspec/`](openspec/) |
| Per-repository specs | [`repositories/`](repositories/) |
| PlantUML sources | [`docs/diagrams/`](docs/diagrams/) |

### Render PlantUML

GitHub renders **Mermaid** in markdown. PlantUML blocks (` ```plantuml `) and `docs/diagrams/*.puml` need a PlantUML previewer:

* VS Code: extension `jebbs.plantuml`
* CLI: `plantuml docs/diagrams/*.puml`
* [Kroki](https://kroki.io/) or the [PlantUML online server](https://www.plantuml.com/plantuml/uml/)

_For the as-built HTTP map, prefer the Spring REST [`DOCUMENTATION.md`](https://github.com/Heavy-Rental/heavy-rental-spring-rest-api/blob/develop/DOCUMENTATION.md) and the contracts under each product repo’s `openspec/`._

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- ROADMAP -->
## Roadmap

- [x] Main submission documentation (`DOCUMENTATION.md`) with Mermaid and PlantUML
- [x] DevContainer QuickStart for REST, Haystack, and Web Portal packs
- [x] OpenSpec + OpenSPDD + ADR for all product and supporting repositories
- [x] Fill this README while retaining the Best-README-Template structure
- [ ] Keep specs aligned when product repos archive OpenSpec changes
- [ ] Optional PNG/SVG export of PlantUML diagrams for PDF submission packs

See the [open issues](https://github.com/Heavy-Rental/Heavy-Rental-Project-Documentation/issues) for a full list of proposed features (and known issues).

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- CONTRIBUTING -->
## Contributing

Contributions are what make the open source community such an amazing place to learn, inspire, and create. Any contributions you make are **greatly appreciated**.

If a suggestion would make this documentation pack better, fork the repo and create a pull request. You can also simply open an issue with the tag "enhancement".
Don't forget to give the project a star! Thanks again!

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Follow [`docs/spec-governance.md`](docs/spec-governance.md) for behavior-changing documentation (OpenSpec proposal → specs → design → adr → tasks)
4. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
5. Push to the Branch (`git push origin feature/AmazingFeature`)
6. Open a Pull Request

Do not edit an **accepted** ADR in place. Add a new ADR that supersedes it.

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- LICENSE -->
## License

Distributed under the MIT License. See `LICENSE.txt` for more information.

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- CONTACT -->
## Contact

Heavy Rental project team — [github.com/Heavy-Rental](https://github.com/Heavy-Rental)

Project Link: [https://github.com/Heavy-Rental/Heavy-Rental-Project-Documentation](https://github.com/Heavy-Rental/Heavy-Rental-Project-Documentation)

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- ACKNOWLEDGMENTS -->
## Acknowledgments

* [Best-README-Template](https://github.com/othneildrew/Best-README-Template)
* [OpenSpec](https://github.com/Fission-AI/OpenSpec)
* [OpenSPDD](https://github.com/gszhangwei/open-spdd)
* [Architecture Decision Records](https://adr.github.io/) / [MADR](https://adr.github.io/madr/)
* [Mermaid](https://mermaid.js.org/)
* [PlantUML](https://plantuml.com/)
* [Choose an Open Source License](https://choosealicense.com)
* [Img Shields](https://shields.io)
* Product and infra sources of truth in the [Heavy-Rental](https://github.com/Heavy-Rental) organization

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- MARKDOWN LINKS & IMAGES -->
<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->
[contributors-shield]: https://img.shields.io/github/contributors/Heavy-Rental/Heavy-Rental-Project-Documentation.svg?style=for-the-badge
[contributors-url]: https://github.com/Heavy-Rental/Heavy-Rental-Project-Documentation/graphs/contributors
[forks-shield]: https://img.shields.io/github/forks/Heavy-Rental/Heavy-Rental-Project-Documentation.svg?style=for-the-badge
[forks-url]: https://github.com/Heavy-Rental/Heavy-Rental-Project-Documentation/network/members
[stars-shield]: https://img.shields.io/github/stars/Heavy-Rental/Heavy-Rental-Project-Documentation.svg?style=for-the-badge
[stars-url]: https://github.com/Heavy-Rental/Heavy-Rental-Project-Documentation/stargazers
[issues-shield]: https://img.shields.io/github/issues/Heavy-Rental/Heavy-Rental-Project-Documentation.svg?style=for-the-badge
[issues-url]: https://github.com/Heavy-Rental/Heavy-Rental-Project-Documentation/issues
[license-shield]: https://img.shields.io/github/license/Heavy-Rental/Heavy-Rental-Project-Documentation.svg?style=for-the-badge
[license-url]: https://github.com/Heavy-Rental/Heavy-Rental-Project-Documentation/blob/master/LICENSE.txt
[linkedin-shield]: https://img.shields.io/badge/-LinkedIn-black.svg?style=for-the-badge&logo=linkedin&colorB=555
[linkedin-url]: https://linkedin.com
[product-screenshot]: images/screenshot.png
[Kotlin]: https://img.shields.io/badge/Kotlin-7F52FF?style=for-the-badge&logo=kotlin&logoColor=white
[Kotlin-url]: https://kotlinlang.org/
[SpringBoot]: https://img.shields.io/badge/Spring%20Boot-6DB33F?style=for-the-badge&logo=springboot&logoColor=white
[SpringBoot-url]: https://spring.io/projects/spring-boot
[React.js]: https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB
[React-url]: https://reactjs.org/
[FastAPI]: https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white
[FastAPI-url]: https://fastapi.tiangolo.com/
[PostgreSQL]: https://img.shields.io/badge/PostgreSQL-316192?style=for-the-badge&logo=postgresql&logoColor=white
[PostgreSQL-url]: https://www.postgresql.org/
[Neo4j]: https://img.shields.io/badge/Neo4j-018BFF?style=for-the-badge&logo=neo4j&logoColor=white
[Neo4j-url]: https://neo4j.com/
[Docker]: https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white
[Docker-url]: https://www.docker.com/
[Terraform]: https://img.shields.io/badge/Terraform-7B42BC?style=for-the-badge&logo=terraform&logoColor=white
[Terraform-url]: https://www.terraform.io/
[AWS]: https://img.shields.io/badge/AWS-232F3E?style=for-the-badge&logo=amazonaws&logoColor=white
[AWS-url]: https://aws.amazon.com/
