# Java Defect Detection

An intelligent system for detecting defects in Java source code using static analysis and machine learning.

Diploma project, Software Engineering.

## Problem

Rule-based static analyzers for Java (PMD, SpotBugs, SonarQube) only find defects that match predefined rules and can produce many false positives, so developers spend time filtering warnings. *(Hypothesis, to be verified in interviews.)*

## Target users

- Java developers checking code before code review
- Team leads and code reviewers
- Students and teachers of Java courses

## Expected outcomes

- A tool that analyzes a Java project and reports likely defects with location and explanation
- An ML model compared against rule-based tools (PMD, SpotBugs)
- An evaluation report with precision, recall, F1 and analysis time

## Team

| Member | Responsibilities |
| --- | --- |
| Sergey Chepurnenko | Analysis, design, development, testing |

Supervisor: Aigerim Bakiyeva

## Scope

**In scope:** analysis of Java source files, detection of a defined set of defect types, a report for the user (web interface or command line, to be decided).

**Out of scope:** other programming languages, automatic fixing of defects, IDE plugin.

## Repository structure

| Folder | Contents |
| --- | --- |
| `src/` | Source code |
| `tests/` | Tests |
| `docs/` | Project documentation (proposal, requirements, analysis, plans) |
| `diagrams/` | UML and architecture diagrams |
| `config/` | Configuration files |

## Status

Analysis and design stage. No runnable code yet.

## Technologies

To be selected, see `docs/technology-comparison.md`.

## Links

- Task tracker (YouTrack): https://java-defect-detection.youtrack.cloud/issues/DIP
- Documentation: [docs/](docs/)

## Setup and run

Will be added when runnable code is available.
