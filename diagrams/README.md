# diagrams

UML and architecture diagrams of the system. Each diagram has an editable PlantUML source (`.puml`) and exported images (`.png`, `.svg`).

| Diagram | Source | Export | Described in |
| --- | --- | --- | --- |
| System context | `system-context.puml` | `system-context.png`, `system-context.svg` | `docs/architecture.md`, Section 2 |
| Use case | `use-case.puml` | `use-case.png`, `use-case.svg` | `docs/architecture.md`, Section 3 |
| Component (draft) | `component.puml` | `component.png`, `component.svg` | `docs/architecture.md`, Section 4 |
| Sequence: analyse a project | `sequence-analyse-project.puml` | `sequence-analyse-project.png`, `sequence-analyse-project.svg` | `docs/architecture.md`, Section 5 |
| Data model (draft) | `data-model.puml` | `data-model.png`, `data-model.svg` | `docs/architecture.md`, Section 6 |

To regenerate the images with PlantUML (https://plantuml.com): `java -jar plantuml.jar -tpng *.puml` and `java -jar plantuml.jar -tsvg *.puml`.
