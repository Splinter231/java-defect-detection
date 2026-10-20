# Technology Comparison

**Task:** DIP-53

**Status:** Draft. The choices may change after the first experiments.

## 1. Method

I compared alternatives for four key technical decisions. The criteria come from the requirements (`docs/requirements.md`). Facts about each tool are taken from its official documentation or repository (checked on 18 October 2026).

The whole system is written in **Python**. It analyses Java code, but the tool itself does not have to be in Java. All libraries below are available for Python, and I am more confident with Python than with Java.

## 2. Parsing Java code

The system needs to read Java files and build a syntax tree (FR-02, FR-03). It must work with modern Java (NFR-08) and should not crash on files with errors (NFR-06).

| Alternative | Java versions | Files with syntax errors | Maintenance and license |
| --- | --- | --- | --- |
| javalang | "A lexer and parser targeting Java 8" [2] | Not documented | Last commit in October 2021; MIT [2] |
| tree-sitter with tree-sitter-java | The grammar has rules for records, sealed classes and switch expressions [3] | Designed to give "useful results even in the presence of syntax errors" [1] | Last commit in September 2025; MIT [3] |
| JavaParser | Java 1.0 to Java 25 [4] | Not compared | Java library; LGPL or Apache License [4] |

**Choice: tree-sitter with tree-sitter-java.** It works from Python, supports modern Java and still gives a partial result for a file with errors. javalang only supports Java 8 and is not updated. JavaParser is a Java library, so it would need a Java process next to the Python system.

## 3. Machine learning library

The model works with a table of code features. It must train without a GPU.

| Alternative | Models | Supported by SHAP's fast tree explainer | License |
| --- | --- | --- | --- |
| scikit-learn | Random forest, gradient boosting and many others | Yes [7] | BSD-3-Clause [5] |
| XGBoost | Gradient boosting | Yes [7] | Apache-2.0 [6] |
| LightGBM | Gradient boosting | Yes [7] | MIT [8] |

**Choice: scikit-learn**, because it has both random forest and gradient boosting in one library. XGBoost and LightGBM will be tried in the experiments, and the best model will be used. All three work with SHAP, so the explanation part does not change.

**Explanations:** I use **SHAP**, because it explains each single prediction (FR-07) and has a fast exact algorithm for tree models [7]. LIME [9] was also considered, but its repository has not been updated since 2021.

## 4. Web framework

The user uploads a project and reads the report in a browser. The analysis can take a few minutes, so it must run in the background (FR-12).

| Alternative | From the documentation | Background work | License |
| --- | --- | --- | --- |
| FastAPI | "A modern, fast (high-performance), web framework for building APIs with Python" [10] | Built-in background tasks; for heavy work the documentation suggests tools like Celery [10] | MIT [10] |
| Django | "A high-level Python web framework" with user authentication and admin "right out of the box" [11] | Not compared | Free and open source [11] |
| Flask | "A lightweight WSGI web application framework" [12] | Not compared | BSD-3-Clause [12] |

**Choice: FastAPI with Jinja2 templates** for the pages. It gives both an API and HTML pages [10], and its built-in background tasks are enough for one user. Django's user accounts and admin panel are not needed. Flask would also work, but FastAPI has background tasks in its documentation, which FR-12 needs.

## 5. Data storage

The system stores analysis jobs, report entries and user marks (FR-08, FR-11, FR-12). There is little data, and the system should start with one command (NFR-10).

| Alternative | From the documentation | Separate server needed |
| --- | --- | --- |
| SQLite | "A lightweight disk-based database that doesn't require a separate server process"; included in Python [13] | No |
| PostgreSQL | "A powerful, open source object-relational database system" [14] | Yes |

**Choice: SQLite.** It needs no server and is enough for one user. The Python documentation notes that an application can start with SQLite and later move to a bigger database such as PostgreSQL [13].

## 6. Summary

| Decision | Choice |
| --- | --- |
| Language | Python |
| Parsing Java code | tree-sitter with tree-sitter-java |
| Machine learning | scikit-learn (XGBoost and LightGBM in experiments) |
| Explanations | SHAP |
| Web framework | FastAPI with Jinja2 templates |
| Storage | SQLite |

## 7. References

[1] Tree-sitter, "Introduction". https://tree-sitter.github.io/tree-sitter/

[2] javalang, GitHub repository and PyPI page. https://github.com/c2nes/javalang ; https://pypi.org/project/javalang/

[3] tree-sitter-java, GitHub repository (including `grammar.js`) and PyPI page. https://github.com/tree-sitter/tree-sitter-java ; https://pypi.org/project/tree-sitter-java/

[4] JavaParser, GitHub repository. https://github.com/javaparser/javaparser

[5] scikit-learn, GitHub repository. https://github.com/scikit-learn/scikit-learn

[6] XGBoost, GitHub repository. https://github.com/dmlc/xgboost

[7] SHAP, GitHub repository. https://github.com/shap/shap

[8] LightGBM, GitHub repository. https://github.com/microsoft/LightGBM

[9] LIME, GitHub repository. https://github.com/marcotcr/lime

[10] FastAPI documentation: home page, "Background Tasks", "Templates". https://fastapi.tiangolo.com/ ; https://fastapi.tiangolo.com/tutorial/background-tasks/ ; https://fastapi.tiangolo.com/advanced/templates/

[11] Django, home page and overview. https://www.djangoproject.com/ ; https://www.djangoproject.com/start/overview/

[12] Flask documentation and GitHub repository. https://flask.palletsprojects.com/en/stable/ ; https://github.com/pallets/flask

[13] Python documentation, "sqlite3 — DB-API 2.0 interface for SQLite databases". https://docs.python.org/3/library/sqlite3.html

[14] PostgreSQL, "About". https://www.postgresql.org/about/
