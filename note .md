# Seasonal Patterns and Cancellation Analysis in Hotel Booking Data

## Project Objective

This project analyzes seasonal hotel booking demand and cancellation
behavior using the Hotel Booking Demand dataset.

The main objectives are to analyze booking demand across months and
hotel types, calculate monthly cancellation rates, compare lead time for
cancelled and non-cancelled bookings, identify important source markets
and market segments, analyze seasonal ADR patterns, and derive
revenue-management insights.

## Dataset

**Dataset:** Hotel Booking Demand\
**Source:** Kaggle --- Jesse Mostipak\
**URL:**
https://www.kaggle.com/datasets/jessemostipak/hotel-booking-demand

The dataset contains **119,390 rows and 32 columns**.

Important columns used in this analysis include `hotel`, `is_canceled`,
`lead_time`, `arrival_date_year`, `arrival_date_month`,
`arrival_date_day_of_month`, `country`, `market_segment`, and `adr`.

## Tools & Technologies

-   Python
-   pandas
-   matplotlib
-   seaborn
-   Jupyter Notebook

## Data Preparation

### Missing Values

Missing values were checked in `country`, `agent`, `company`, and
`children`.

They were handled as follows:

-   `country` → `"Unknown"`
-   `agent` → `0`
-   `company` → `0`
-   `children` → `0`

### Arrival Date

The `arrival_date_year`, `arrival_date_month`, and
`arrival_date_day_of_month` columns were combined into a proper datetime
column called `arrival_date`.

The arrival months were also converted to an ordered categorical
variable so that analyses follow January-to-December order.

## Seasonal Demand Analysis

A pivot table was created with arrival month as rows, hotel type as
columns, and booking count as values.

  Month         City Hotel   Resort Hotel
  ----------- ------------ --------------
  January            3,736          2,193
  February           4,965          3,103
  March              6,458          3,336
  April              7,480          3,609
  May                8,232          3,559
  June               7,894          3,045
  July               8,088          4,573
  August             8,983          4,894
  September          7,400          3,108
  October            7,605          3,555
  November           4,357          2,437
  December           4,132          2,648

August has the highest combined booking demand with **13,877 bookings**,
while January has the lowest with **5,929 bookings**.

City Hotel has a higher booking volume than Resort Hotel in every month,
while Resort Hotel shows a stronger summer increase.

**Visualization:** `booking_heatmap.png`

## Cancellation Analysis

### Monthly Cancellation Rate

Cancellation rate was calculated as:

**Cancelled bookings / Total bookings × 100**

City Hotel has a higher cancellation rate than Resort Hotel in every
month.

-   City Hotel highest: **April --- 46.3%**
-   Resort Hotel highest: **August --- 33.4%**
-   City Hotel lowest: **March --- 36.9%**
-   Resort Hotel lowest: **January --- 14.8%**

**Visualization:** `cancellation_rate.png`

### Lead Time and Cancellation

  Booking status     Average lead time
  ---------------- -------------------
  Not Canceled              79.98 days
  Canceled                 144.85 days

Cancelled bookings have an average lead time approximately **64.87 days
longer** than non-cancelled bookings. This indicates an association
between longer lead times and cancellation behavior, but does not
establish causation.

## Country Analysis

The top 10 countries were identified by total booking volume and their
cancellation rates were calculated.

    Rank Country                    Total bookings   Cancellation rate
  ------ ------------------------ ---------------- -------------------
       1 PRT --- Portugal                   48,590              56.64%
       2 GBR --- United Kingdom             12,129              20.22%
       3 FRA --- France                     10,415              18.57%
       4 ESP --- Spain                       8,568              25.41%
       5 DEU --- Germany                     7,287              16.71%
       6 ITA --- Italy                       3,766              35.40%
       7 IRL --- Ireland                     3,375              24.65%
       8 BEL --- Belgium                     2,342              20.24%
       9 BRA --- Brazil                      2,224              37.32%
      10 NLD --- Netherlands                 2,104              18.39%

Portugal is the largest source market with **48,590 bookings** and has a
**56.64% cancellation rate**.

**Visualization:** `top_10_countries.png`

