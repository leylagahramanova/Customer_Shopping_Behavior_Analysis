# Customer Shopping Behavior Analysis

> Turning 3,900 purchase records into practical customer and merchandising insights.

This project combines Python, PostgreSQL, and Excel to explore customer spending patterns, product preferences, customer segments, and subscription behavior.

## At A Glance

| Dataset | Records | Fields | Missing values |
| --- | ---: | ---: | --- |
| Customer shopping behavior | 3,900 | 18 | 37 review ratings |

## Project Files

- [Source dataset](customer_shopping_behavior.csv)
- [Analysis notebook](customer_shopping_behavior_analysis.ipynb)
- [Dashboard preview](Screenshot%202026-06-17%20at%2013.18.40.png)

## Exploratory Data Analysis Using Python

The notebook uses pandas to inspect and prepare the source data:

1. Load the CSV and review its structure, descriptive statistics, and null values.
2. Fill missing `Review Rating` values with the median rating for the relevant product category.
3. Standardize column names to snake case and rename `purchase_amount_(usd)` to `purchase_amount`.
4. Create `age_group` from age quartiles.
5. Convert purchase-frequency labels into the numeric `purchase_frequency_days` field.
6. Compare `discount_applied` with `promo_code_used` and remove the redundant field.

## Data Analysis Using SQL (Business Transactions)

The cleaned DataFrame is loaded into PostgreSQL for structured business analysis. The notebook writes to the `customer` table in the `customer_behavior` database.

### Revenue And Customers

| Analysis | Result |
| --- | --- |
| Revenue by gender | Female: **$75,191**; Male: **$157,890** |
| Subscription revenue | Non-subscribers: **$170,436**; Subscribers: **$62,645** |
| Average spend by subscription | Non-subscribers: **$59.87**; Subscribers: **$59.49** |
| Customer segments | Loyal: **3,116**; Returning: **701**; New: **83** |
| Repeat buyers with more than five purchases | Non-subscribers: **2,518**; Subscribers: **958** |

### Products, Discounts, And Shipping

**Top-rated products**

| Product | Average rating |
| --- | ---: |
| Gloves | 3.86 |
| Sandals | 3.84 |
| Boots | 3.82 |
| Hat | 3.80 |
| Skirt | 3.78 |

**Highest discounted-purchase rates**

| Product | Discount rate |
| --- | ---: |
| Hat | 50.00% |
| Sneakers | 49.66% |
| Coat | 49.07% |
| Sweater | 48.17% |
| Pants | 47.37% |

Express orders had a higher average purchase amount than Standard orders: **$60.48** compared with **$58.46**.

### Top Products By Category

| Category | Top products by order volume |
| --- | --- |
| Accessories | Jewelry, Sunglasses, Belt |
| Clothing | Blouse, Pants, Shirt |
| Footwear | Sandals, Shoes, Sneakers |
| Outerwear | Jacket, Coat |

### Revenue By Age Group

| Age group | Total revenue |
| --- | ---: |
| Young Adult | $62,143 |
| Middle-aged | $59,197 |
| Adult | $55,978 |
| Senior | $55,763 |

## Excel Dashboard

The cleaned results were presented in an interactive Excel dashboard for visual exploration of customer and product performance.

![Customer shopping behavior dashboard](Screenshot%202026-06-17%20at%2013.18.40.png)

## Business Recommendations

- **Boost subscriptions:** Promote exclusive benefits and targeted conversion campaigns; average spend is currently similar for subscribers and non-subscribers.
- **Build loyalty:** Reward repeat buyers and encourage Returning customers to move into the Loyal segment.
- **Review discount policy:** Monitor margin impact for products with high discounted-purchase rates, especially Hats, Sneakers, and Coats.
- **Position proven products:** Feature highly rated and frequently purchased products in campaigns and merchandising.
- **Target high-value audiences:** Focus marketing on high-revenue age groups and customers who select Express shipping.

## Running The Notebook

Open [the analysis notebook](customer_shopping_behavior_analysis.ipynb) from the project directory and run the cells in order. The CSV must remain in the same directory as the notebook.

The database-loading cell expects a local PostgreSQL connection with:

```text
database: customer_behavior
host: localhost
port: 5432
user: postgres
```

Update the connection settings for your local environment before running the PostgreSQL step. The notebook uses `pandas`, `psycopg2`, and `sqlalchemy`.
