# indian-ipo-underpricing-analysis

# What drives underpricing in Indian IPOs?

An exploratory analysis of 509 Indian IPOs (January 2010 to August 2025) to find out which factors are linked to a high listing gain.

## Question
Are heavily subscribed IPOs more underpriced, and do market conditions (India VIX) make a difference?

## Dataset
[Indian IPO Underpricing 2010-2025 on Kaggle](https://www.kaggle.com/datasets/ishans474/indian-ipo-underpricing-2010-2025) - 509 rows, 19 columns covering issue size, subscription levels (QIB, HNI, RII, Total), market indicators and underpricing.

## Key findings
- **Subscription is the strongest signal.** Median underpricing is 0% for IPOs subscribed under 3 times, 4.3% for 3 to 31 times, and 31.2% for those subscribed over 31 times.
- **Market conditions matter, but less.** Median underpricing falls from 10.6% in low-VIX periods to 2.9% in high-VIX periods.
- **Issue size shows little link** to underpricing (correlation -0.10). The largest IPO, LIC, listed below its offer price.
- **Means mislead:** a few extreme listings push the average well above the median in many years, so medians are used.

## Limitations
- These are associations, not proof of cause.
- Some years have very few IPOs, and 2025 ends in August.
- Subscription and VIX are related, which makes their effects hard to separate.

## Tools
Python, pandas (groupby, qcut, correlation analysis), Jupyter Notebook

## Files
- [ipo_underpricing_analysis.ipynb](ipo_underpricing_analysis.ipynb) - the full analysis
- [IPO_Underpricing_Final.csv](IPO_Underpricing_Final.csv) - the dataset