## Market Segment Analysis

  ------------------------------------------------------------------------
  Market segment      Total bookings Cancelled bookings  Cancellation rate
  --------------- ------------------ ------------------ ------------------
  Online TA                   56,477             20,739             36.72%

  Offline TA/TO               24,219              8,311             34.32%

  Groups                      19,811             12,097             61.06%

  Direct                      12,606              1,934             15.34%

  Corporate                    5,295                992             18.73%

  Complementary                  743                 97             13.06%

  Aviation                       237                 52             21.94%

  Undefined                        2                  2            100.00%
  ------------------------------------------------------------------------

Online TA is the largest market segment with **56,477 bookings**,
representing approximately **47.3%** of all bookings.

Groups has the highest cancellation rate among the major market segments
at **61.06%**.

Complementary has the lowest observed cancellation rate at **13.06%**,
but it contains only 743 bookings. Undefined has a 100% rate based on
only two bookings and should not be treated as a meaningful pattern.

**Visualization:** `market_segment.png`

## Average Daily Rate (ADR) Analysis

Average Daily Rate (ADR) was calculated by month and hotel type.

The analysis shows seasonal variation in ADR. Resort Hotel ADR rises
during the summer and reaches a high level around August, while City
Hotel also shows seasonal variation.

A dual-axis chart was used because the two hotel types have different
ADR ranges.

**Visualization:** `adr_by_month.png`

## Business Insights

### 1. Strong Seasonal Demand

August is the peak booking month with **13,877 bookings**, while January
has the lowest demand with **5,929 bookings**. Seasonal pricing,
capacity planning, and targeted promotions can be aligned with these
demand differences.

### 2. Higher City Hotel Cancellation Risk

City Hotel has a higher cancellation rate than Resort Hotel in every
month, reaching **46.3% in April**. Cancellation risk should therefore
be incorporated into occupancy and expected-revenue forecasting.

### 3. Longer Lead Times Are Associated With Cancellations

Cancelled bookings have an average lead time of **144.85 days**,
compared with **79.98 days** for non-cancelled bookings. Advance
bookings may therefore require closer cancellation monitoring.

### 4. Market Segments Differ in Demand and Risk

Online TA represents approximately **47.3%** of bookings, while Groups
has a **61.06% cancellation rate**. Revenue managers should consider
both booking volume and cancellation risk when managing market segments.

## Key Findings

-   August: **13,877 bookings**
-   January: **5,929 bookings**
-   City Hotel has higher monthly cancellation rates than Resort Hotel
    throughout the year.
-   City Hotel's highest monthly cancellation rate: **46.3%**
-   Resort Hotel's highest monthly cancellation rate: **33.4%**
-   Cancelled booking average lead time: **144.85 days**
-   Non-cancelled booking average lead time: **79.98 days**
-   Portugal is the largest source market: **48,590 bookings**
-   Online TA is the largest market segment: **56,477 bookings**
-   Groups has a **61.06%** cancellation rate
-   Complementary has the lowest observed cancellation rate: **13.06%**

## Limitations

-   The analysis identifies associations and patterns but does not
    establish causal relationships.
-   Cancellation behavior can also be affected by other variables not
    isolated in this analysis.
-   Some countries and market segments have relatively small booking
    volumes.
-   ADR is an average booking-level rate and should not be interpreted
    as total hotel revenue.
-   The dataset represents historical booking behavior.

## Conclusion

The analysis demonstrates clear seasonal patterns in hotel demand and
meaningful differences in cancellation behavior across hotel types,
countries, and market segments.

Booking demand is strongest during the summer, particularly in August.
City Hotel consistently shows higher monthly cancellation rates than
Resort Hotel, while cancelled bookings have substantially longer average
lead times.

Online TA generates the largest share of bookings, while Groups has a
notably high cancellation rate. ADR also varies seasonally, providing
additional context for revenue-management decisions.

## Project Structure

``` text
hotel-booking-analysis/
│
├── hotel_bookings.csv
├── hotel_booking_analysis.ipynb
├── note.md
│
├── booking_heatmap.png
├── cancellation_rate.png
├── top_10_countries.png
├── market_segment.png
└── adr_by_month.png
```
