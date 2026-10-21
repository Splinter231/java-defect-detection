# Project Plan, Milestones and Risks

**Task:** DIP-56

**Status:** Draft. Dates after 24 October are my plan and will be agreed with the supervisor. University dates (next pre-defenses and the defense) will be added when they are announced.

## 1. How the work is organised

- **YouTrack** (project DIP): every piece of work is a task with an expected outcome, acceptance criteria and a deadline. The work is split into 9 stages; each stage is a parent task.
- **Board stages:** Очередь (queue) → Разработка (in progress) → Ревью (review) → Тест (testing) → На тестовом окружении (test environment) → Готово (done).
- **Git:** one branch per task (`DIP-N-short-name`), commit messages start with the task key (`DIP-N: ...`), changes go to `main` through a pull request linked in the task.

## 2. Responsibilities

| Role | Person | Responsibilities |
| --- | --- | --- |
| Student | Sergey Chepurnenko (SE-2422) | All project work: analysis, design, code, experiments, tests, documentation and thesis |
| Supervisor | Aigerim Bakiyeva | Confirms the scope, reviews key results, gives feedback |
| Interview participants | Teachers and Java developers | Answer interview questions, try the prototype |

## 3. Stages

| Stage | YouTrack | Result | Planned dates |
| --- | --- | --- | --- |
| 1. Domain analysis | DIP-2 | Proposal, literature review, tool comparison, requirements, interviews | 15–18 Oct 2026 |
| 2. System design | DIP-3 | Architecture, diagrams, technology comparison, prototype, evaluation plan | 18–20 Oct 2026 |
| Pre-defense 1 | DIP-50 | Project plan, supervisor feedback, tag `pre-defense-1` | 21–24 Oct 2026 |
| 3. Training data | DIP-4 | Labelled dataset of Java methods | 26 Oct – 29 Nov 2026 |
| 4. Static analysis module | DIP-5 | Parser, metrics, rule checks, unit tests | 2 Nov – 13 Dec 2026 |
| 5. ML model | DIP-6 | Trained and compared models, explanations | 30 Nov 2026 – 31 Jan 2027 |
| 6. Backend and web interface | DIP-7 | API, database, report, web pages | 4 Jan – 28 Feb 2027 |
| 7. Testing and evaluation | DIP-8 | Tests, comparison with SpotBugs and PMD | 1 Feb – 21 Mar 2027 |
| 8. Thesis writing | DIP-9 | Thesis chapters | Nov 2026 – Apr 2027 |
| 9. Defense preparation | DIP-10 | Presentation, demo video, final pre-defense | Apr 2027 – defense |

## 4. Milestones

| Milestone | Done when | Date |
| --- | --- | --- |
| Pre-defense 1 | All `pre-defense-1` tasks are closed and the tag is created | 24 Oct 2026 |
| Dataset ready | Defective and clean methods are labelled | 29 Nov 2026 |
| First model results | First models are compared with the simple baselines | 10 Jan 2027 |
| Working system | A user can upload a project and see a report in the browser | 28 Feb 2027 |
| Evaluation done | Comparison with SpotBugs and PMD is finished | 21 Mar 2027 |
| Thesis draft | The full draft is sent to the supervisor | Apr 2027 |
| Final pre-defense and defense | — | Set by the university |

## 5. Dependencies

- The **parser** (DIP-22) is needed first, because it is used to find which methods a bug fix changed. So stages 3 and 4 run in parallel.
- **Features** (DIP-26) need the dataset (DIP-21) and the metrics (DIP-23).
- **Model training and evaluation** (DIP-27 to DIP-29) need the features.
- **Explanations and the report** (DIP-30, DIP-34) need the trained model.
- The **web interface** (DIP-33) needs the API (DIP-31); it can start with a placeholder model.
- **Comparison with SpotBugs and PMD** (DIP-38) and **Chapter 4** of the thesis (DIP-44) need the evaluated model.

The longest chain is: parser → dataset → features → model → evaluation → thesis chapter 4. Delays here move the final pre-defense, so these tasks go first.

## 6. Risks

| Risk | Probability | Impact | What I will do |
| --- | --- | --- | --- |
| Too few or wrong labels in the dataset | Medium | High | Use Defects4J, where fixes are cleaned; check the dataset size early (by 29 Nov) |
| The model is not better than the simple baselines or the tools | Medium | High | Compare with baselines from the first experiment; try other features and models; report the results honestly |
| SpotBugs cannot analyse the old Defects4J projects | Medium | Medium | Check at the start of stage 3; use an older SpotBugs version if needed |
| Not enough time because of other courses and exams | High | Medium | About one week of buffer per stage; drop Could requirements first |
| Fewer than 3 interviews | Medium | Medium | Ask more teachers and the supervisor for contacts; ask Java developers online |
| Weak Java knowledge slows down work with Java tools | Medium | Medium | The system is written in Python; Java tools are run through scripts |
| Laptop failure or lost work | Low | High | Push to GitHub often; datasets can be downloaded again |
