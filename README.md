# Flipkart Product Catalog Analysis

An end-to-end data analysis project on a ~20,000-product Flipkart e-commerce dataset — covering data cleaning, exploratory data analysis, and an interactive Power BI dashboard to answer real business questions around pricing, discounting, ratings, and seller trust signals.


## Project Overview

This project analyzes a real-world Flipkart product listings dataset (sourced from Kaggle) to uncover pricing strategy, discounting behavior, customer rating patterns, and the effect of the "FK Advantage" program on product listings. The goal was to go beyond basic exploratory charts and answer questions a business stakeholder would actually care about — then present those findings in a clean, single-page interactive dashboard.

## Dataset

- **Source:** [Flipkart Products Dataset – Kaggle](https://www.kaggle.com/) 
- **Size:** ~20,000 rows, 15 original columns
- **Fields:** product name, category tree, price, discounted price, brand, rating, description, and more

## Tools Used

- **Python** (pandas, matplotlib, seaborn) — data cleaning and exploratory analysis
- **Jupyter Notebook** — analysis workflow
- **Power BI** — interactive dashboard

## Data Cleaning

Key cleaning steps performed (full detail in the notebook):
- Removed rows with missing price data (~78 rows)
- Converted `product_rating` / `overall_rating` from mixed text/numeric to proper numeric fields, handling the "No rating available" string
- Parsed the nested `product_category_tree` string into a clean `main_category` field using regex, with a fallback bucket for products lacking a category hierarchy
- Handled ~29% missing `brand` values, filled as "Unknown" with a documented limitation (some non-brand values like sizes/colors were found in the source data)
- Removed duplicate product listings (same product re-crawled at different timestamps)
- Engineered a `discount_pct` feature and validated it against logical bounds

## Key Insights

1. **Product concentration** — Clothing and Jewellery together make up nearly 50% of the ~19,920-product catalog, with a long tail of 30+ smaller categories.
2. **Pricing varies sharply by category** — Jewellery, Furniture, and Automotive carry the highest average prices; Home Improvement and Baby Care are the most budget-oriented.
3. **Discounting is deliberate, not organic** — discount percentages spike sharply at 0% and ~50%, suggesting many sellers price around round, marketing-friendly numbers rather than organic demand-based discounting. Automotive and Mobiles & Accessories are discounted most aggressively (~50-55%); Beauty and Personal Care is discounted the least (~15%).
4. **Ratings are sparse and polarized** — only 9.2% of products carry any customer rating. Among rated products, ratings follow a J-shaped distribution (concentrated at 5★ and, to a lesser extent, 1★), consistent with well-documented reviewer bias.
5. **Rating is independent of price and discount** — correlation between rating and both price (r≈0.05) and discount % (r≈-0.002) is negligible. Expensive products aren't rated better; heavily discounted products aren't rated worse.
6. **"FK Advantage" functions as a trust signal, not a pricing tier** — Advantage-labeled products are priced similarly to regular listings but discounted ~13 percentage points less on average (28% vs 41%), and lack the extreme high-price outliers seen elsewhere in the catalog.
7. **Brand quality is inconsistent** — among brands with sufficient rating volume, top performers (JDX, Bosch: ~4.95★) far outpace others; some named brands (e.g., Clovia: 3.25★) actually underperform the "Unknown"/unbranded average (3.77★).

## Dashboard

The Power BI dashboard consolidates these findings into a single interactive page:
- KPI summary (total products, avg. price, avg. discount, % rated, avg. rating)
- Category-level breakdowns for product count, price, and discount (filtered to top categories by volume to avoid small-sample distortion)
- Rating distribution chart
- FK Advantage comparison
- Interactive category and brand filters

## Limitations

- ~90% of products have no customer rating, so rating-based insights are drawn from a smaller, potentially non-representative subset of the catalog
- ~29% of products have no listed brand; some brand entries in the source data contained non-brand values (sizes/colors)
- Dataset reflects a single crawl period (late 2015 / mid-2016) and does not capture longer-term pricing or rating trends
