# Project Proposal

**Task:** DIP-51
**Status:** Draft for supervisor review

## 1. Project title

Development of an intelligent system for detecting defects in Java source code based on static analysis and machine learning methods

*(Russian: «Разработка интеллектуальной системы обнаружения дефектов в программном коде на языке Java на основе статического анализа и методов машинного обучения»)*

## 2. Team and supervisor

| Member | Group | Responsibilities |
| --- | --- | --- |
| Sergey Chepurnenko | SE-2422 | Analysis, design, implementation, testing, documentation (individual project) |

Supervisor: Aigerim Bakiyeva

## 3. Problem statement

Java developers rely on static analysis tools such as SpotBugs, PMD and SonarQube to find defects before the code is reviewed, tested or released. These tools work with predefined rules: a defect is reported only if the code matches a known pattern. This leads to two practical problems:

1. **Too many irrelevant warnings.** Rule-based tools report many warnings that developers consider false or unimportant. As a result, developers spend time filtering the output or stop paying attention to it.
2. **Missed defects.** Defects that do not match any predefined rule are not reported at all, so they reach testing or production.

Research on machine learning for defect detection and defect prediction shows that models trained on real bug data can learn patterns of defective code that are not described by fixed rules. However, most of these approaches remain research prototypes. They are not packaged as a tool that a developer can run on a project and use to understand where the likely defects are and why.

This project addresses the gap between rule-based static analyzers and research ML models: it combines static analysis with a machine learning model in one tool that reports likely defects with their location and an explanation.

*Evidence status:* the statements above are working hypotheses. They will be supported or corrected by the literature review (DIP-12) and by interviews with teachers of programming courses and Java developers (DIP-52). Confirmed findings and remaining assumptions will be separated in `docs/relevance.md`.

## 4. Definition of a defect

In this project, a **defect** is an error in the source code that can cause incorrect program behaviour (a bug), for example a possible null-pointer dereference, a resource that is not closed, an incorrect comparison or an error in exception handling.

Code smells and style issues (long methods, naming, formatting) are **not** treated as defects in this project.

The exact list of defect categories that the system supports will be fixed in the requirements specification (DIP-14), based on the available labelled data.

## 5. Target users

| User group | Need |
| --- | --- |
| Java developers (primary users) | Check their code for likely bugs before code review or before merging |
| Code reviewers and team leads | Focus review effort on the parts of the code that are most likely to contain defects |
| Students and teachers of Java courses | Find typical errors in student projects and understand why the code is risky |

## 6. Aim

To develop a web-based system that detects likely defects in Java source code by combining static analysis with machine learning, and to evaluate its accuracy against existing rule-based tools.

## 7. Objectives

1. Review the literature on machine learning methods for defect detection and defect prediction in source code.
2. Compare existing defect detection tools for Java against a consistent set of criteria.
3. Collect and analyse requirements through interviews with teachers of programming courses and Java developers.
4. Prepare a labelled dataset of Java code with known defects, based on public bug datasets (candidates: Defects4J, Unified Bug Dataset, PROMISE).
5. Implement a static analysis module that parses Java source code and extracts code metrics and structural features.
6. Train and compare several machine learning models (for example, random forest, gradient boosting and a neural baseline) for identifying defective code.
7. Develop a web application where a user uploads a Java project and receives a report with the location, type, confidence and explanation of each likely defect.
8. Evaluate the system against rule-based tools (SpotBugs as the main baseline, PMD as an additional one) using precision, recall, F1-score and analysis time.

## 8. Expected outcomes

- A working web application that analyses a Java project and produces a defect report.
- A trained machine learning model and a reproducible training pipeline.
- A description of the dataset and of the features used by the model.
- An evaluation report comparing the system with SpotBugs and PMD.
- Project documentation: requirements, architecture, user guide and test results.

## 9. Project scope

**In scope:**

- Analysis of Java source code files (a single file or a whole project uploaded as an archive).
- Detection of a defined set of defect categories (see section 4).
- Defect localisation at file, class and method level, with line numbers where possible.
- Explanation for each reported defect: which rule or which code features led to the result.
- Web interface for uploading a project and viewing and exporting the report.
- Comparison with SpotBugs and PMD on the same data.

**Out of scope:**

- Programming languages other than Java.
- Automatic fixing of defects.
- Plugins for IDEs (IntelliJ IDEA, Eclipse, VS Code) and CI/CD integration (possible future work).
- Dynamic analysis (running the analysed program) and analysis of compiled bytecode.
- Security vulnerability scanning as a separate goal.
- User accounts, teams and other multi-user features.

## 10. Engineering complexity

The project includes several technically distinct parts that have to work together:

- parsing Java source code and building an abstract syntax tree;
- feature engineering from code metrics and code structure;
- preparing a labelled dataset from public bug data;
- training, tuning and comparing machine learning models;
- explaining model predictions to the user;
- a web application with project upload, background analysis and a report view;
- an experimental comparison with existing tools.

## 11. Key decisions

| Decision | Choice | Status |
| --- | --- | --- |
| User interface | Web application | Waiting for supervisor confirmation |
| What counts as a defect | Errors in code (bugs), not code smells | Waiting for supervisor confirmation |
| Main baseline for evaluation | SpotBugs (PMD as an additional baseline) | Proposed |
| Implementation language and libraries | To be selected in the technology comparison (DIP-53) | Open |

## 12. Related documents

- Literature review: `docs/literature-review.md` (DIP-12)
- Existing systems comparison: `docs/existing-systems.md` (DIP-13)
- Requirements: `docs/requirements.md` (DIP-14)
- Evaluation plan: `docs/evaluation-plan.md` (DIP-55)
