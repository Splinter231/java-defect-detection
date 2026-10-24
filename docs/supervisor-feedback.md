# Supervisor's Feedback

**Task:** DIP-57

This file records the comments of the supervisor (Bakiyeva A. M., PhD) and what I decided for each comment.

## 22 October 2026 (messages)

| # | Comment | Decision |
| --- | --- | --- |
| 1 | The repository can be public, so that the supervisor and the committee can open it without an invitation | Done: the repository is public (DIP-18) |
| 2 | One interview is acceptable for pre-defense 1 | Accepted: the evidence of relevance uses interview P1 and the literature (`docs/relevance.md`) |

## 24 October 2026 (supervisor's review of the pre-defense 1 report)

The supervisor wrote the review in the report file (full text below). Her overall assessment: the project has a strong research foundation and a clear practical goal; the main area for improvement is the precision of the research and implementation plan.

I received the review on the day of the submission. I fixed the points that change the plan itself (defect categories, role of machine learning, labelling, data split, how a correct detection is counted, primary user) and planned the other points for the next stages.

| # | Recommendation | Decision | Where |
| --- | --- | --- | --- |
| R1 | Define the defect categories of the first version and how each is identified | Done: null dereference and resource not closed, found by rule checks | `docs/proposal.md`, Section 4; FR-05 |
| R2 | Explain how methods are labelled as defective or not | Done: changed lines are mapped to methods; other methods are "not known to be defective"; unclear bugs are left out | `docs/evaluation-plan.md`, Section 2 |
| R3 | Separate training, validation and test data; avoid leakage | Done: split by project, one bug in one set, validation only on training projects | `docs/evaluation-plan.md`, Section 3 |
| R4 | Choose one role for machine learning | Done: the model predicts defective methods; SpotBugs and PMD are only baselines | `docs/proposal.md`, Section 4 |
| R5 | Define measurable success criteria | Partly done: false positives added to the metrics; target values will be set and justified after the first experiment with simple baselines (DIP-29) | `docs/evaluation-plan.md`, Section 5 |
| R6 | Make the explanation mechanism concrete | Planned: explanation design in stage 5 (DIP-30), after the features are fixed (DIP-26) | — |
| R7 | Define a minimum viable product | Planned: MVP in the project plan at the start of stage 3 (DIP-56). Partly done: the first version has two categories | — |
| R8 | Present the interview as preliminary evidence; interview practising developers | Done in the text; 1–2 interviews with practising developers planned for November 2026 | `docs/relevance.md`, Section 5 |
| R9 | Position the web application as the first version and choose the primary user | Done: primary user is Java developers; an IDE plugin or CI check can use the same API later | `docs/proposal.md`, Sections 5 and 11 |
| R10 | Define the ground truth and when a detection is correct | Done: the unit is the method; a reported method is correct if the fix changed it; unchanged methods are "not known to be defective" | `docs/evaluation-plan.md`, Sections 2 and 4 |

### Full text of the review

Copied from the supervisor's file without changes.

> The topic of our diploma thesis, "Development of an intelligent system for detecting defects in Java source code based on static analysis and machine learning methods," was proposed independently by the student, Sergey Chepurnenko, based on his own interests and skills. It is clear that, drawing upon the available data and findings, we will be testing—and potentially even synthesizing—static analysis techniques combined with machine learning methods. The theoretical analysis was conducted to an excellent standard; there is also a possibility that, as the project progresses, we may incorporate additional hybrid methods.The project addresses a relevant software engineering problem: existing static analysis tools can produce many false-positive warnings while still missing real defects. The proposal is well structured, supported by scientific literature, and demonstrates a good understanding of the limitations of rule-based analysis and the potential of machine learning.
>
> **Strengths**
>
> The problem statement is supported by specific research findings rather than general assumptions. The project scope is clearly defined, including the decision to focus on Java defects rather than code smells or style issues. The literature review critically discusses previous studies, including data leakage and the limitations of existing defect prediction approaches.
>
> The interview provides practical requirements for the proposed system, such as explaining warnings, showing confidence scores, and supporting local code analysis.
>
> The planned comparison with SpotBugs and PMD provides a reasonable basis for evaluating the proposed solution.
>
> **Recommendations for improvement**
>
> 1. Define the defect categories more precisely. The proposal mentions null pointer dereferences, resource leaks, incorrect comparisons, and exception-handling errors. Specify exactly which defect categories the first version will support and how each category will be identified. A limited, clearly defined set of defect types would make implementation and evaluation more manageable.
>
> 2. Explain the dataset labelling process. The proposal plans to use Defects4J and GitBug-Java, but it does not yet fully explain how individual methods will be labelled as defective or non-defective. Describe how buggy and fixed versions will be compared, how changed lines will be mapped to methods, and how ambiguous or partially fixed cases will be handled.
>
> 3. Strengthen the experimental design. Explain how the training, validation, and test sets will be separated. Avoid placing different versions of the same bug or closely related code samples in different sets. Consider evaluating the model on separate projects or using a chronological split to assess its ability to generalise to previously unseen code.
>
> 4. Clarify the role of machine learning in the system. Specify whether the model will predict defects in methods independently, prioritise warnings produced by static analysis tools, or combine both approaches. These are different tasks and require different labels and evaluation methods. The proposal should select one primary approach and explain how it complements SpotBugs and PMD.
>
> 5. Define measurable success criteria. Establish target metrics before conducting the experiments. For example, compare the proposed system with SpotBugs and PMD in terms of precision, recall, F1-score, and analysis time. Also measure the number of false-positive warnings and compare performance against a simple baseline. Any target values should be justified and treated as evaluation goals rather than guaranteed results.
>
> 6. Make the explanation mechanism more concrete. The proposal mentions SHAP and explanations for individual predictions. Specify which model features will be explained, how the explanation will be presented in the report, and how users will distinguish model confidence from defect severity. If SHAP is used, clarify what its feature contributions mean and what they cannot establish about the actual cause of a defect.
>
> 7. Prioritise the implementation scope. The project includes Java parsing, feature extraction, dataset preparation, several ML models, a web application, report generation, and comparative evaluation. For an individual project, define a minimum viable product: one or two defect categories, one baseline model, a working analysis pipeline, and a reproducible evaluation. Additional models and interface features can be implemented after the core system works.
>
> 8. Address the limitations of the interview evidence. The current relevance study is based on one participant, who has substantial Java experience but currently works primarily in teaching. Present the interview as preliminary evidence rather than proof of industry-wide needs. If possible, interview additional practising developers and use their responses to validate the requirements concerning web reports, local processing, and warning prioritisation.
>
> 9. Resolve the uncertainty about the target interface. The interview indicates that developers would prefer an IDE plugin or CI integration, while a web report is particularly useful for teaching. Since these integrations are outside the current scope, explicitly position the web application as the first version and identify the primary target user. This will help keep the requirements consistent with the actual user needs.
>
> 10. Improve the evaluation of real defects. Explain how the ground truth will be established for the test set and how a detection will be counted as correct. For example, define whether a prediction must overlap a known defective line, identify the affected method, or match a specific defect category. Report the limitations of the available datasets and avoid treating every unchanged line in a buggy version as definitively defect-free.
>
> **Overall assessment**
>
> The proposal has a strong research foundation and a clearly motivated practical objective. Its main area for improvement is not the general project idea, but the precision of the research and implementation plan. The most important next steps are to define the initial defect categories, document the dataset labelling procedure, specify the machine learning task, and establish a leakage-resistant evaluation protocol. Addressing these points will make the project more technically rigorous and help ensure that the final results demonstrate a measurable contribution beyond existing static analysis tools.
