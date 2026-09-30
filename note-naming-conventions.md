# Naming Conventions 🏷️ ![Style](https://img.shields.io/badge/Clean_Naming-Future_You_Says_Thanks-2ea44f?style=for-the-badge)

> Bad file names are technical debt with a friendly face. `final_v2_REAL_final.xlsx` has ended more careers than any bug.

Pick a convention, stick to it, and your repo reads like a well-organized library instead of a junk drawer.

## 🔤 The Case Types You'll Meet

| Case | Looks like | Typical home |
|:-----|:-----------|:-------------|
| `snake_case` | `sales_summary_2026` | Python, SQL, datasets |
| `kebab-case` | `sales-summary-2026` | HTML, CSS, R, repo folders |
| `PascalCase` | `SalesSummary` | Java classes |
| `camelCase` | `salesSummary` | Variables in JS and Java |
| `Title Case` | `Sales Summary 2026` | Human-facing documents |

## 📁 File-Type Cheat Sheet

| File type | Convention | Example |
|:----------|:-----------|:--------|
| Microsoft Word | `Title Case.docx` or `Title_Case.docx` | `Quarterly Report.docx` |
| Microsoft Excel | `Title Case.xlsx` or `Title_Case.xlsx` | `Sales Tracker.xlsx` |
| Dataset (CSV) | `snake_case.csv` | `customer_orders.csv` |
| Tableau Workbook | `Title_Case.twbx` or `kebab-case.twbx` | `Sales_Dashboard.twbx` |
| PDF | `Title Case.pdf` or `Title_Case.pdf` | `Project_Report.pdf` |
| [Jupyter Notebook](https://docs.jupyter.org/en/latest/contributing/ipython-dev-guide/coding_style.html) | `snake_case.ipynb` | `exploratory_data_analysis.ipynb` |
| [Python](https://www.python.org/dev/peps/pep-0008/#package-and-module-names) | `snake_case.py` | `clean_data.py` |
| SQL script | `snake_case.sql` | `monthly_revenue.sql` |
| [Java](https://www.oracle.com/java/technologies/javase/codeconventions-namingconventions.html) | `PascalCase.java` | `OrderService.java` |
| [R](http://web.stanford.edu/class/cs109l/unrestricted/resources/google-style.html) | `kebab-case.R` | `sales-model.R` |
| [HTML](https://developers.google.com/style/filenames#naming-guidelines) | `kebab-case.html` or `snake_case.html` | `index.html`, `about-me.html` |
| [CSS](https://ecss.benfrain.com/chapter5.html) | `kebab-case.css` | `main-styles.css` |
| [JavaScript](https://google.github.io/styleguide/jsguide.html#file-name) | `snake_case.js` | `chart_helpers.js` |

## 🧠 My Rules of Thumb

1. **Be consistent before being clever.** One convention per file type, everywhere.
2. **No spaces in code and data files.** Spaces break scripts and command lines. Use `_` or `-`.
3. **Say what it is, not how you feel.** `customer_churn_analysis.ipynb` beats `stuff2.ipynb`.
4. **Dates go year-first.** `2026-09-30` sorts correctly on its own; `30-09-2026` does not.
5. **Use version numbers, not the word "final".** `report_v3` is honest. `report_final_FINAL` is a cry for help.
6. **Keep it lowercase where possible.** Case-sensitive systems (Linux, some servers) will punish you otherwise.
7. **Short but readable.** If you need to squint, rename it.

## ✅ Before & After

| ❌ Messy | ✅ Clean |
|:---------|:---------|
| `Untitled1.ipynb` | `netflix_eda.ipynb` |
| `Sales Data (1) final.csv` | `sales_data_2026.csv` |
| `MyDashboard NEW.twbx` | `Sales_Dashboard_v2.twbx` |
| `query.sql` | `top_customers_by_revenue.sql` |
