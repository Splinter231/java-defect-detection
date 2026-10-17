# Interview Questions

**Task:** DIP-52
**Format:** text chat
**Interviewees:** teachers of programming courses and Java developers (target: 3–5)

## Hypotheses

| ID | Hypothesis |
| --- | --- |
| H1 | Static analysis tools and IDE inspections produce many irrelevant warnings, so users ignore part of them. |
| H2 | Some bugs are not caught by existing checks (tools, code review, tests) and are found late. |
| H3 | Users would trust an ML-based tool only if it explains why the code is considered risky. |
| H4 | A web report with a list of likely defects (location, type, confidence) is useful for checking code. |

## Questions

| # | Question | Hypothesis |
| --- | --- | --- |
| 1 | What is your role, and how long have you worked with Java (in teaching or in development)? | Context |
| 2 | How do you check Java code for errors: your own code or students' projects? Which tools do you use (IDE inspections, SpotBugs, PMD, SonarQube, others), and what do you like or dislike about them? | H1 |
| 3 | Roughly what share of the warnings from these tools is actually useful? What happens with the rest? | H1 |
| 4 | Give an example of an error that was found too late (in production, in testing or at a project defense). What was it, and why was it not caught earlier? | H2 |
| 5 | Which types of errors are the most common or the most costly in the code you work with? | Requirements |
| 6 | Would you trust a tool that uses machine learning to point at risky code? What would make you trust or distrust it? | H3 |
| 7 | What should a report about a possible error contain so that you can quickly decide what to do with it? | H3, H4 |
| 8 | Where would such a report be most convenient for you: a web page, the IDE or the CI pipeline? Would you use such a tool, and for what? | H4 |

## Recording answers

Save each conversation as `docs/interviews/interview-NN.md`: date, role and experience, the answers (copied from the chat) and a short table marking each hypothesis as confirmed, not confirmed or unclear.

## Questions in Russian (sent in the chat)

1. Какая у вас роль и сколько лет вы работаете с Java (в преподавании или в разработке)?
2. Как вы проверяете Java-код на ошибки — свой или студенческие проекты? Какими инструментами пользуетесь (инспекции IDE, SpotBugs, PMD, SonarQube, другие) и что в них нравится или не нравится?
3. Примерно какая доля предупреждений от этих инструментов действительно полезна? Что происходит с остальными?
4. Приведите пример ошибки, которую нашли слишком поздно (в продакшене, на тестировании или на защите проекта). Что это была за ошибка и почему её не заметили раньше?
5. Какие ошибки в коде, с которым вы работаете, встречаются чаще всего или обходятся дороже всего?
6. Доверились бы вы инструменту, который с помощью машинного обучения показывает подозрительный код? Что повысило бы доверие, а что оттолкнуло бы?
7. Что должно быть в отчёте о возможной ошибке, чтобы вы могли быстро решить, что с ней делать?
8. Где такой отчёт был бы удобнее: на веб-странице, в IDE или в CI? Стали бы вы пользоваться таким инструментом и для чего?
