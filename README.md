# Java Defect Detection

A web system that finds likely defects (bugs) in Java code using static analysis and machine learning.

Diploma project, Software Engineering, Astana IT University.

## Problem

Tools like SpotBugs, PMD and SonarQube find errors with fixed rules. Studies show that many of their warnings are wrong and that they miss most real bugs (see the [literature review](docs/literature-review.md)). This project combines static analysis with a machine learning model and explains each result to the user.

## Target users

- Java developers who check code before code review
- Code reviewers and team leads
- Teachers and students of Java courses

## Expected outcomes

- A web application: the user uploads a Java project and gets a report with likely defects, their location, a score and an explanation
- A trained model and scripts to repeat the training
- A comparison with SpotBugs and PMD (precision, recall, F1, analysis time)

## Team

| Member | Responsibilities |
| --- | --- |
| Sergey Chepurnenko (SE-2422) | Analysis, design, development, testing, documentation (individual project) |

Supervisor: Aigerim Bakiyeva

## Scope

**In scope:** Java source code, a fixed list of bug types, location and explanation of each result, a web interface with report export, comparison with SpotBugs and PMD.

**Out of scope:** other languages, automatic fixing, IDE plugins, security scanning, user accounts.

## Status

Analysis and design are done for pre-defense 1. Development starts with the training data and the Java parser (see the [project plan](docs/project-plan.md)).

## Technologies

Python, tree-sitter (Java parser), scikit-learn, SHAP (explanations), FastAPI with Jinja2 (web), SQLite (storage). See the [technology comparison](docs/technology-comparison.md).

## Prototype

![Report screen](docs/prototype/4-report.png)

All screens: [docs/prototype](docs/prototype/README.md). Figma file: https://www.figma.com/design/pSddtE9uL8kJwAsBiiZxbe/Java-Defect-Detection---Prototype

## Documentation

| Document | Task |
| --- | --- |
| [Proposal](docs/proposal.md) | DIP-51 |
| [Literature review](docs/literature-review.md) | DIP-12 |
| [Existing systems](docs/existing-systems.md) | DIP-13 |
| [Interview questions](docs/interviews/questions.md), [interviews](docs/interviews/README.md), [evidence of relevance](docs/relevance.md) | DIP-52 |
| [Requirements](docs/requirements.md) | DIP-14 |
| [Technology comparison](docs/technology-comparison.md) | DIP-53 |
| [Architecture](docs/architecture.md) and [diagrams](diagrams/README.md) | DIP-15, DIP-16, DIP-17 |
| [Prototype](docs/prototype/README.md) | DIP-54 |
| [Evaluation and test plan](docs/evaluation-plan.md) | DIP-55 |
| [Project plan and risks](docs/project-plan.md) | DIP-56 |
| [Supervisor's feedback](docs/supervisor-feedback.md) | DIP-57 |
| [Pre-defense 1 submission note](docs/pre-defense-1.md) | DIP-58 |

Task tracker (YouTrack): https://java-defect-detection.youtrack.cloud/issues/DIP

## Repository structure

| Folder | Contents |
| --- | --- |
| `src/` | Source code |
| `tests/` | Tests |
| `docs/` | Documentation |
| `diagrams/` | Diagrams (PlantUML sources and images) |
| `config/` | Configuration files |

## Setup and run

Will be added with the first working version.
