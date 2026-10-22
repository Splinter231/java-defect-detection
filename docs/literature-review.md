# Literature Review

**Task:** DIP-12

**Status:** Draft

## 1. Method

The review tries to answer four questions:

1. How well do rule-based static analysis tools find real bugs in Java code?
2. How is machine learning used to find defects or to filter tool warnings, and how reliable are the results?
3. Which public datasets of real Java bugs can be used for training and testing?
4. What do new approaches that combine static analysis with large language models (LLMs) add?

**Where I searched:** Google Scholar, arXiv, IEEE Xplore and ACM Digital Library, with queries such as `software defect prediction machine learning`, `static analysis false positives`, `static bug detectors Defects4J` and `Java bug benchmark`.

**Which sources were included:** the paper is about bugs (not only code smells or style), uses Java or can be applied to Java, is peer-reviewed or is official documentation of a tool used in the project, and is freely available. Most sources are from 2021–2026; older papers are included only if they are key works (a widely used dataset or an important study).

**Result:** 15 sources: 13 scientific papers (9 of them from 2021–2026) and 2 tool documentations. Most papers are from top software engineering conferences (ICSE, ASE, MSR, ISSTA) or from Q1–Q2 journals.

**Limitations and gaps:** in Table 2 and Section 3.5 I only list limitations and open problems that the authors of each paper wrote themselves. The column "Use in this project" is my own interpretation.

## 2. Analysis tables

### Table 1. What each source did and found

| # | Source | Approach | Data | Key results |
| --- | --- | --- | --- | --- |
| 1 | Johnson et al., 2013 [1] | Interviews with developers about static analysis tools | 20 developers | False positives and badly presented warnings stop developers from using the tools; all but one had problems understanding the results |
| 2 | Just et al., 2014 [2] | Database of real Java bugs (Defects4J) | First 357 bugs from 5 projects; now 854 bugs from 17 projects | Each bug has a buggy version, a fixed version and a test that shows the bug |
| 3 | Habib and Pradel, 2018 [3] | Ran three bug detectors on real bugs | Error Prone, Infer and SpotBugs on 594 bugs from 15 Java projects | Together they found 27 of 594 bugs (4.5%); SpotBugs found 18 of them; many missed bugs are domain-specific and match no bug pattern |
| 4 | Ferenc et al., 2020 [4] | Joined public Java bug datasets and recomputed code metrics with one tool | 5 datasets, class and file level | Recomputed metrics differ significantly from the original ones; bug prediction tested with a decision tree |
| 5 | Yang et al., 2021 [5] | Classify tool warnings as actionable or not | FindBugs warnings from 9 Java projects | A linear SVM reached median recall 96.1% and median AUC 99.5%; the authors recommend simple models over deep learning for this data |
| 6 | Pornprasit and Tantithamthavorn, 2021 [6] | JITLine: random forest predicts bug-introducing commits; LIME shows risky lines | OpenStack and Qt projects | AUC 0.83 and 0.82; training takes 36 s and 175 s instead of 70–300 minutes for deep learning models (on CPU) |
| 7 | Giray et al., 2023 [7] | Review of deep learning for defect prediction | 102 studies | Most studies use supervised learning; two thirds use code metrics; CNN is the most used model |
| 8 | Kang et al., 2022 [8] | Re-checks machine learning detectors of false alarms | FindBugs warnings, checked by people | After removing data leakage and duplicates, F1 drops from 0.88 to 0.31, while a trivial baseline gets 0.52; only 47% of warnings labelled "actionable" were confirmed by people |
| 9 | Lenarduzzi et al., 2023 [9] | Compares six static analysis tools | 47 Java projects | Tools almost do not agree with each other; precision from 18% (SonarQube) to 86% (Checkstyle), 57% for FindBugs and 52% for PMD |
| 10 | Mahbub and Rahman, 2024 [10] | Bugsplorer: a transformer model predicts defective lines | 24 Python projects and a Java dataset (9 systems, 32 releases) | On Java data: balanced accuracy 0.901 against 0.538 for DeepLineDP |
| 11 | Silva et al., 2024 [11] | GitBug-Java: benchmark of recent Java bugs | 199 bugs from 2023 in 55 repositories | Bugs can be reproduced in prepared environments |
| 12 | Li et al., 2025 [12] | IRIS: an LLM helps CodeQL find vulnerabilities | 120 real vulnerabilities in Java projects | CodeQL alone found 27, IRIS with GPT-4 found 55 |
| 13 | Du et al., 2026 [13] | An LLM filters false positives of an industrial analyzer | 433 warnings from Tencent, mostly C/C++ | LLM and static analysis together remove 94–98% of false positives; costs $0.0011–0.12 per warning instead of 10–20 minutes of manual checking |
| 14 | SpotBugs documentation [14] | List of bug patterns | Categories such as Correctness, Bad practice, Performance | Shows what the main baseline can find |
| 15 | PMD documentation [15] | List of Java rules | 8 categories, including Error Prone | Shows what the second baseline can find |

