# Evaluation and Test Plan

**Task:** DIP-55

**Status:** Draft. Targets are first estimates and may change after the first experiments. Labelling, data split and correct detections updated after the supervisor's review on 24 October 2026.

## 1. Goal

The aim of the project is a system that finds likely defects in Java code and is compared with rule-based tools. This plan describes how this will be checked:

- **model evaluation** (Sections 2–6): how well the system finds defective methods compared with SpotBugs, PMD and simple baselines;
- **software testing** (Section 7): whether the system meets the requirements in `docs/requirements.md`.

## 2. Data

| Dataset | Content | Use |
| --- | --- | --- |
| Defects4J 3.0.1 | 854 real bugs from 17 Java projects; each fix is cleaned from unrelated changes [1] | Training and testing |
| GitBug-Java | 199 real bugs from 55 projects, fixed in 2023 [2] | Testing only, never used for training |

**Labels.** For each bug I compare the code before and after the fix:

- each changed or deleted line of the code before the fix is mapped to its method, and this method is **defective** (if the fix only adds lines, the method where they are added);
- the other methods in the same files are **not known to be defective**: they are used as clean examples, but they can still contain bugs that were never found;
- changes only in comments or spaces are ignored; bugs whose fix changes only code outside methods are left out and counted.

GitBug-Java gives the commit before and after each fix and the patch [2], so I only need the source code. The full GitBug-Java environment (about 240 GB) is not needed, because the project does not run tests.

## 3. How the data is split

A model can look much better than it is if test data leaks into training. In one study, F1 dropped from 0.88 to 0.31 after such problems were fixed (literature review [8]). So:

- **Split by project.** Each of the 17 Defects4J projects is used once as the test project, and the model is trained on the other 16 (NFR-02).
- **Final test on new bugs.** The final model is trained on all of Defects4J and tested once on GitBug-Java.
- **No duplicates.** Methods with the same code in training and test data are removed from the test data.
- **One bug in one set.** All methods of one bug are always in the same set (this holds with the split by project).
- **Validation set.** Model settings are chosen only on the training projects; the test project is used once, for the final result.
- **Only the code before the fix** is used to compute features.

## 4. What the system is compared with

**Models of this project:** random forest and gradient boosting (scikit-learn; XGBoost and LightGBM are also tried) and a simple neural network (scikit-learn MLP) for comparison. The best model is used in the web application.

| Baseline | How it works | Why |
| --- | --- | --- |
| All methods | Reports every method | Shows how often a method is defective by chance |
| Method size | Reports long methods (threshold chosen on training data) | A simple rule; the model should do better than this |
| SpotBugs | Bug patterns, "Correctness" category only [3, 4] | Main rule-based tool |
| PMD | Rules, "Error Prone" category only [5] | Second rule-based tool |

I use only the bug-related categories of SpotBugs and PMD, because this project is about bugs, not style. A tool "reports" a method if one of its warnings is on a line inside that method.

**Correct detection.** The unit is the method: a method reported by the model or by a tool is a correct detection if the fix changed it. The category is not needed for this; the two rule checks are tested separately (FR-05).

SpotBugs works on compiled code [3], so each Defects4J project is compiled first. The SpotBugs documentation says that class files from JDK 10 and older are not supported [3], so I will check this on a few projects first and use an older SpotBugs version if needed.

## 5. Metrics and targets

| Metric | Meaning |
| --- | --- |
| Precision | Of the reported methods, how many are really defective |
| Recall | Of the defective methods, how many are reported |
| F1-score | Balance of precision and recall |
| Bugs found | Share of bugs where at least one defective method is reported |
| False positives | Reported methods that the fix did not change, per project |
| Analysis time | Time to analyse one project |

**Targets (first estimates):**

- the model has a higher F1 than the simple baselines;
- the model has a higher recall than SpotBugs and PMD;
- a project with up to 10,000 lines is analysed in at most 2 minutes (NFR-01).

Results that do not meet the targets will also be reported.

## 6. Measurement conditions

- All experiments run on my laptop without a GPU; the processor and memory are written in the report.
- Dataset versions, tool versions (SpotBugs, PMD), library versions and random seeds are saved (NFR-04).
- Each model is trained 5 times with different fixed seeds; the average is reported.
- Analysis time is measured on three open-source projects of up to 10,000 lines.
- The results are saved as CSV files in `results/` and described in `docs/evaluation-report.md`.

## 7. Testing plan

| Level | What is tested | Tool | Requirements |
| --- | --- | --- | --- |
| Unit tests | Project loader, parser, feature extractor, report builder | pytest | FR-02, FR-03, NFR-09 |
| Integration tests | The full analysis on small sample projects | pytest | FR-04 to FR-07 |
| API tests | Upload, status, report and export | pytest, FastAPI test client | FR-01, FR-08, FR-10 to FR-12 |
| System tests | The whole web application, checked by hand against the acceptance criteria | Checklist | All requirements |

**Test data:** small Java files with known metric values; one file with a known defect for each category; files with Java 8–17 features; bad inputs (empty archive, non-Java file, file with syntax errors, archive over 50 MB).

**Other checks:**

- Privacy (NFR-05): network activity is watched during an analysis; there should be no outgoing requests.
- Usability (NFR-07): 3 people (for example, interview participants) upload a project and explain one warning in their own words.
- Deployment (NFR-10): the system is started on a clean machine with one command.

## 8. Risks for the evaluation

- Not every changed method is really the cause of a bug, and some "clean" methods may have unknown bugs, so labels are not perfect.
- Defects4J bugs are old; this is why GitBug-Java is used as a second test set.
- GitBug-Java is small (199 bugs), so its results are less certain.

## 9. References

[1] Defects4J, GitHub repository, version 3.0.1. https://github.com/rjust/defects4j

[2] GitBug-Java, GitHub repository (README and `data/bugs`). https://github.com/gitbugactions/gitbug-java

[3] SpotBugs, "Introduction", SpotBugs 4.10.5 documentation. https://spotbugs.readthedocs.io/en/stable/introduction.html

[4] SpotBugs, "Bug descriptions". https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html

[5] PMD, "Error Prone" rule category for Java. https://docs.pmd-code.org/latest/pmd_rules_java_errorprone.html

References in the form "literature review [n]" point to `docs/literature-review.md`.
