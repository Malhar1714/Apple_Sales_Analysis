# Apple_Sales_Analysis
# Apple Products Data Analysis

This is a data analysis project on iPhone listings from Flipkart. I wanted to see how Apple products are priced, how much discount they get, and how customers rate and review them. I used Python (pandas, Matplotlib and Seaborn) and did everything in a Jupyter Notebook.

## Why I made this

I wanted to practice the full flow of a small data project: loading raw data, cleaning it, and then exploring it with charts. The dataset is small, so it's easy to follow and a good one to learn from.

## Key questions this project answers

1. How are iPhone prices spread out, and how big is the gap between MRP and sale price?
2. How much discount do buyers usually get?
3. Do customers rate Apple products highly, and is there any difference between products?
4. Do products with more ratings also get more reviews?
5. Which products are the most popular (most rated and most reviewed)?

## About the dataset

The data is in an Excel file called `apple_products.xlsx`. It has **62 rows** (one per product listing) and **11 columns**.

| Column | What it means |
|---|---|
| Product Name | Full name of the listing, with model, color and storage |
| Product URL | Link to the product page on Flipkart |
| Brand | Brand name (Apple) |
| Sale Price | The price the product is actually sold at |
| Mrp | The original maximum retail price |
| Discount Percentage | How much discount is given on the MRP |
| Number Of Ratings | How many people rated the product |
| Number Of Reviews | How many people wrote a review |
| Upc | Product code |
| Star Rating | Average star rating (4.5, 4.6 or 4.7 in this data) |
| Ram | RAM of the phone |

The data was already quite clean. There were no missing values and no duplicate rows.

**Good to know:** each row is a *listing*, not a unique phone model. The same iPhone can appear several times with different colors or storage sizes, so a "product" in the charts below really means a listing.

## Steps I followed

### 1. Loading and checking the data
- Read the Excel file with pandas
- Looked at the first rows, the shape, the data types and the column names
- Checked for missing values and duplicates

**Why:** Before any analysis you need to know what you are working with. Checking shape, data types and missing values early prevents wrong results later (for example, a price stored as text cannot be averaged).

### 2. Cleaning the data
- Removed extra spaces from the column names
- Removed extra spaces from all the text columns
- Checked if any product had an MRP higher than its sale price
- Checked the unique star ratings
- Saved the cleaned data as `apple_cleaned_data.csv`

**Why:** Hidden spaces make `"Apple "` and `"Apple"` look like two different values, which breaks grouping and counting. The MRP check is a sanity test: a sale price above the MRP would mean a data error, since the discount would be negative. Checking the unique star ratings showed the ratings only take three values (4.5, 4.6, 4.7), which matters when reading the rating chart.

### 3. Exploring the data
I loaded the cleaned CSV and made these charts. For each one, here is what it shows and how to read it.

#### 1. Top 10 products (most frequent names)
- **What it shows:** Which product names appear most often in the dataset.
- **How to read it:** A tall bar means that model is listed many times, usually because it comes in many colors and storage options.
- **Insight:** Frequency here reflects how many *variants* exist, not how many units were sold. Models with the most variants are the ones Apple sells in the widest range of options. _[Add the top model names from your chart.]_

#### 2. Sale price distribution
- **What it shows:** How the selling prices are spread out (histogram).
- **How to read it:** Look for where the tallest bars are (the most common price range) and whether the chart is skewed to one side.
- **Insight:** iPhone prices are usually spread across clear tiers because older and base models cost much less than Pro models, so expect more than one cluster instead of a single bell shape. _[Add the most common price range and the lowest and highest prices from your data.]_

#### 3. MRP vs Sale Price
- **What it shows:** A scatter plot comparing the original price with the actual selling price.
- **How to read it:** Points close to a diagonal line mean the sale price follows the MRP closely. The further a point sits *below* the line, the bigger the discount.
- **Insight:** The two prices move together almost in a straight line, which is expected: a higher-priced phone has a higher MRP. Because no product had an MRP lower than its sale price, every point sits on or below the diagonal, so discounts are never negative. _[Mention if any points are clearly far below the line.]_

