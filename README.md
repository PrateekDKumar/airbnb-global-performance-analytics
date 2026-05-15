# airbnb-global-performance-analytics

> End-to-end data analytics pipeline on 279K+ Airbnb listings across 10 global cities, delivering pricing, market share, and guest experience insights via an interactive Power BI dashboard.

---

## Overview

This project presents a comprehensive data analytics solution built on real-world Airbnb listing and review data spanning 10 major cities worldwide. The pipeline covers the full analytics lifecycle - from raw CSV ingestion and preprocessing in Python/SQL, through KPI modeling in Power BI (DAX), to an executive-grade interactive dashboard. The resulting dashboard enables stakeholders to explore market concentration, pricing dynamics, superhost distribution, property type trends, and multi-dimensional guest ratings - all in one place.

---

## Problem Statement

The short-term rental market has grown dramatically since Airbnb's founding in 2008, but the landscape is far from uniform across geographies. City administrators, investors, and platform strategists lack a unified view of:

- Which cities dominate listings volume and how concentrated the market is
- How pricing varies across room types and geographies
- Whether Superhost status meaningfully differentiates listings
- How guest satisfaction scores compare across cities and rating dimensions
- What growth and decline patterns exist over time (including COVID-19 impact)

This project addresses these questions through a structured analytical pipeline and interactive dashboard.

---

## Dataset

Dataset Link - https://mavenanalytics.io/data-playground/airbnb-listings-reviews

| File | Description | Records |
|---|---|---|
| `Listings.csv` | Core listing metadata - host info, location, property type, room type, pricing, ratings | 279,712 rows × 33 columns |
| `Reviews.csv` | Per-listing review log with reviewer ID and review date | 5,373,143 rows |
| `Listings_data_dictionary.csv` | Column definitions for Listings dataset | - |
| `Reviews_data_dictionary.csv` | Column definitions for Reviews dataset | - |

**Key columns used:**
- `city`, `neighbourhood`, `district` - geography
- `host_is_superhost`, `host_since`, `host_total_listings_count` - host attributes
- `room_type`, `property_type`, `price`, `accommodates`, `bedrooms` - listing attributes
- `review_scores_rating`, `review_scores_accuracy`, `review_scores_checkin`, `review_scores_communication`, `review_scores_location`, `review_scores_value` - guest ratings
- `instant_bookable`, `minimum_nights`, `maximum_nights` - booking policies

**Coverage:** 10 cities - Paris, New York, Sydney, Rome, Rio de Janeiro, Istanbul, Mexico City, Bangkok, Cape Town, Hong Kong  
**Time span:** 2008-2021

---

## Tools & Technologies

| Layer | Tool / Library |
|---|---|
| Data Modeling & KPIs | Power BI Desktop, DAX |
| Visualization | Power BI (bar charts, line charts, heatmaps, KPI cards) |
| Version Control | Git / GitHub |

---

## Methods

1. **Power BI Modeling**
   - Built a star-schema data model linking Listings and Reviews on `listing_id`
   - Authored DAX measures for: total listings, active hosts, Superhost %, avg price by room type, cumulative market share %, avg rating dimensions per city
   - Implemented toggle slicer for Overall Rating vs Detailed Rating drill-down

2. **Dashboard Design**
   - Page 1: KPI overview (totals for listings, cities, hosts, property types, reviews) + New Listings lifecycle area chart
   - Page 2: Market Share Pareto chart, Average Price by room type, Ratings heatmap table, city-level drill-down

---

## Key Insights

### 1. Market Concentration - Paris Dominates
Paris alone accounts for **23.1%** of all global listings (64,690). The top 3 cities - Paris, New York, Sydney - together represent **48.4%** of the entire dataset, revealing strong geographic concentration. Hong Kong sits at the tail with just **2.5%** share (7,087 listings).

### 2. Pricing Paradox - Hotel Rooms Outprice Entire Places
Average nightly prices by room type:
- Hotel room: **$800** (highest)
- Entire place: **$673**
- Shared room: **$580**
- Private room: **$462** (most affordable)

Counterintuitively, hotel rooms command a premium over entire apartments, suggesting Airbnb's hotel inventory skews boutique/luxury. Shared rooms being pricier than private rooms may reflect premium co-living or hostel-style properties in high-demand cities.