### Table 2. Limitations stated by the authors and use in this project

| # | Source | Limitations stated by the authors | Use in this project |
| --- | --- | --- | --- |
| 1 | Johnson et al. [1] | Small sample, so results may not generalise; only developers who had used such tools; some participants had built such tools themselves, which may bias them; participants worked with unfamiliar code | Supports the problem; the report must explain each warning |
| 2 | Just et al. [2] | No limitations section. Future work: add more programs and bugs, classify the bugs. (A later paper [11] notes that most Defects4J bugs are 10–15 years old.) | Main dataset for training and testing |
| 3 | Habib and Pradel [3] | The studied bugs and tools may not represent others; project developers may have used such tools before, so some bugs were already removed; the matching method can miss found bugs or count random matches; the final decision was made by a person; no claim that results generalise | Shows the gap that machine learning can address; SpotBugs on Defects4J becomes the baseline |
| 4 | Ferenc et al. [4] | Original datasets were used "as is" without checking, although some have problems; for some systems the right source version was not found; old systems were analysed with the newest Java standard | Possible extra training data |
| 5 | Yang et al. [5] | Conclusions are limited to the studied data; other metrics may give other results; default model settings were used; should be repeated on other data. (A later study [8] found data leakage in this setup.) | Simple models are popular, but results must be checked for leakage |
| 6 | Pornprasit and Tantithamthavorn [6] | Only two datasets; the ground truth may miss bug-introducing commits that are not fixed yet; one train/test split, so no statistical tests; results depend on settings and randomness | A fast model with line-level explanations |
| 7 | Giray et al. [7] | Only studies until the end of 2021; grey literature and studies with only classic machine learning were excluded; some studies may be missed; possible bias of the researchers | Overview of methods and open problems |
| 8 | Kang et al. [8] | Only FindBugs and Java, so results may not apply to other tools; only one approach was analysed; human labels may have errors; choice of projects | Avoid data leakage and compare with simple baselines |
| 9 | Lenarduzzi et al. [9] | Default tool settings; only open-source Java projects; manual checking may have errors; recall was not measured | Evidence of the false positive problem; idea for the tool comparison (DIP-13) |
| 10 | Mahbub and Rahman [10] | May not work well for defects across several files; errors on code that depends on the environment or uses rare syntax; possible mistakes when re-implementing other methods | Showing lines, not only files, is useful |
| 11 | Silva et al. [11] | No limitations section. The environment could not be built for 7 bug fixes, and 100 could not be reproduced offline or had flaky tests | Second test set with recent bugs |
| 12 | Li et al. [12] | Many vulnerabilities are still not found; many LLM calls make it expensive; unknown if it works for other languages; a gap remains between the generated report and the report developers want | Combining static analysis with a learned model helps; possible future work |
| 13 | Du et al. [13] | Recall is below the 90% the company wants; hard cases with deep or cross-module context; mostly memory-safety bugs in C/C++ code of one company; LLM answers are random; the data cannot be shared | False positives are a real cost in industry |
| 14 | SpotBugs documentation [14] | — (documentation) | Choosing SpotBugs categories for the comparison |
| 15 | PMD documentation [15] | — (documentation) | Choosing PMD rules for the comparison |

