# Indian IPO Underpricing Analysis (pandas + SQL)

An exploratory analysis of 509 Indian IPOs (January 2010 to August 2025) to find out which factors are linked to a high listing gain. The same dataset is analysed twice: in Python (pandas) and in MySQL.

## Question
Are heavily subscribed IPOs more underpriced, and do market conditions (India VIX) make a difference?

## Dataset
[Indian IPO Underpricing 2010-2025 on Kaggle](https://www.kaggle.com/datasets/ishans474/indian-ipo-underpricing-2010-2025) - 509 rows, 19 columns covering issue size, subscription levels (QIB, HNI, RII, Total), market indicators and underpricing.

## Part 1: pandas analysis
Notebook: [ipo_underpricing_analysis.ipynb](ipo_underpricing_analysis.ipynb)

Key findings:
- **Subscription is the strongest signal.** Median underpricing is 0% for IPOs subscribed under 3 times, 4.3% for 3 to 30 times, and 31.2% for those subscribed over 30 times.
- **Market conditions matter, but less.** Median underpricing falls from 10.6% in low-VIX periods to 2.9% in high-VIX periods.
- **Issue size shows little link** to underpricing (correlation -0.10). The largest IPO, LIC, listed below its offer price.
- **Means mislead:** a few extreme listings push the average well above the median in many years, so medians are used.

## Part 2: SQL analysis (MySQL)
Notebook: [ipo_sql_analysis.ipynb](ipo_sql_analysis.ipynb), run against a local MySQL database from Python (SQLAlchemy).

Techniques practised: GROUP BY / HAVING, CASE WHEN, CTEs, subqueries, window functions (RANK, LAG, FIRST_VALUE, NTILE, moving averages with frame clauses).

Key result: splitting IPOs into four subscription quartiles with NTILE(4), average underpricing rises steadily from -0.91% (least subscribed) to 2.43%, 13.84% and 48.84% (most subscribed), which agrees with the pandas result.

### How to reproduce the SQL part
1. Create a MySQL database named `ipo_db`.
2. Import [ipo_clean.csv](ipo_clean.csv) into a table named `ipos` (set the `underpricing` column to DOUBLE).
3. Open the notebook, run the first cells, and enter your MySQL password when prompted.

## Limitations
- These are associations, not proof of cause.
- Some years have very few IPOs, and 2025 ends in August.
- Subscription and VIX are related, which makes their effects hard to separate.

## Tools
Python, pandas, Jupyter Notebook, MySQL, SQLAlchemy

## Files
- [ipo_underpricing_analysis.ipynb](ipo_underpricing_analysis.ipynb) - pandas analysis
- [ipo_sql_analysis.ipynb](ipo_sql_analysis.ipynb) - SQL analysis
- [IPO_Underpricing_Final.csv](IPO_Underpricing_Final.csv) - original dataset
- [ipo_clean.csv](ipo_clean.csv) - cleaned file used for the MySQL table

- ## Part 3: Power BI dashboard
 <img width="722" height="414" alt="dashboard_overview png" src="https://github.com/user-attachments/assets/09997d06-fd48-43e5-bfa3-28805085203a" />
<img width="719" height="416" alt="dashboard_details png" src="https://github.com/user-attachments/assets/36fd4d64-22c1-42f4-84f3-5a355c8f93c0" />


Median underpricing by subscription tier (cutoffs: under 3x, 3x to 30x, over 30x): 0.0%, 4.5% and 30.6%. The pandas and SQL parts use tercile cutoffs (2.98x and 30.63x), which give slightly different medians (0%, 4.3% and 31.2%). The pattern is the same either way: heavily subscribed IPOs are underpriced far more.

File: [ipo_report_powerbi.pbix](ipo_report_powerbi.pbix) (open with Power BI Desktop)