### 3. Platform Lifecycle - COVID-19 Sharply Cut New Listings
New listing additions peaked around **2014-2016** (Maturity phase), declined through **2017-2018** (Decline), rebounded slightly during **2019** (Reinvention), then collapsed in **2020-2021** due to COVID-19 travel restrictions. Entire place listings drove most of the growth and suffered the steepest fall.

### 4. Superhost Distribution is Uneven
Overall Superhost penetration is **18%** of hosts, but city-level rates vary significantly:
- Mexico City: **31.9%** - highest Superhost density
- Cape Town: **24.1%**
- Rome: **25.8%**
- Paris: **12.5%** - surprisingly low despite being the largest market
- Istanbul: **13.2%**

Higher Superhost density in smaller markets suggests more curated hosting cultures vs. high-volume, transactional markets in Paris and New York.

### 5. Mexico City Leads Guest Satisfaction
Mexico City ranks #1 across all rating dimensions - Accuracy (9.7), Check-in (9.8), Communication (9.8), Location (9.8), and Value (9.6). Rio de Janeiro follows closely. Hong Kong consistently scores lowest across all dimensions (overall rating: 89.7 vs the dataset mean of 93.4), suggesting quality or expectation-setting challenges in that market.

### 6. Room Type Mix - Entire Place is Dominant
Of 279,712 listings:
- Entire place: **65%** (182,005)
- Private room: **31%** (86,988)
- Hotel room: **2.1%** (5,857)
- Shared room: **1.7%** (4,862)

Guests overwhelmingly prefer privacy. The shared room segment is shrinking relative to platform growth.

### 7. Instant Bookability - Still a Minority Feature
Only **41.3%** of listings have instant booking enabled, meaning the majority of hosts still require manual approval - a potential friction point for last-minute travelers.

### 8. Review Volume Mirrors Listing Growth
Reviews grew from just 2 in 2008 to a peak of **1.63 million in 2019**, before dropping to 755K in 2020 (COVID impact) and 82K in 2021 (dataset truncation). The acceleration between 2015-2019 aligns with the platform's global marketing push and mobile growth era.

---

## Dashboard

The Power BI dashboard consists of two interactive pages:

**Page 1: Portfolio Overview**
- KPI cards: Total Listings (2,79,712), Cities (10), Hosts (1,82,024), Property Types (144), Reviews (5,373K)
- New Listings over time : area chart by room type with lifecycle phase annotations (Introduction → Growth → Maturity → Decline → Reinvention → COVID-19)

**Page 2: Performance & Ratings**
- Market Share by City : Pareto combo chart (bars = listing count, line = cumulative %)
- Average Price by Room Type : horizontal bar chart
- Ratings Heatmap : city × rating dimension table with conditional color formatting
- Toggle slicer : switch between Overall Rating and Detailed Rating views

## Results and Conclusion

The analysis reveals that the global Airbnb market is highly concentrated in a few key cities, with Paris serving as the dominant market. Pricing does not follow intuitive room-size logic - hotel rooms outprice entire apartments, highlighting the platform's luxury segment. Guest satisfaction is broadly high (mean rating: 93.4/100) but varies meaningfully by city, with Mexico City leading and Hong Kong lagging across all dimensions. The Superhost program is unevenly adopted, suggesting an opportunity for platform-level incentivization in low-penetration markets. The COVID-19 impact is clearly visible - both in new listing volumes and review counts - confirming the platform's sensitivity to global travel restrictions.

This project demonstrates that combining SQL/Python preprocessing with Power BI's DAX modeling enables rich, multi-dimensional analysis of large-scale marketplace data, delivering actionable insights for strategic decision-making.

---

## Future Work

- **Sentiment Analysis** : Apply NLP to review text (if available) to extract qualitative satisfaction signals beyond star ratings.
- **Price Prediction Model** : Build a regression model to predict optimal listing price given city, room type, location, and amenities.
- **Occupancy Rate Estimation** : Use the San Francisco Model (reviews as proxy) to estimate occupancy and revenue per listing.
- **Geospatial Analysis** : Map listings density and pricing at the neighbourhood level using latitude/longitude coordinates.
- **Superhost Impact Analysis** : Quantify the premium (if any) that Superhost status commands in pricing and review scores.
- **Time-Series Forecasting** : Forecast listing growth post-COVID using ARIMA or Prophet models.
- **Competitive Benchmarking** : Integrate competitor data (Booking.com, Vrbo) for cross-platform comparisons.
