# Evidence of Relevance

**Task:** DIP-52

**Status:** Draft. 1 interview of at least 3 is done (P1); the status of each hypothesis will be set after at least three interviews.

## 1. Method

I check the four hypotheses from `docs/interviews/questions.md` with two kinds of evidence:

- the literature review (`docs/literature-review.md`, references [n]);
- interviews with teachers and Java developers, done as text chats (notes in `docs/interviews/`).

A hypothesis is **confirmed** if most participants support it and the literature agrees, **partly confirmed** if the answers are mixed, and **not confirmed** if most participants disagree.

## 2. Evidence by hypothesis

| Hypothesis | Literature | Interviews | Status |
| --- | --- | --- | --- |
| H1. Tools give many useless warnings, so users ignore part of them | Precision of six tools was 18–86% [9]; false positives stop developers from using the tools [1] | P1: only about 20–30% of warnings are useful; the rest are postponed or ignored | Pending |
| H2. Some bugs are not caught and are found late | Three bug detectors found only 27 of 594 real bugs [3] | P1: a missing null check was found in production; the analyzer's warning was lost among others | Pending |
| H3. Users trust an ML tool only if it explains its results | Almost all interviewed developers had problems understanding tool results [1]; trust in ML tools was not studied in the reviewed papers | P1: would trust it as a helper if it explains the result and shows confidence; a "black box" would push her away | Pending |
| H4. A web report with likely defects (location, type, score) is useful | Badly presented results are a problem for developers [1] | P1: a web report is useful for teaching; developers and teams would prefer an IDE plugin or CI | Pending |

## 3. Verified findings and assumptions

**Verified** (supported by the literature and the interviews): to be added after the interviews.

**Assumptions** (not yet supported): to be added after the interviews.

## 4. Effect on the requirements

New requirements from the interviews will be added to `docs/requirements.md` (Section 6) with the source **I**.

## 5. Limitations

- Only 3–5 interviews, so the results cannot be generalised.
- Most participants are teachers, not industry developers.
- Text chats give shorter answers than live interviews.
