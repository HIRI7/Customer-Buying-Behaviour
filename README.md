 Customer Shopping Behavior Analysis — End-to-End (Python, SQL, Power BI)

An end-to-end analytics project on a 3,900-row retail customer dataset, covering data cleaning and feature engineering in Python, business-question analysis in SQL, and an interactive dashboard in Power BI.

Overview
This project explores customer shopping behavior — spending patterns, discount usage, subscription status, and purchase frequency — to answer questions a retail/e-commerce business would realistically ask about its customer base.

Tools & Skills
1)Python (pandas) 
2) SQL (SQL Server, window functions, CTEs) 
3)Power BI (DAX, Power Query, data visualization)

Process

1. Data Cleaning & Feature Engineering (Python)
- Cleaned a 3,900-row, 18-column dataset; identified 37 missing values, all concentrated in 'Review Rating'
- Handled missing 'Review Rating' values using category-wise median imputation (more accurate than a flat overall median, since rating patterns differ by product category)
- Standardized column names (lowercase, snake_case) for consistency
- Engineered an 'age_group' feature (Young Adult / Adult / Middle-aged / Senior) using quartile-based binning
- Engineered a 'purchase_frequency_days' feature, converting categorical frequency labels (e.g. "Fortnightly", "Quarterly") into numeric day intervals for easier analysis
- Verified and removed a redundant column: 'Promo Code Used' was found to exactly mirror 'Discount Applied' across all 3,900 rows
- Exported the cleaned dataset directly into SQL Server via SQLAlchemy for the next stage

**2. Business Analysis (SQL)**
Wrote 10 queries to answer specific business questions. Sample results:
- **839 of 1,677 discount-using customers (50%)** still spent above the $59.76 dataset average — discounts aren't purely driving down basket size
- Express shipping customers spend more on average ($60.48) than Standard shipping customers ($58.46)
- Highest-rated products by average review score: Gloves (3.86), Sandals (3.84), Boots (3.82)
- Highest discount-reliance products: Hat (50% of purchases discounted), Sneakers (49.7%), Coat (49.1%)
- Customer segmentation (New ≤2 prior purchases, Returning 3–10, Loyal >10 purchases) found 3,116 of 3,900 customers (80%) already classify as Loyal — a high-repeat customer base
- Of customers with more than 5 previous purchases, 2,518 are non-subscribers vs. 958 subscribers — repeat buying doesn't strongly predict subscription
- Top 3 products per category identified using 'ROW_NUMBER() OVER (PARTITION BY category ORDER BY count DESC)'

See (sql/customer_behavior_queries.sql) for the full set of 10 queries.

3. Dashboard (Power BI)
Built an interactive Power BI dashboard visualizing the query results — revenue breakdowns, customer segments, discount impact, and category-level performance with filters for dynamic exploration.

 Key Insights
- Male customers generated more than double the revenue of female customers ($157,890 vs. $75,191) — likely reflects a larger male customer base in this dataset rather than higher per-customer spend
- Subscribers do not spend more per transaction than non-subscribers ($59.49 vs. $59.87 average) — and non-subscribers drive the majority of total revenue ($170,436 vs. $62,645) simply due to higher volume (2,847 vs. 1,053 customers), challenging the assumption that subscription status signals higher-value customers
- Revenue is fairly evenly distributed across age groups, with Young Adults contributing slightly more ($62,143) than Seniors ($55,763) — no single age group dominates the customer base
- 80% of customers (3,116 of 3,900) already qualify as "Loyal" (10+ previous purchases) — the dataset represents a highly retained customer base rather than one skewed toward first-time buyers
- Half of all discount-using customers still spent above the dataset average purchase amount — suggesting discounts are being used opportunistically by higher-spending customers, not just as an incentive for price-sensitive ones

Dashboard Preview
https://github.com/HIRI7/Customer-Buying-Behaviour/blob/89af7c0645030d29ffa8f8add5d0d4b85e12a16e/Customer%20buying%20behaviour%20dashboard.png

 Notes
This project followed a guided YouTube tutorial for the core end-to-end structure (Python → SQL → Power BI), extended with two additional dashboard visuals built independently.

 Files
- `python/Customer_shopping_behaviour.ipynb` — data cleaning & feature engineering
- `sql/customer_behavior_queries.sql` — business analysis queries
- `Practice_project_power_bi.pbix` — Power BI dashboard file
- `customer_shopping_behavior.csv` — source dataset

  Acknowledgement-
  Project layout and dataset inspired by Amlan Mohanty tutorials.
