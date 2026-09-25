# Seasonal Patterns and Cancellation Analysis in Hotel Booking Data

This project analyzes hotel booking demand, seasonal patterns, cancellation behavior, customer source markets, market segments, and Average Daily Rate (ADR) using the Hotel Booking Demand dataset.

## Project Objective

The objective is to use time-based aggregation and pivot tables to understand hotel booking demand and cancellation behavior.

The analysis focuses on:

- Seasonal booking demand across months and hotel types
- Monthly cancellation rates
- Lead time differences between cancelled and non-cancelled bookings
- Top countries by booking volume and their cancellation rates
- Booking distribution across market segments
- Seasonal ADR patterns
- Revenue-management implications

## Dataset

**Dataset:** Hotel Booking Demand  
**Source:** Kaggle — Jesse Mostipak  
**Link:** https://www.kaggle.com/datasets/jessemostipak/hotel-booking-demand

The dataset contains **119,390 rows and 32 columns**.

### Main Columns Used

| Column | Description |
|---|---|
| `hotel` | Hotel type |
| `is_canceled` | Whether the booking was cancelled |
| `lead_time` | Number of days between booking and arrival |
| `arrival_date_year` | Arrival year |
| `arrival_date_month` | Arrival month |
| `arrival_date_day_of_month` | Arrival day |
| `country` | Guest country |
| `market_segment` | Booking market segment |
| `adr` | Average Daily Rate |

## Tools & Technologies

- Python
- pandas
- matplotlib
- seaborn
- Jupyter Notebook

## Data Preparation

### Missing Values

Missing values were checked in `country`, `agent`, `company`, and `children`.

They were handled as follows:

| Column | Treatment |
|---|---|
| `country` | Fill with `"Unknown"` |
| `agent` | Fill with `0` |
| `company` | Fill with `0` |
| `children` | Fill with `0` |

### Creating the Arrival Date

The original arrival date components were combined into a new `arrival_date` column with the `datetime64[ns]` data type.

The arrival month was converted to an ordered categorical variable so that analysis follows January through December.

## Seasonal Demand Analysis

A pivot table was created with arrival month as rows, hotel type as columns, and booking count as values.

| Month | City Hotel | Resort Hotel |
|---|---:|---:|
| January | 3,736 | 2,193 |
| February | 4,965 | 3,103 |
| March | 6,458 | 3,336 |
| April | 7,480 | 3,609 |
| May | 8,232 | 3,559 |
| June | 7,894 | 3,045 |
| July | 8,088 | 4,573 |
| August | 8,983 | 4,894 |
| September | 7,400 | 3,108 |
| October | 7,605 | 3,555 |
| November | 4,357 | 2,437 |
| December | 4,132 | 2,648 |

August has the highest combined demand with **13,877 bookings**, while January has the lowest with **5,929 bookings**.

City Hotel has a higher booking volume than Resort Hotel in every month, while Resort Hotel shows a stronger summer increase.

### Booking Demand Heatmap

![Monthly Hotel Booking Demand](hotel_readme_assets/booking_heatmap.png)

## Cancellation Analysis

Cancellation rate was calculated as:

**Cancelled Bookings / Total Bookings × 100**

City Hotel has a higher cancellation rate than Resort Hotel in every month.

- City Hotel highest: **46.3% in April**
- Resort Hotel highest: **33.4% in August**
- City Hotel lowest: **36.9% in March**
- Resort Hotel lowest: **14.8% in January**

### Monthly Cancellation Rate

![Monthly Cancellation Rate](hotel_readme_assets/cancellation_rate.png)

### Lead Time Comparison

| Booking Status | Average Lead Time |
|---|---:|
| Not Canceled | 79.98 days |
| Canceled | 144.85 days |

Cancelled bookings have an average lead time approximately **64.87 days longer** than non-cancelled bookings.

This indicates an association between longer lead times and cancellation behavior, but does not establish causation.

## Country Analysis

The top 10 countries were identified by total booking volume.

| Rank | Country | Total Bookings | Cancellation Rate |
|---:|---|---:|---:|
| 1 | PRT — Portugal | 48,590 | 56.64% |
| 2 | GBR — United Kingdom | 12,129 | 20.22% |
| 3 | FRA — France | 10,415 | 18.57% |
| 4 | ESP — Spain | 8,568 | 25.41% |
| 5 | DEU — Germany | 7,287 | 16.71% |
| 6 | ITA — Italy | 3,766 | 35.40% |
| 7 | IRL — Ireland | 3,375 | 24.65% |
| 8 | BEL — Belgium | 2,342 | 20.24% |
| 9 | BRA — Brazil | 2,224 | 37.32% |
| 10 | NLD — Netherlands | 2,104 | 18.39% |

Portugal is the largest source market with **48,590 bookings** and a cancellation rate of **56.64%**.

### Top 10 Countries Visualization

![Top 10 Countries by Total Bookings](hotel_readme_assets/top_10_countries.png)

