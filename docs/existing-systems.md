# Comparison of Existing Systems

**Task:** DIP-13

**Status:** Draft

## 1. Systems and criteria

I compared five tools that find defects in Java code. All information comes from official documentation or published studies (checked on 18 October 2026).

| System | Why it was chosen |
| --- | --- |
| SpotBugs | Bug-pattern detector for Java; the main tool to compare with |
| PMD | Rule-based source code analyzer; the second tool to compare with |
| SonarQube Community Build | Free code-quality platform with a web interface |
| Infer | Static analyzer for bugs such as null dereferences and resource leaks |
| Snyk Code | Commercial tool that says it uses an AI-based engine |

Error Prone and CodeQL were not included. Error Prone looks for the same kind of common mistakes as SpotBugs [10], and CodeQL is focused on security vulnerabilities [11], which are out of scope.

| # | Criterion | Why it matters |
| --- | --- | --- |
| C1 | Detection approach | Fixed rules, program analysis or machine learning |
| C2 | What is analysed | Source code or compiled code |
| C3 | Main focus | Bugs, code style or security |
| C4 | Languages | Whether the tool is made for Java |
| C5 | Explanation of results | Developers say that unclear results stop them from using such tools [14] |
| C6 | How results are shown | Command line, IDE, build tool or web interface |
| C7 | License and cost | Whether students and small teams can use it for free |
| C8 | Independent evidence | Precision or recall measured by researchers, not by the vendor |

## 2. Comparison

### Table 1. How the tools work (C1–C4)

