# Evidence of Relevance

**Task:** DIP-52

**Status:** Draft. One interview is done (P1). The plan was 3–5 interviews; the supervisor agreed that one interview is enough for pre-defense 1. More interviews can be added later.

## 1. Method

I check the four hypotheses from `docs/interviews/questions.md` with two kinds of evidence:

- the literature review (`docs/literature-review.md`, references [n]);
- interviews with teachers and Java developers, done as text chats (notes in `docs/interviews/`).

Because there is only one interview, a hypothesis is **supported** if the interview and the literature both support it, **partly supported** if only one of them supports it or the answer is mixed, and **not supported** if both disagree.

## 2. Evidence by hypothesis

| Hypothesis | Literature | Interviews | Status |
| --- | --- | --- | --- |
| H1. Tools give many useless warnings, so users ignore part of them | Precision of six tools was 18–86% [9]; false positives stop developers from using the tools [1] | P1: only about 20–30% of warnings are useful; the rest are postponed or ignored | Supported |
| H2. Some bugs are not caught and are found late | Three bug detectors found only 27 of 594 real bugs [3] | P1: a missing null check was found in production; the analyzer's warning was lost among others | Supported |
| H3. Users trust an ML tool only if it explains its results | Almost all interviewed developers had problems understanding tool results [1]; trust in ML tools was not studied in the reviewed papers | P1: would trust it as a helper if it explains the result and shows confidence; a "black box" would push her away | Partly supported (the literature does not study trust in ML tools) |
| H4. A web report with likely defects (location, type, score) is useful | Badly presented results are a problem for developers [1] | P1: a web report is useful for teaching; developers and teams would prefer an IDE plugin or CI | Partly supported |

## 3. Verified findings and assumptions

**Verified** (supported by the literature and the interview):

- Rule-based tools give many warnings that are not useful, so users ignore part of them (H1: [9], [1], P1).
- Real bugs are missed or found late; a useful warning can be lost among many others (H2: [3], P1).
- Users need to understand why a result is shown (H3: [1], P1).

**Assumptions** (not yet supported):

- Users will trust an ML tool more if it shows an explanation and a confidence score. Only P1 says this; the reviewed papers do not study it.
- A web report is a good format for developers. P1 sees it as useful for teaching, but for developers she prefers an IDE plugin or CI (H4).
- An ML model gives fewer useless warnings than rule-based tools. This will be checked in the experiment (`docs/evaluation-plan.md`).

## 4. Effect on the requirements

Requirements from the interview are added to `docs/requirements.md`, Section 6, with the source **I**: severity level (FR-15), a concrete risk scenario and a suggested fix (FR-16), new or old problem (FR-17) and a summary over several projects (FR-18). The interview also supports FR-07 (explanation), FR-11 ("not a bug" mark), FR-04 (same result on the same code) and NFR-05 (no cloud). An IDE plugin and CI integration stay out of scope (Section 5 of the requirements).

## 5. Limitations

- Only one interview, so the results cannot be generalised; they are combined with the literature. The interview is preliminary evidence; 1–2 interviews with practising Java developers are planned for November 2026.
- The participant is a teacher who worked as a developer before, not a current industry developer.
- Text chats give shorter answers than live interviews.
