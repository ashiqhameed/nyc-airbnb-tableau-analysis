# 🏙️ NYC Airbnb Data Analysis — Tableau Dashboard & Price Model

An exploratory data analysis and interactive dashboard built in Tableau, uncovering pricing, availability, and host patterns across ~48,895 Airbnb listings in New York City — plus a Python notebook that cleans the data and trains a model to predict nightly price.

🔗 **[View Interactive Dashboard on Tableau Public](https://public.tableau.com/views/NewYorkCityAirbnb_17768523314010/Dashboard1?:language=en-US&publish=yes&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link)**

![NYC Airbnb Dashboard](dashboard-screenshot.png)

## Overview

New York City hosts thousands of Airbnb listings across its five boroughs, making it a rich but complex dataset to analyze. This project explores pricing patterns, neighborhood preferences, availability trends, and host behavior through an interactive Tableau dashboard.

## Objectives

- Identify the distribution of listings across different neighborhoods and boroughs
- Analyze pricing trends based on room type, location, and availability
- Understand host activity and the concentration of listings per host
- Detect patterns in customer reviews and their correlation with pricing
- Provide actionable insights through an interactive dashboard

## Dataset

- **Source:** [Inside Airbnb](http://insideairbnb.com/) / Kaggle public dataset
- **Records:** ~48,895 Airbnb listings in New York City
- **Key attributes:** Listing ID, Name, Host ID, Neighbourhood Group, Neighbourhood, Room Type, Price, Minimum Nights, Number of Reviews, Availability, Last Review Date
- **Raw data:** included in this repo as `AB_NYC_2019.csv`

## Tools & Technologies

| Tool | Purpose |
|------|---------|
| Tableau Desktop / Public | Data visualization and dashboard creation |
| Microsoft Excel / CSV | Preliminary data review and cleaning |
| Python (pandas, scikit-learn, matplotlib) | Reproducible cleaning, EDA, and price model |
| Kaggle / Inside Airbnb | Source platform for dataset |

## Key Insights

- **Manhattan and Brooklyn** account for the majority of listings, reflecting their popularity among tourists and short-term visitors
- **Entire home/apartment** listings command significantly higher prices than private or shared rooms
- Listings with **higher review counts tend toward moderate pricing**, suggesting a sweet spot between affordability and quality
- **Availability varies greatly by neighborhood** — some hosts maintain year-round listings while others operate seasonally
- A **small number of hosts manage a disproportionately large share of listings**, indicating the presence of professional hosting businesses operating at scale

## Python Analysis & Price Prediction

📓 **[`analysis.ipynb`](analysis.ipynb)** — a reproducible companion to the dashboard:

- **Cleaning:** drops invalid \$0 prices, excludes the 0.5% of listings above \$1,000/night, caps unrealistic minimum stays, and treats missing review data as "never reviewed" rather than an error
- **EDA:** price distribution, borough × room-type medians, a price map, and host concentration
- **Model:** predicts log nightly price from location, room type, reviews, and availability, compared against a simple *borough × room-type median* baseline

| Model (held-out test set) | MAE | Median abs. error | R² (log price) |
|---|---|---|---|
| Baseline: borough × room-type median | \$54.10 | \$28.00 | 0.48 |
| Ridge regression | \$49.61 | \$25.17 | 0.58 |
| **Gradient boosting** | **\$45.50** | **\$22.87** | **0.65** |

Gradient boosting reduces average error by ~16% over the baseline. Room type and neighbourhood dominate; once the neighbourhood is known, the borough adds nothing. The notebook discusses why the gain is modest (the dataset lacks size and amenity data) and its limitations.

```bash
pip install -r requirements.txt
jupyter notebook analysis.ipynb
```

## Dashboard Features

The interactive dashboard lets users filter by borough, room type, price range, and availability, and includes:
- Total bookings by room type and neighborhood group
- Average price by neighborhood group and room type
- Top 10 hosts by total reviews
- Reviews-per-month trends and yearly review volume
- Geographic map of pricing by neighborhood

## Possible Extensions

- Sentiment analysis on guest reviews
- Time-series forecasting of pricing trends
- Geo-spatial clustering to identify high-demand micro-areas

## Author

Ashiq Hameed — B.Tech Artificial Intelligence & Data Science

