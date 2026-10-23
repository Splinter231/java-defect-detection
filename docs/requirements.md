# Requirements Specification

**Task:** DIP-14

**Status:** Draft. Section 6 is added from the first interview (DIP-52).

## 1. Introduction

This document lists the functional and non-functional requirements of the system from the proposal (`docs/proposal.md`).

**Priorities (MoSCoW):** **Must** — needed for the system to work; **Should** — important, planned for the final version; **Could** — if there is time; **Won't** — not planned (Section 5).

**Sources:** P — proposal; L[n] — literature review, reference [n]; S — comparison of existing systems; I — interviews (`docs/interviews/`).

Numbers in the acceptance criteria (sizes, times, percentages) are first estimates. They will be checked with the supervisor and after the first experiments.

## 2. Users

| User | Main scenario |
| --- | --- |
| Java developer | Uploads a project and checks the list of likely defects before code review |
| Code reviewer or team lead | Uses the report to decide which code to review more carefully |
| Teacher or student | Checks a student project for typical errors and reads why the code is risky |

## 3. Functional requirements

| ID | Requirement | Priority | Acceptance criterion | Source |
| --- | --- | --- | --- | --- |
| FR-01 | The user can upload a Java project as a ZIP archive or a single `.java` file | Must | A ZIP up to 50 MB with `.java` files is accepted; an archive without `.java` files is rejected with a clear message | P |
| FR-02 | The system parses every `.java` file | Must | Files that cannot be parsed are listed in the report with the reason; other files are still analysed | P |
| FR-03 | The system computes code metrics and other features for each method | Must | Unit tests check the values on sample files with known metrics | P |
| FR-04 | A machine learning model gives each method a score from 0 to 1 (probability of a defect) | Must | Every analysed method has a score; the same input always gives the same score | P |
| FR-05 | The system shows the likely defect category when possible (for example null dereference, resource not closed, wrong comparison, exception handling error) | Should | For test files with a known defect of each category, the right category is shown | P |
| FR-06 | Each result shows the file, class, method and lines | Must | Every report entry has the file path, class and method; lines are shown when available | P, L[10] |
| FR-07 | Each result has an explanation: the main code features that led to the score, in simple words | Must | Every entry shows at least three factors with a short text | L[1], L[12] |
| FR-08 | The report lists results sorted by score | Must | Entries are sorted by score; the user can filter by file and by minimum score | P |
| FR-09 | The user can open the code of a method with the related lines highlighted | Should | Clicking an entry opens the code with the lines highlighted | P, L[1] |
| FR-10 | The user can export the report | Should | JSON and CSV export contain all fields of the report | P |
| FR-11 | The user can mark a result as a false positive | Could | The mark is saved and shown; marked entries can be hidden | S, L[9] |
| FR-12 | The system shows the status of a running analysis | Should | The page shows the status: queued, running, finished or failed | P |
| FR-13 | A training script builds the model from public bug datasets | Must | Running it with the same random seed gives the same model and the same metrics | L[2], L[4] |
| FR-14 | An evaluation script computes precision, recall and F1 of the system, SpotBugs and PMD on the same data | Must | The script outputs a table with the three metrics for each tool | P, L[3], L[9] |

## 4. Non-functional requirements

| ID | Type | Requirement | Priority | Acceptance criterion | Source |
| --- | --- | --- | --- | --- | --- |
| NFR-01 | Performance | A project of up to 10,000 lines is analysed in at most 2 minutes on a laptop without a GPU | Should | Measured on three open-source projects | P |
| NFR-02 | Evaluation | The model is tested on projects that were not used for training | Must | The evaluation report shows that test projects are not in the training data | L[8] |
| NFR-03 | Evaluation | Results are compared with simple baselines, SpotBugs and PMD | Must | All of them are in the evaluation report on the same test data | L[8], L[3] |
| NFR-04 | Reproducibility | Training and evaluation can be repeated | Must | Dataset versions, random seeds and library versions are saved; a repeated run gives the same metrics | L[6] |
| NFR-05 | Privacy | Uploaded code is not sent to other services | Must | No outgoing network requests during analysis; uploaded files are deleted after 24 hours | S |
| NFR-06 | Robustness | Bad input does not crash the system | Must | An empty archive, a non-Java file and a file with syntax errors give an error message or a partial report | P |
| NFR-07 | Usability | A new user can upload a project and understand the report without help | Should | 3 test users each upload a project and explain one warning within 5 minutes | L[1] |
| NFR-08 | Compatibility | Modern Java syntax is supported | Should | Test files with Java 8 to Java 17 features are parsed without errors | P |
| NFR-09 | Maintainability | The analysis code is covered by automated tests | Should | Test coverage of the analysis code is at least 70% | P |
| NFR-10 | Deployment | The system starts with one command | Should | On a clean machine with the listed prerequisites, one command starts the web interface | P |

## 5. Constraints and out of scope

**Constraints:** one developer; training without a GPU; only public datasets that allow research use.

**Won't (not planned):** other languages, automatic fixing, IDE plugins and CI/CD integration, dynamic analysis, security scanning as a separate goal, user accounts.

## 6. Requirements from interviews

Source: interview P1 ([interview-01.md](interviews/interview-01.md)), see also `docs/relevance.md`.

| ID | Requirement | Priority | Acceptance criterion | Source |
| --- | --- | --- | --- | --- |
| FR-15 | Each result shows a severity level (high, medium, low) next to the score | Should | Every result in the report has a severity level; the level depends on the defect category and the score | I (P1, Q7) |
| FR-16 | The explanation describes what can happen because of the defect and, if possible, how to fix it | Could | For each defect category there is a short risk scenario and a fix hint | I (P1, Q7) |
| FR-17 | When the same project is analysed again, the report shows which results are new | Could | Results that were in the previous analysis of the project are marked as old | I (P1, Q7, Q8) |
| FR-18 | A teacher can see a summary over several analysed projects | Could | One page lists the analysed projects with the number of results and the highest score | I (P1, Q8) |

The interview also supports existing requirements: FR-07 (explanation), FR-11 (mark as false positive), FR-04 (the same input gives the same score) and NFR-05 (code is not sent to other services). An IDE plugin and CI integration were also mentioned; they stay out of scope (Section 5) and are possible future work.
