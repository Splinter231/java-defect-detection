# Interview 01

**Participant:** P1

**Date:** 20 October 2026

**Role and experience with Java:** university teacher who supervises diploma projects; earlier developed web services and maintained information systems. More than 10 years with Java.

**Format:** text chat in Russian. The participant agreed that the answers can be used without the name.

## Answers

The answers are copied from the chat without changes, except the name of the company, which is removed so that the participant cannot be identified. The summaries are mine.

**1. Role and experience**

> Я работала в [компания], где участвовала в разработке веб-сервисов и сопровождении информационных систем. Сейчас преподаю в Astana IT University и руковожу дипломными проектами. С Java работаю более 10 лет: 10 лет в разработке и более10 лет в преподавании.

Summary: former developer of web services and information systems, now a university teacher and diploma supervisor; more than 10 years with Java.

**2. How the code is checked, which tools are used**

> В [компания] код проверялся на код-ревью и статическим анализом. Использовали SonarQube в CI и инспекции IntelliJ IDEA. Студенческие проекты я сейчас проверяю в основном вручную и через инспекции IDE, иногда через SonarLint.
>
> Что нравится: IDE подсвечивает проблемы прямо в редакторе и предлагает quick fix, а SonarQube в CI не даёт пропустить совсем грубые ошибки. Хорошо ловятся возможный NullPointerException, незакрытые ресурсы, дублирование кода.
>
> Что не нравится: много шума и стилистических замечаний. Правила долго настраивать под конкретный проект. На старом коде при сопровождении предупреждений сотни, и разобрать их невозможно. Анализаторы почти не видят ошибок интеграции и бизнес-логики.

Summary: at work, code review, SonarQube in CI and IntelliJ IDEA inspections; student projects are checked mostly by hand and with IDE inspections, sometimes SonarLint. Good: highlighting in the editor, quick fixes, CI stops gross errors, possible NullPointerException and unclosed resources are found. Bad: a lot of noise and style remarks, rules take long to configure, hundreds of warnings on old code, integration and business logic errors are almost not found.

**3. Share of useful warnings**

> По моему опыту, реально полезны примерно 20–30%. Остальное — стиль, мелочи или ложные срабатывания. В рабочих проектах такие предупреждения часто помечали как «won’t fix» или просто откладывали, особенно в унаследованном коде. Студенты их обычно игнорируют. Из-за этого среди шума теряются и действительно важные предупреждения.

Summary: about 20–30% of warnings are useful. The rest are style, minor issues or false positives; they are marked "won't fix", postponed or ignored, and important warnings get lost in the noise.

**4. An error found too late**

> При сопровождении ИС был случай. Веб-сервис получал данные от смежной системы, и в одном из ответов необязательное поле пришло пустым. Сервис не проверял его на null и падал с ошибкой. Часть запросов не обрабатывалась, и обнаружилось это уже в продакшене по обращениям пользователей.
>
> Раньше не заметили по трём причинам: на тестовом стенде данные всегда были заполнены полностью; тесты не покрывали граничные случаи; предупреждение анализатора о возможном null терялось среди множества других.
>
> Похожее бывает и у студентов. Например, приложение на Spring Boot зависает на защите из-за незакрытых соединений с базой данных.

Summary: a missing null check on an optional field from another system crashed a web service, and it was found in production from user complaints. Reasons: complete test data, no tests for edge cases, and the analyzer's null warning was lost among many others. Students have similar problems, for example unclosed database connections.

**5. Most common or costly errors**

> Чаще всего встречаются:
>
> - NullPointerException и отсутствие проверки входных данных, особенно от внешних систем;
> - «проглоченные» исключения и плохое логирование, из-за которых при сопровождении трудно найти причину сбоя;
> - утечки ресурсов: соединения, потоки;
> - ошибки при работе с датами, часовыми поясами и кодировками;
> - некорректные equals/hashCode, сравнение через ==.
>
> Дороже всего обходятся:
>
> - ошибки на стыке систем (интеграции, форматы данных, таймауты) — они проявляются только в продакшене;
> - проблемы безопасности и обработки персональных данных: SQL-инъекции, секреты в коде;
> - логические ошибки в бизнес-логике, которые анализаторы не ловят.

