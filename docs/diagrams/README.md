# PlantUML diagram sources

These files twin the diagrams in [`DOCUMENTATION.md`](../../DOCUMENTATION.md). Open them with the PlantUML CLI, VS Code (`jebbs.plantuml`), or [the PlantUML server](https://www.plantuml.com/plantuml/uml/).

| File | Kind |
|------|------|
| `context.puml` | Component / context |
| `usecase-system.puml` | Use case |
| `usecase-surfaces.puml` | Use case (portal vs mobile) |
| `seq-auth.puml` | Sequence |
| `seq-booking-pay.puml` | Sequence |
| `seq-recommender.puml` | Sequence |
| `seq-delivery.puml` | Sequence |
| `seq-merge.puml` | Sequence |
| `erd.puml` | Entity relationship |
| `seq-cloud.puml` | Sequence (Academy request path) |
| `class-spring.puml` | Class |
| `class-android.puml` | Class |
| `state-booking.puml` | State |
| `deployment-academy.puml` | Deployment |

Render all:

```bash
plantuml docs/diagrams/*.puml
```