## 3. Critical review

### 3.1 Rule-based tools are useful but miss a lot

Static bug detectors are widely used [3], but they have two problems. First, many warnings are not useful: precision of six tools on 47 Java projects was from 18% to 86%, and the tools almost did not agree with each other [9]. Developers named false positives and badly presented warnings as reasons not to use such tools [1]. Second, the tools miss most real bugs: Error Prone, Infer and SpotBugs together found only 27 of 594 real Java bugs [3]. Both studies have limits: the interview study had only 20 people [1], and the detector study does not claim that its results generalise [3].

### 3.2 Machine learning for defects

Some works train a model to separate useful warnings from false alarms. A simple SVM reached a median AUC of 99.5% on FindBugs warnings [5], but a later study found data leakage and duplicates in this setup. After fixing them, F1 fell from 0.88 to 0.31, which is worse than a trivial baseline (0.52) [8]. The authors advise comparing new methods with simple baselines [8].

Defect prediction models try to guess which files, methods or lines contain bugs. Most studies use supervised learning and code metrics [7]. JITLine shows that a random forest can be trained in minutes instead of hours and still give AUC 0.82–0.83, and that LIME can show risky lines [6]. Transformer models can find defective lines more accurately on Java data [10].

I start with classic models (random forest, gradient boosting) with explanations and use a neural network only for comparison. This is my own decision, based on the fast training and explanations in [6] and on the time I have.

### 3.3 Datasets

Defects4J is a widely used dataset of real Java bugs [11]; each bug has a buggy and a fixed version [2]. Static bug detectors were also tested on it [3], so SpotBugs can be compared on the same bugs. However, most Defects4J bugs are 10–15 years old [11]. GitBug-Java adds 199 newer bugs from 2023 [11]. The Unified Bug Dataset has class- and file-level metrics [4], but its authors did not check the original data [4].

### 3.4 LLMs with static analysis

New works combine static analysis with LLMs. IRIS found 55 of 120 Java vulnerabilities, while CodeQL alone found 27 [12]. In industry, LLMs combined with static analysis removed 94–98% of false positives of a static analyzer [13]. But the authors say that many vulnerabilities are still missed and LLM calls are expensive [12], and that the results come from C/C++ code of one company [13]. In this project, LLMs are a possible extension, not the main approach.

### 3.5 Gaps stated by the authors and how this project responds

| Gap stated in the source | Source | How this project responds |
| --- | --- | --- |
| Tools do not give enough information to decide what to do with a warning; the authors suggest better explanations | [1] | Each result has a location, type, score and explanation |
| Bug detectors miss most real bugs; future tools should go beyond generic bug patterns | [3] | A learned model is added to static analysis and tested on the same bugs as SpotBugs |
| New methods should be compared with simple baselines | [8] | The evaluation includes simple baselines, SpotBugs and PMD |
| Recall of the tools was not measured | [9] | The evaluation measures both precision and recall |
| Little evidence that defect prediction models are used in practice | [7] | The project builds a usable web tool and asks potential users |
| Most Defects4J bugs are old | [11] | GitBug-Java is used as a second test set |

## 4. References

[1] B. Johnson, Y. Song, E. Murphy-Hill and R. Bowdidge, "Why don't software developers use static analysis tools to find bugs?", in *Proc. 35th International Conference on Software Engineering (ICSE)*, 2013. Available: https://petertsehsun.github.io/soen7481/papers/icse13b.pdf