## Market Segment Analysis

| Market Segment | Total Bookings | Cancelled Bookings | Cancellation Rate |
|---|---:|---:|---:|
| Online TA | 56,477 | 20,739 | 36.72% |
| Offline TA/TO | 24,219 | 8,311 | 34.32% |
| Groups | 19,811 | 12,097 | 61.06% |
| Direct | 12,606 | 1,934 | 15.34% |
| Corporate | 5,295 | 992 | 18.73% |
| Complementary | 743 | 97 | 13.06% |
| Aviation | 237 | 52 | 21.94% |
| Undefined | 2 | 2 | 100.00% |

Online TA is the largest market segment with **56,477 bookings**, approximately **47.3%** of all bookings.

Groups has the highest cancellation rate among the major segments at **61.06%**.

Complementary has the lowest observed cancellation rate at **13.06%**, although it contains only 743 bookings. Undefined has a 100% rate based on only two bookings and should not be treated as a meaningful pattern.

### Market Segment Visualization

![Booking Distribution by Market Segment](hotel_readme_assets/market_segment.png)

## Average Daily Rate (ADR) Analysis

ADR stands for **Average Daily Rate** and represents the average room rate associated with hotel bookings.

Average ADR was calculated by month and hotel type. The analysis shows seasonal variation in ADR. Resort Hotel ADR increases during the summer and reaches a high level around August, while City Hotel also shows seasonal variation.

A dual-axis chart was used because City Hotel and Resort Hotel have different ADR ranges.

### ADR Visualization

![Average Daily Rate by Month and Hotel Type](hotel_readme_assets/adr_by_month.png)

## Bonus Analysis

### Lowest Cancellation-Rate Market Segment

The market segment with the lowest observed cancellation rate is:

**Complementary — 13.06%**

This segment contains only **743 bookings**, so its cancellation rate should be interpreted together with its smaller sample size.

## Business Insights

### 1. Strong Seasonal Demand

August is the peak booking month with **13,877 bookings**, while January has the lowest demand with **5,929 bookings**.

Revenue managers can use seasonal pricing, capacity planning, and targeted promotions to respond to differences between peak and low-demand periods.

### 2. Higher City Hotel Cancellation Risk

City Hotel has a higher cancellation rate than Resort Hotel in every month, reaching **46.3% in April**.

Cancellation risk should therefore be incorporated into occupancy and expected-revenue forecasting.

### 3. Longer Lead Times Are Associated With Cancellations

Cancelled bookings have an average lead time of **144.85 days**, compared with **79.98 days** for non-cancelled bookings.

Advance bookings may therefore require closer cancellation monitoring.

### 4. Market Segments Differ in Demand and Cancellation Risk

Online TA represents approximately **47.3%** of bookings, while Groups has a **61.06% cancellation rate**.

Revenue managers should consider both booking volume and cancellation risk when managing market segments.

## Key Findings

- **August:** 13,877 bookings
- **January:** 5,929 bookings
- City Hotel has higher monthly cancellation rates than Resort Hotel throughout the year.
- City Hotel's highest monthly cancellation rate: **46.3%**
- Resort Hotel's highest monthly cancellation rate: **33.4%**
- Cancelled booking average lead time: **144.85 days**
- Non-cancelled booking average lead time: **79.98 days**
- Portugal is the largest source market: **48,590 bookings**
- Online TA is the largest market segment: **56,477 bookings**
- Groups has a **61.06%** cancellation rate
- Complementary has the lowest observed cancellation rate: **13.06%**

## Limitations

- The analysis identifies associations and patterns but does not establish causal relationships.
- Cancellation behavior can be affected by other variables not isolated in this analysis.
- Some countries and market segments have relatively small booking volumes.
- ADR is an average booking-level rate and should not be interpreted as total hotel revenue.
- The dataset represents historical booking behavior and may not reflect current hotel-market conditions.

## Conclusion

This project demonstrates how time-based aggregation, pivot tables, and visualization can be used to analyze hotel demand and cancellation behavior.

The results show clear seasonal patterns, with August representing the highest booking-demand period. City Hotel consistently has higher cancellation rates than Resort Hotel, and cancelled bookings have substantially longer average lead times.

Online TA is the largest booking channel, while Groups has a notably high cancellation rate. Seasonal ADR patterns provide additional context for understanding hotel pricing and demand.

Together, booking volume, cancellation behavior, lead time, market segment, country, and ADR provide useful information for hotel revenue-management analysis.

## Project Structure

```text
hotel-booking-analysis/
│
├── README.md
├── note.md
├── hotel_booking_analysis.ipynb
├── hotel_bookings.csv
├── hotel_bookings_cleaned.csv
│
└── hotel_readme_assets/
    ├── booking_heatmap.png
    ├── cancellation_rate.png
    ├── top_10_countries.png
    ├── market_segment.png
    └── adr_by_month.png