| System | C1. Approach | C2. What is analysed | C3. Main focus | C4. Languages |
| --- | --- | --- | --- | --- |
| SpotBugs | Bug patterns [1] | Compiled bytecode, so the code must be built first [1] | Bugs: correctness, bad practice, multithreading, performance and others [3] | Java [1] |
| PMD | Rules on the syntax tree; 400+ rules [4] | Source code [4] | Programming flaws, including style [5] | Java, Apex and 16 more [4] |
| SonarQube Community Build | Coding rules [7] | Source code [6] | Maintainability, reliability and security [7] | 40+, including Java [6] |
| Infer | Program analysis run through the build [8] | Code built by the build command [8] | Bugs: null dereferences, resource leaks, race conditions [8] | Java, C, C++, Objective-C [8] |
| Snyk Code | "AI-based engine" (vendor's claim) [9] | Source code sent to the vendor [9] | Security vulnerabilities [9] | Many, including Java [9] |

### Table 2. What the user gets (C5–C8)

| System | C5. Explanation | C6. How results are shown | C7. License and cost | C8. Independent evidence |
| --- | --- | --- | --- | --- |
| SpotBugs | Pattern description, confidence and rank [1, 3] | Command line, GUI, IDE and build plugins [1] | Open source, LGPL-2.1 [2] | Found 18 of the 27 bugs that three tools found out of 594 [12]; FindBugs precision 57% [13] |
| PMD | Rule description, priority, examples [5] | Command line, build plugins, IDE, CI [4] | Open source, BSD-style [4] | Precision 52% [13] |
| SonarQube Community Build | Rule description, code locations and execution flow [7] | Web interface of own server [6] | Free; paid editions exist [6] | Precision 18% [13] |
| Infer | Short message with the reason and line [8] | Command line [8] | Open source, MIT [8] | Found 3 bugs that the other tools missed [12] |
| Snyk Code | Data flow, fix examples, priority [9] | Web interface, IDE, command line [9] | Commercial [9] | Not found in the reviewed studies |

## 3. Findings

1. **Free tools use rules.** SpotBugs, PMD, SonarQube Community Build and Infer find problems with patterns, rules or program analysis (C1). Only the commercial Snyk Code says it uses AI, and it is focused on security (C1, C3).
2. **Bug-focused tools find few real bugs.** SpotBugs, Error Prone and Infer together found only 27 of 594 real Java bugs [12] (C8).
3. **Many warnings are wrong.** For the compared tools, precision was from 18% to 57% [13] (C8).
4. **Few tools have a web report.** Only SonarQube and Snyk Code show results in a web interface. SonarQube needs its own server, and Snyk Code sends the code to the vendor (C2, C6).

## 4. Where the proposed system fits

| Criterion | Proposed system (planned) |
| --- | --- |
| C1 | Static analysis features plus a machine learning model trained on real Java bugs |
| C2 | Java source code; the user uploads a project |
| C3 | Bugs only, not style and not security |
| C4 | Java |
| C5 | Location, defect type, score and an explanation of the main reasons |
| C6 | Web interface |
| C7 | Free, runs on the user's computer |
| C8 | Compared with SpotBugs and PMD on the same bugs (`docs/evaluation-plan.md`) |

**Limitations of this comparison:** I did not run the tools myself yet; this is part of the evaluation plan. The independent evidence comes from two studies with their own limits (see the literature review). For Snyk Code, the claim about fewer false positives is only the vendor's claim.

## 5. References

[1] SpotBugs, "Introduction", "Filter file" and table of contents, SpotBugs 4.10.5 documentation. https://spotbugs.readthedocs.io/en/stable/introduction.html ; https://spotbugs.readthedocs.io/en/stable/filter.html ; https://spotbugs.readthedocs.io/en/stable/

[2] SpotBugs GitHub repository (README and license). https://github.com/spotbugs/spotbugs

[3] SpotBugs, "Bug descriptions". https://spotbugs.readthedocs.io/en/stable/bugDescriptions.html

[4] PMD, home page, "Tools / Integrations" and GitHub repository (license). https://pmd.github.io/ ; https://docs.pmd-code.org/latest/pmd_userdocs_tools.html ; https://github.com/pmd/pmd

[5] PMD, "Java Rules" and "Error Prone" rule category. https://docs.pmd-code.org/latest/pmd_rules_java.html ; https://docs.pmd-code.org/latest/pmd_rules_java_errorprone.html

[6] SonarSource, SonarQube Community Build documentation (home page, supported languages) and "Why upgrade from Community Build?". https://docs.sonarsource.com/sonarqube-community-build/ ; https://docs.sonarsource.com/sonarqube-community-build/analyzing-source-code/languages/overview ; https://www.sonarsource.com/products/sonarqube/why-upgrade/community-build/

[7] SonarSource, "SonarQube rules" and "Managing issues: Introduction", SonarQube Community Build documentation. https://docs.sonarsource.com/sonarqube-community-build/quality-standards-administration/managing-rules/rules ; https://docs.sonarsource.com/sonarqube-community-build/user-guide/issues/introduction

[8] Infer, home page, "Hello, World!" and GitHub repository (license). https://fbinfer.com/ ; https://fbinfer.com/docs/hello-world ; https://github.com/facebook/infer

[9] Snyk, "Snyk Code", "Supported languages, package managers, and frameworks" and plans page. https://docs.snyk.io/scan-with-snyk/snyk-code ; https://docs.snyk.io/supported-languages-package-managers-and-frameworks ; https://snyk.io/plans/

[10] Error Prone, home page. https://errorprone.info/

[11] GitHub, CodeQL home page. https://codeql.github.com/

[12] A. Habib and M. Pradel, "How many of all bugs do we find? A study of static bug detectors", in *Proc. 33rd ACM/IEEE International Conference on Automated Software Engineering (ASE)*, 2018, pp. 317–328. https://software-lab.org/publications/ase2018_static_bug_detectors_study.pdf

[13] V. Lenarduzzi, F. Pecorelli, N. Saarimäki, S. Lujan and F. Palomba, "A critical comparison on six static analysis tools: Detection, agreement, and precision", *Journal of Systems and Software*, 2023. https://oulurepo.oulu.fi/handle/10024/45331

[14] B. Johnson, Y. Song, E. Murphy-Hill and R. Bowdidge, "Why don't software developers use static analysis tools to find bugs?", in *Proc. 35th International Conference on Software Engineering (ICSE)*, 2013. https://petertsehsun.github.io/soen7481/papers/icse13b.pdf