[2] R. Just, D. Jalali and M. D. Ernst, "Defects4J: A database of existing faults to enable controlled testing studies for Java programs", in *Proc. International Symposium on Software Testing and Analysis (ISSTA)*, 2014. Available: https://homes.cs.washington.edu/~mernst/pubs/bug-database-issta2014.pdf ; dataset: https://github.com/rjust/defects4j

[3] A. Habib and M. Pradel, "How many of all bugs do we find? A study of static bug detectors", in *Proc. 33rd ACM/IEEE International Conference on Automated Software Engineering (ASE)*, 2018, pp. 317–328. Available: https://software-lab.org/publications/ase2018_static_bug_detectors_study.pdf

[4] R. Ferenc, Z. Tóth, G. Ladányi, I. Siket and T. Gyimóthy, "A public unified bug dataset for Java and its assessment regarding metrics and bug prediction", *Software Quality Journal*, vol. 28, pp. 1447–1506, 2020. Open access: https://doi.org/10.1007/s11219-020-09515-0

[5] X. Yang, J. Chen, R. Yedida, Z. Yu and T. Menzies, "Learning to recognize actionable static code warnings (is intrinsically easy)", *Empirical Software Engineering*, 2021. https://doi.org/10.1007/s10664-021-09948-6 ; open preprint: https://arxiv.org/abs/2006.00444

[6] C. Pornprasit and C. Tantithamthavorn, "JITLine: A simpler, better, faster, finer-grained just-in-time defect prediction", in *Proc. 18th International Conference on Mining Software Repositories (MSR)*, 2021. Available: https://arxiv.org/abs/2103.07068

[7] G. Giray, K. E. Bennin, Ö. Köksal, Ö. Babur and B. Tekinerdogan, "On the use of deep learning in software defect prediction", *Journal of Systems and Software*, 2023. Open access: https://www.sciencedirect.com/science/article/pii/S0164121222002138 ; preprint: https://arxiv.org/abs/2210.02236

[8] H. J. Kang, K. L. Aw and D. Lo, "Detecting false alarms from automatic static analysis tools: How far are we?", in *Proc. 44th International Conference on Software Engineering (ICSE)*, 2022. Available: https://arxiv.org/abs/2202.05982

[9] V. Lenarduzzi, F. Pecorelli, N. Saarimäki, S. Lujan and F. Palomba, "A critical comparison on six static analysis tools: Detection, agreement, and precision", *Journal of Systems and Software*, 2023. Open access: https://www.sciencedirect.com/science/article/pii/S0164121222002515 ; repository copy: https://oulurepo.oulu.fi/handle/10024/45331

[10] P. Mahbub and M. M. Rahman, "Predicting line-level defects by capturing code contexts with hierarchical transformers", in *Proc. IEEE International Conference on Software Analysis, Evolution and Reengineering (SANER)*, 2024. Available: https://arxiv.org/abs/2312.11889

[11] A. Silva, N. Saavedra and M. Monperrus, "GitBug-Java: A reproducible benchmark of recent Java bugs", in *Proc. 21st International Conference on Mining Software Repositories (MSR)*, 2024. Available: https://arxiv.org/abs/2402.02961

[12] Z. Li, S. Dutta and M. Naik, "IRIS: LLM-assisted static analysis for detecting security vulnerabilities", in *Proc. International Conference on Learning Representations (ICLR)*, 2025. Available: https://arxiv.org/abs/2405.17238

[13] X. Du, J. Feng, Y. Zou, W. Xu, J. Ma, W. Zhang, S. Liu, X. Peng and Y. Lou, "Reducing false positives in static bug detection with LLMs: An empirical study in industry", in *Proc. 48th International Conference on Software Engineering (ICSE), Software Engineering in Practice track*, 2026. Available: https://arxiv.org/abs/2601.18844

[14] SpotBugs, "Bug descriptions", SpotBugs documentation. Available: https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html

[15] PMD, "Java rules", PMD Source Code Analyzer documentation. Available: https://docs.pmd-code.org/latest/pmd_rules_java.html