Summary: most common are NullPointerException and missing input checks, swallowed exceptions, resource leaks, date, time zone and encoding errors, wrong equals/hashCode and comparison with ==. Most costly are integration errors, security problems and business logic errors.

**6. Trust in an ML tool**

> Доверилась бы как помощнику, а не как окончательному судье.
>
> Доверие повысили бы:
>
> - понятное объяснение, почему код подозрителен;
> - оценка уверенности модели;
> - мало ложных срабатываний;
> - возможность пометить «это не ошибка», чтобы инструмент это учитывал;
> - прозрачность того, на каких данных обучена модель;
> - работа локально или внутри контура организации. Для госсистем это обязательное условие: код нельзя отправлять на сторонние серверы.
>
> Оттолкнули бы:
>
> - «чёрный ящик» без объяснений;
> - много шума;
> - разные результаты на одном и том же коде;
> - обязательная загрузка кода в облако.

Summary: would trust it as a helper, not as the final judge. Trust grows with a clear explanation, model confidence, few false positives, a "not a bug" mark, known training data and local work. A black box, noise, different results on the same code and a required cloud upload would push her away.

**7. What a report should contain**

> - Файл, строка и фрагмент кода с подсветкой.
> - Тип проблемы и короткое описание простым языком.
> - Почему это ошибка и к чему она может привести, лучше с конкретным сценарием (например, «при пустом поле X из внешнего сервиса будет NPE»).
> - Серьёзность и уверенность модели.
> - Предлагаемое исправление.
> - Ссылка на правило или документацию.
> - Кнопки «исправить» и «ложное срабатывание».
> - Для сопровождения — пометка, новая это проблема или она уже была в коде раньше.

Summary: location with highlighted code, problem type in simple words, why it is an error with a concrete scenario, severity and confidence, a suggested fix, a link to a rule, "fix" and "false positive" buttons, and whether the problem is new or old.

**8. Where the report should be; would you use it**

> Для разработчика удобнее всего в IDE, в виде плагина для IntelliJ IDEA, чтобы видеть проблемы сразу при написании. Для команды и сопровождения нужна интеграция с CI: проверка на каждый merge request и отчёт только по новым изменениям, чтобы не тонуть в старых предупреждениях. Для преподавания удобен веб-отчёт со сводкой по всем студенческим проектам.
>
> Да, я бы пользовалась таким инструментом для трёх задач:
>
> - быстрой предварительной проверки дипломных и курсовых проектов;
> - поиска рискованных мест, на которые стоит обратить внимание на защите;
> - обучения: студенты сами видели бы свои ошибки с объяснениями до сдачи.
>
> Из опыта в [компания] могу сказать, что при сопровождении такой инструмент тоже был бы полезен, особенно для поиска ошибок обработки данных от внешних систем.

Summary: for developers an IntelliJ IDEA plugin, for teams a CI check on new changes, for teaching a web report with a summary of all student projects. Would use it to pre-check diploma and course projects, to find risky places before a defense and for teaching.

## Hypotheses

| Hypothesis | Result | Evidence |
| --- | --- | --- |
| H1. Many useless warnings | Confirmed | Only 20–30% of warnings are useful; the rest are ignored or postponed (Q3) |
| H2. Bugs found late | Confirmed | A null check error was found in production (Q4) |
| H3. Trust needs explanations | Confirmed | A clear explanation and confidence increase trust; a "black box" would push her away (Q6) |
| H4. A web report is useful | Partly confirmed | Useful for teaching; for developers and teams an IDE plugin and CI are preferred (Q8) |

**Ideas for requirements:**

- Show the model's confidence and a severity level for each result.
- Explain the risk with a concrete scenario and, if possible, suggest a fix.
- Let the user mark "not a bug" (already FR-11).
- Give the same result on the same code (already FR-04) and work locally without a cloud (already NFR-05).
- Show whether a problem is new or was already in the previous version.
- For teachers: a summary report over several student projects.
- IDE plugin and CI integration are out of scope now (requirements, Section 5); they are possible future work.