#### 4. Discount percentage distribution
- **What it shows:** How much discount products get on their MRP.
- **How to read it:** The tallest bar is the most common discount level.
- **Insight:** Discounts on Apple products tend to be modest compared with other phone brands because Apple controls its pricing tightly. Most listings fall in a narrow discount band rather than being spread widely. _[Add the most common discount range and the maximum discount.]_

#### 5. Star rating distribution
- **What it shows:** How many products got each star rating.
- **How to read it:** There are only three bars (4.5, 4.6, 4.7) because that is the full range in the data.
- **Insight:** Every product is rated very high, so star rating alone **cannot separate good products from great ones** here. The difference between 4.5 and 4.7 is small, so number of ratings and reviews is a better signal of popularity than stars. _[Add which of the three ratings is the most common.]_

#### 6. Ratings vs Reviews
- **What it shows:** Number of ratings against number of reviews for each product.
- **How to read it:** An upward trend means products with more ratings also have more reviews.
- **Insight:** A positive, strong relationship is expected, because a review usually comes together with a rating, so reviews are always a smaller group than ratings. Points far from the trend are products where people rate often but rarely write reviews (or the other way round). _[Add the approximate share of ratings that also left a review.]_

#### 7. Top 10 products by number of ratings
- **What it shows:** The most rated listings.
- **How to read it:** More ratings usually means more buyers, so this is a rough proxy for popularity.
- **Insight:** A small number of listings tend to hold a large share of all ratings, which shows that demand is concentrated on a few popular models. _[Add the top product and its rating count.]_

#### 8. Top 10 products by number of reviews
- **What it shows:** The most reviewed listings.
- **How to read it:** Compare it with chart 7. If the same products appear in both, popularity is consistent.
- **Insight:** The lists are likely to overlap heavily because reviews follow ratings (see chart 6). Any product that is high in one list but missing from the other is worth a closer look. _[Note any differences between the two lists.]_

#### 9. Correlation heatmap
- **What it shows:** The correlation between all the numeric columns. Values go from -1 to +1.
- **How to read it:** Close to +1 means the two columns rise together, close to 0 means no relationship, close to -1 means one rises while the other falls.
- **Insight:**
  - **Sale Price and Mrp** should be very close to +1, since one is derived from the other.
  - **Number Of Ratings and Number Of Reviews** should also be strongly positive.
  - **Star Rating** has only three possible values, so its correlations are usually weak and should be read with care.
  - Remember that correlation does not mean one thing causes the other.

## Summary of findings

- **Pricing:** Sale price follows MRP closely, and no listing is sold above its MRP.
- **Discounts:** Discounts exist but stay within a fairly narrow range.
- **Ratings:** All products are rated 4.5 to 4.7, so customers are very satisfied across the board and stars do not help to rank products.
- **Popularity:** Number of ratings and reviews rise together, and a few listings account for most of the engagement.
- **Data quality:** The dataset had no missing values or duplicates, so no rows had to be removed.

> Fill in the exact numbers (average price, most common discount, top product, etc.) from your notebook output so these findings are backed by real values.

## Limitations

- Only 62 listings, so patterns may not hold for the whole market.
- Multiple listings of the same model (different colors/storage) can make some models look more popular than they are.
- Star ratings have almost no spread (4.5 to 4.7), so they give little information.
- Prices and discounts are a snapshot from when the data was collected.

## Project files

```
apple.ipynb              the main notebook with all the code and charts
apple_products.xlsx      the original dataset
apple_cleaned_data.csv   the cleaned dataset (created by the notebook)
README.md                this file
```

## Tools used

- Python 3
- pandas and NumPy for data handling
- Matplotlib and Seaborn for charts
- openpyxl for reading the Excel file
- Jupyter Notebook

## How to run it

1. Download or clone this project.
2. Install the libraries:
   ```
   pip install numpy pandas matplotlib seaborn openpyxl jupyter
   ```
3. Make sure `apple_products.xlsx` is in the same folder as the notebook.
4. Start Jupyter:
   ```
   jupyter notebook
   ```
5. Open `apple.ipynb` and run all the cells from top to bottom.

The first part of the notebook creates `apple_cleaned_data.csv`, and the second part reads it for the charts, so run the cells in order.

## Notes

- The dataset is small (only 62 products), so the results show a trend for this data and may not match the whole market.
- The prices are from the time the data was collected, so they may be different now.
