# Project Proposal

**Task:** DIP-51

**Status:** Draft for supervisor review

## 1. Project title

Development of an intelligent system for detecting defects in Java source code based on static analysis and machine learning methods

(Russian: «Разработка интеллектуальной системы обнаружения дефектов в программном коде на языке Java на основе статического анализа и методов машинного обучения»)

## 2. Team and supervisor

| Member | Group | Responsibilities |
| --- | --- | --- |
| Sergey Chepurnenko | SE-2422 | All work: analysis, design, development, testing, documentation (individual project) |

Supervisor: Aigerim Bakiyeva

## 3. Problem statement

Java developers use static analysis tools like SpotBugs, PMD and SonarQube to find errors before code review or release. These tools work with fixed rules, so they only report code that matches a known pattern. This causes two problems:

1. **Many useless warnings.** In a study of six tools on 47 Java projects, only 18% to 86% of the checked warnings were correct [9]. Developers say that false positives and badly presented warnings are reasons why they do not use such tools [1].
2. **Many real bugs are missed.** Three bug detectors together found only 27 of 594 real Java bugs (4.5%) [3].

Machine learning models for defect prediction are well studied, but a review of 102 studies says there is "still little evidence on the practicability and adoption of defect prediction models in industry" [7].

The idea of this project is to combine static analysis with a machine learning model in one tool that shows likely bugs, where they are and why the tool thinks so.

The numbers [n] refer to the literature review (`docs/literature-review.md`). Whether these problems are important for real users is checked in interviews (`docs/relevance.md`).

## 4. What counts as a defect

In this project a **defect** is an error in the code that can make the program work incorrectly (a bug). Examples: a possible null pointer dereference, a resource that is not closed, a wrong comparison, an error in exception handling.

Code smells and style problems (long methods, naming, formatting) are **not** counted as defects.

## 5. Target users

| User group | What they need |
| --- | --- |
| Java developers | Check their code for likely bugs before code review |
| Code reviewers and team leads | Know which parts of the code to review more carefully |
| Teachers and students of Java courses | Find typical errors in student projects and understand why the code is risky |

## 6. Aim

To develop a web system that finds likely defects in Java code using static analysis and machine learning, and to compare its results with existing rule-based tools.

## 7. Objectives

1. Review the literature on defect detection with static analysis and machine learning.
2. Compare existing tools for finding defects in Java code.
3. Interview teachers and Java developers to collect requirements.
4. Prepare a labelled dataset of Java methods from public bug datasets (Defects4J and GitBug-Java).
5. Build a module that parses Java code and computes code metrics and other features.
6. Train and compare several models (random forest, gradient boosting and a simple neural network).
7. Build a web application where the user uploads a Java project and gets a report with the location, type, score and explanation of each likely defect.
8. Compare the system with SpotBugs and PMD using precision, recall, F1-score and analysis time.

## 8. Expected outcomes

- A working web application that analyses a Java project and shows a report.
- A trained model and scripts to repeat the training.
- An evaluation report that compares the system with SpotBugs and PMD.
- Project documentation: requirements, architecture, test results and a user guide.

## 9. Scope

**In scope:**

- Java source code (one file or a whole project as a ZIP archive).
- A fixed list of defect types (Section 4).
- Location of each defect: file, class, method and lines where possible.
- An explanation for each result.
- A web interface to upload a project and view or export the report.
- Comparison with SpotBugs and PMD.

**Out of scope:**

- Other programming languages.
- Automatic fixing of defects.
- IDE plugins and CI/CD integration.
- Running the analysed program (dynamic analysis).
- Security scanning as a separate goal.
- User accounts.

## 10. Engineering complexity

The project has several different technical parts that must work together:

- parsing Java code and working with its syntax tree;
- computing features from the code;
- building a labelled dataset from public bug data;
- training and comparing machine learning models;
- explaining the model's results to the user;
- a web application with file upload, background analysis and a report;
- an experiment that compares the system with existing tools.

## 11. Key decisions

| Decision | Choice | Status |
| --- | --- | --- |
| User interface | Web application | Waiting for supervisor confirmation |
| What counts as a defect | Bugs, not code smells | Waiting for supervisor confirmation |
| Tools to compare with | SpotBugs (main), PMD (additional) | Proposed |
| Technologies | Python, tree-sitter, scikit-learn, SHAP, FastAPI, SQLite (`docs/technology-comparison.md`) | Proposed |
