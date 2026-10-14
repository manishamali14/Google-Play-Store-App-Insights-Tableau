# Google Play Store App Insights — Tableau Analysis

An end-to-end analysis of 10,000+ Google Play Store apps and 64,000 user reviews, built in Tableau,
to find out what drives app ratings, installs and user sentiment.

## Business problem

A mobile app company wants to understand:

1. What factors contribute to an app's success on the Google Play Store?
2. How can the company use these factors to improve its own apps?
3. What do user preferences and behaviour look like?

The analysis answers 25 questions (10 basic, 10 medium, 5 advanced) covering ratings, categories,
genres, pricing, app size, update patterns and review sentiment.

## Dataset

- **Source:** [Google Play Store Apps on Kaggle](https://www.kaggle.com/datasets/lava18/google-play-store-apps)
- `googleplaystore.csv`: 10,841 rows, 13 columns (app, category, rating, reviews, size, installs, type, price, content rating, genres, last updated, current version, Android version)
- `googleplaystore_user_reviews.csv`: 64,295 rows (app, translated review, sentiment, polarity, subjectivity)

## Tools

- **Power Query (Excel):** data cleaning and type conversion
- **Tableau Public:** calculated fields, analysis and dashboards

## Data cleaning

| Step | What was done |
|---|---|
| Encoding | Read the CSVs as UTF-8, fixing 542 app names with corrupted characters |
| Duplicates | Removed 483 exact duplicate app rows (10,357 rows remain) and 7,735 exact duplicate review rows |
| Malformed rows | Removed 1 row with shifted columns |
| Missing values | Converted "NaN" and "nan" text to true blanks; removed 26,863 empty review rows; left 1,465 missing ratings blank (not imputed); filled 1 missing Type as "Free" based on its price of 0 |
| Data types | Installs ("10,000+") and Price ("$4.99") converted to numbers; Last Updated converted to dates; Size converted to MB |
| Text | Trimmed whitespace, standardised category names, kept upper and lower case distinct |

Missing ratings were deliberately not imputed. The unrated apps have almost no users (a median of 1 review),
so filling them with an average would invent good ratings for apps nobody rated.

## Dashboards

| Dashboard | Covers |
|---|---|
| 1. Overview | Average rating, free vs paid, content ratings, app sizes, top installed apps, installs vs rating |
| 2. Pricing & Content | Price vs rating for paid apps, content ratings for free vs paid apps |
| 3. Category & Genre | Top categories by installs, top genres among popular apps, genre ratings |
| 4. Reviews & Ratings | Most reviewed and highest rated apps, review sentiment and complaint themes |
| 5. Trends Over Time | Update trends and seasonality, update frequency, size vs installs, rating by install bin |

Each dashboard has an interactive filter (category, or free vs paid) for exploring the results.

## Key findings

- **Ratings are generally high:** the average rating is 4.19, and 78% of rated apps score 4.0 or above.
- **Free apps dominate:** 92.6% of apps are free. Paid apps receive far fewer reviews (11,901 on average, against 437,328 for free apps).
- **Popularity and rating are only weakly linked:** the correlation between installs and rating is 0.05. Ratings dip to about 4.0 for apps with 1K–50K installs and rise to 4.41 for apps with 100M+ installs.
- **Games lead installs:** Game (31.5B), Communication (24.2B) and Social (12.5B) are the most installed categories.
- **Some genres rate consistently higher:** Events (4.44), Word (4.40) and Puzzle (4.39) rate highest; Educational (3.87) and Dating (3.97) rate lowest.
- **Higher prices go with slightly lower ratings:** paid apps up to $1 average 4.30, while apps over $50 average 3.91.
- **Larger apps get more installs:** median installs rise from 10,000 for apps under 10 MB to 1,000,000 for apps of 50–100 MB.
- **Updates happen on weekdays:** about 1,700–1,900 updates per weekday against 634 on Sunday, rising towards the end of each year.
- **Stability drives bad reviews:** high-rated apps receive 70.6% positive reviews, against 53.2% for low-rated apps. Among negative reviews, bugs and crashes are the top complaint for low-rated apps (29.9%), while price and payments lead for high-rated apps (29.9%).

## Recommendations

1. **Prioritise stability:** bugs, crashes and problematic updates are what most separate low-rated apps from high-rated ones.
2. **Price carefully:** keep paid apps low-cost, or use a free model, since ratings and reviews fall as price rises.
3. **Target strong categories:** games, communication and productivity reach the largest audiences, while creative and educational genres earn the best ratings.
4. **Release updates mid-week and plan for year-end:** this matches common practice across the store.

## Limitations

- **Repeated apps:** only exact duplicate rows were removed. 523 apps still appear on more than one row, so totals follow the row-level method in the project brief.
- **Installs are ranges:** "1,000,000+" is the lower bound of a bucket, not an exact count.
- **Update history is thin:** only 42 apps have more than one update date, so update-frequency results rest on a small sample.
- **Partial review coverage:** reviews cover about 1,000 apps, and complaint themes were identified by keywords.

## Repository contents

| File | Description |
|---|---|
| `Google Play Store App Insights.twbx` | Tableau packaged workbook (includes the data) |
| `Googleplaystore.xlsx` | Cleaned app data, with the Power Query cleaning steps |
| `Googleplaystorereview.xlsx` | Cleaned review data, with the Power Query cleaning steps |

## Author

Manisha Mali
