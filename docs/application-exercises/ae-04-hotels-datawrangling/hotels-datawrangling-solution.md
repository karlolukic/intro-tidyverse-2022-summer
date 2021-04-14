Hotel bookings — data wrangling — solutions
================
Lukas Jürgensmeier

``` r
library(tidyverse)
library(skimr)
```

    ## Warning: package 'skimr' was built under R version 4.0.4

``` r
# From TidyTuesday: https://github.com/rfordatascience/tidytuesday/blob/master/data/2020/2020-02-11/readme.md
hotels <- read_csv("https://raw.githubusercontent.com/rfordatascience/tidytuesday/master/data/2020/2020-02-11/hotels.csv")
```

## Exercises

### Exercise 1.

Warm up! Take a look at an overview of the data with the `skim()`
function.

**Note:** I already gave you the answer to this exercise. You just need
to knit the document and view the output. A definition of all variables
is given in the [Data dictionary](#data-dictionary) section at the end,
though you don’t need to familiarize yourself with all variables in
order to work through these exercises.

``` r
skim(hotels)
```

|                                                  |        |
|:-------------------------------------------------|:-------|
| Name                                             | hotels |
| Number of rows                                   | 119390 |
| Number of columns                                | 32     |
| \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_   |        |
| Column type frequency:                           |        |
| character                                        | 13     |
| Date                                             | 1      |
| numeric                                          | 18     |
| \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ |        |
| Group variables                                  | None   |

Data summary

**Variable type: character**

| skim\_variable        | n\_missing | complete\_rate | min | max | empty | n\_unique | whitespace |
|:----------------------|-----------:|---------------:|----:|----:|------:|----------:|-----------:|
| hotel                 |          0 |              1 |  10 |  12 |     0 |         2 |          0 |
| arrival\_date\_month  |          0 |              1 |   3 |   9 |     0 |        12 |          0 |
| meal                  |          0 |              1 |   2 |   9 |     0 |         5 |          0 |
| country               |          0 |              1 |   2 |   4 |     0 |       178 |          0 |
| market\_segment       |          0 |              1 |   6 |  13 |     0 |         8 |          0 |
| distribution\_channel |          0 |              1 |   3 |   9 |     0 |         5 |          0 |
| reserved\_room\_type  |          0 |              1 |   1 |   1 |     0 |        10 |          0 |
| assigned\_room\_type  |          0 |              1 |   1 |   1 |     0 |        12 |          0 |
| deposit\_type         |          0 |              1 |  10 |  10 |     0 |         3 |          0 |
| agent                 |          0 |              1 |   1 |   4 |     0 |       334 |          0 |
| company               |          0 |              1 |   1 |   4 |     0 |       353 |          0 |
| customer\_type        |          0 |              1 |   5 |  15 |     0 |         4 |          0 |
| reservation\_status   |          0 |              1 |   7 |   9 |     0 |         3 |          0 |

**Variable type: Date**

| skim\_variable            | n\_missing | complete\_rate | min        | max        | median     | n\_unique |
|:--------------------------|-----------:|---------------:|:-----------|:-----------|:-----------|----------:|
| reservation\_status\_date |          0 |              1 | 2014-10-17 | 2017-09-14 | 2016-08-07 |       926 |

**Variable type: numeric**

| skim\_variable                    | n\_missing | complete\_rate |    mean |     sd |      p0 |     p25 |     p50 |  p75 | p100 | hist  |
|:----------------------------------|-----------:|---------------:|--------:|-------:|--------:|--------:|--------:|-----:|-----:|:------|
| is\_canceled                      |          0 |              1 |    0.37 |   0.48 |    0.00 |    0.00 |    0.00 |    1 |    1 | ▇▁▁▁▅ |
| lead\_time                        |          0 |              1 |  104.01 | 106.86 |    0.00 |   18.00 |   69.00 |  160 |  737 | ▇▂▁▁▁ |
| arrival\_date\_year               |          0 |              1 | 2016.16 |   0.71 | 2015.00 | 2016.00 | 2016.00 | 2017 | 2017 | ▃▁▇▁▆ |
| arrival\_date\_week\_number       |          0 |              1 |   27.17 |  13.61 |    1.00 |   16.00 |   28.00 |   38 |   53 | ▅▇▇▇▅ |
| arrival\_date\_day\_of\_month     |          0 |              1 |   15.80 |   8.78 |    1.00 |    8.00 |   16.00 |   23 |   31 | ▇▇▇▇▆ |
| stays\_in\_weekend\_nights        |          0 |              1 |    0.93 |   1.00 |    0.00 |    0.00 |    1.00 |    2 |   19 | ▇▁▁▁▁ |
| stays\_in\_week\_nights           |          0 |              1 |    2.50 |   1.91 |    0.00 |    1.00 |    2.00 |    3 |   50 | ▇▁▁▁▁ |
| adults                            |          0 |              1 |    1.86 |   0.58 |    0.00 |    2.00 |    2.00 |    2 |   55 | ▇▁▁▁▁ |
| children                          |          4 |              1 |    0.10 |   0.40 |    0.00 |    0.00 |    0.00 |    0 |   10 | ▇▁▁▁▁ |
| babies                            |          0 |              1 |    0.01 |   0.10 |    0.00 |    0.00 |    0.00 |    0 |   10 | ▇▁▁▁▁ |
| is\_repeated\_guest               |          0 |              1 |    0.03 |   0.18 |    0.00 |    0.00 |    0.00 |    0 |    1 | ▇▁▁▁▁ |
| previous\_cancellations           |          0 |              1 |    0.09 |   0.84 |    0.00 |    0.00 |    0.00 |    0 |   26 | ▇▁▁▁▁ |
| previous\_bookings\_not\_canceled |          0 |              1 |    0.14 |   1.50 |    0.00 |    0.00 |    0.00 |    0 |   72 | ▇▁▁▁▁ |
| booking\_changes                  |          0 |              1 |    0.22 |   0.65 |    0.00 |    0.00 |    0.00 |    0 |   21 | ▇▁▁▁▁ |
| days\_in\_waiting\_list           |          0 |              1 |    2.32 |  17.59 |    0.00 |    0.00 |    0.00 |    0 |  391 | ▇▁▁▁▁ |
| adr                               |          0 |              1 |  101.83 |  50.54 |   -6.38 |   69.29 |   94.58 |  126 | 5400 | ▇▁▁▁▁ |
| required\_car\_parking\_spaces    |          0 |              1 |    0.06 |   0.25 |    0.00 |    0.00 |    0.00 |    0 |    8 | ▇▁▁▁▁ |
| total\_of\_special\_requests      |          0 |              1 |    0.57 |   0.79 |    0.00 |    0.00 |    0.00 |    1 |    5 | ▇▁▁▁▁ |

### Exercise 2.

Are people traveling last minute? Let’s see…

Fill in the blanks for filtering for hotel bookings where the guest is
**not** from the US (`country` code `"USA"`) and the `lead_time` is less
than 1 day.

**Note:** You will need to set `eval=TRUE` when you have an answer you
want to try out.

``` r
hotels %>%
  filter(
    country != "USA", 
    lead_time < 1
    )
```

    ## # A tibble: 6,174 x 32
    ##    hotel is_canceled lead_time arrival_date_ye~ arrival_date_mo~
    ##    <chr>       <dbl>     <dbl>            <dbl> <chr>           
    ##  1 Reso~           0         0             2015 July            
    ##  2 Reso~           0         0             2015 July            
    ##  3 Reso~           0         0             2015 July            
    ##  4 Reso~           0         0             2015 July            
    ##  5 Reso~           0         0             2015 July            
    ##  6 Reso~           0         0             2015 July            
    ##  7 Reso~           0         0             2015 July            
    ##  8 Reso~           0         0             2015 July            
    ##  9 Reso~           0         0             2015 July            
    ## 10 Reso~           0         0             2015 July            
    ## # ... with 6,164 more rows, and 27 more variables:
    ## #   arrival_date_week_number <dbl>, arrival_date_day_of_month <dbl>,
    ## #   stays_in_weekend_nights <dbl>, stays_in_week_nights <dbl>, adults <dbl>,
    ## #   children <dbl>, babies <dbl>, meal <chr>, country <chr>,
    ## #   market_segment <chr>, distribution_channel <chr>, is_repeated_guest <dbl>,
    ## #   previous_cancellations <dbl>, previous_bookings_not_canceled <dbl>,
    ## #   reserved_room_type <chr>, assigned_room_type <chr>, booking_changes <dbl>,
    ## #   deposit_type <chr>, agent <chr>, company <chr>, days_in_waiting_list <dbl>,
    ## #   customer_type <chr>, adr <dbl>, required_car_parking_spaces <dbl>,
    ## #   total_of_special_requests <dbl>, reservation_status <chr>,
    ## #   reservation_status_date <date>

### Exercise 3.

How many bookings involve at least 1 child **or** baby?

In the following chunk, replace

-   `[AT LEAST]` with the logical operator for “at least” (in two
    places)
-   `[OR]` with the logical operator for “or”

**Note:** You will need to set `eval=TRUE` when you have an answer you
want to try out.

``` r
hotels %>%
  filter(
    children >= 1 | babies >= 1
    ) %>% 
  # optionally, select only the relevant columns to check
  # if your filtering criteria worked
  select(hotel, children, babies)
```

    ## # A tibble: 9,332 x 3
    ##    hotel        children babies
    ##    <chr>           <dbl>  <dbl>
    ##  1 Resort Hotel        1      0
    ##  2 Resort Hotel        2      0
    ##  3 Resort Hotel        2      0
    ##  4 Resort Hotel        2      0
    ##  5 Resort Hotel        1      0
    ##  6 Resort Hotel        1      0
    ##  7 Resort Hotel        2      0
    ##  8 Resort Hotel        2      0
    ##  9 Resort Hotel        0      1
    ## 10 Resort Hotel        0      1
    ## # ... with 9,322 more rows

### Exercise 4.

Do you think it’s more likely to find bookings with children or babies
in city hotels or resort hotels? Test your intuition. Using `filter()`
determine the number of bookings in resort hotels that have more than 1
child **or** baby in the room? Then, do the same for city hotels, and
compare the numbers of rows in the resulting filtered data frames.

Tip: you can run parts of the `dplyr` pipeline by only selecting some
lines. That way, you can easily check the intermediary steps.

``` r
hotels %>% 
  filter(
    hotel == "Resort Hotel",
    children > 1
  ) %>%
  # optionally, select only the relevant columns to check
  # if your filtering criteria worked
  select(hotel, children, babies) %>% 
  # count number of observations
  nrow()
```

    ## [1] 1646

``` r
hotels %>% 
  filter(
    hotel == "Resort Hotel",
    babies > 1
  ) %>%
  # optionally, select only the relevant columns to check
  # if your filtering criteria worked
  select(hotel, children, babies) %>% 
  # count number of observations
  nrow()
```

    ## [1] 9

### Exercise 5.

Create a frequency table of the number of `adults` in a booking. Display
the results in descending order so the most common observation is on
top. What is the most common number of adults in bookings in this
dataset? Are there any surprising results?

**Note:** Don’t forget to label your R chunk as well (where it says
`label-me-1`). Your label should be short, informative, and shouldn’t
include spaces. It also shouldn’t repeat a previous label, otherwise R
Markdown will give you an error about repeated R chunk labels.

``` r
hotels %>% 
  count(adults) %>% 
  arrange(desc(n))
```

    ## # A tibble: 14 x 2
    ##    adults     n
    ##     <dbl> <int>
    ##  1      2 89680
    ##  2      1 23027
    ##  3      3  6202
    ##  4      0   403
    ##  5      4    62
    ##  6     26     5
    ##  7      5     2
    ##  8     20     2
    ##  9     27     2
    ## 10      6     1
    ## 11     10     1
    ## 12     40     1
    ## 13     50     1
    ## 14     55     1

### Exercise 6.

Repeat Exercise 5, once for canceled bookings (`is_canceled` coded as 1)
and once for not canceled bookings (`is_canceled` coded as 0). What does
this reveal about the surprising results you spotted in the previous
exercise?

**Note:** Don’t forget to label your R chunk as well (where it says
`label-me-2`).

``` r
hotels %>% 
  filter(is_canceled == 1) %>% 
  count(adults) %>% 
  arrange(desc(n))
```

    ## # A tibble: 14 x 2
    ##    adults     n
    ##     <dbl> <int>
    ##  1      2 35258
    ##  2      1  6674
    ##  3      3  2151
    ##  4      0   109
    ##  5      4    16
    ##  6     26     5
    ##  7      5     2
    ##  8     20     2
    ##  9     27     2
    ## 10      6     1
    ## 11     10     1
    ## 12     40     1
    ## 13     50     1
    ## 14     55     1

``` r
hotels %>% 
  filter(is_canceled == 0) %>% 
  count(adults) %>% 
  arrange(desc(n))
```

    ## # A tibble: 5 x 2
    ##   adults     n
    ##    <dbl> <int>
    ## 1      2 54422
    ## 2      1 16353
    ## 3      3  4051
    ## 4      0   294
    ## 5      4    46

It appears that most unusual numbers of adults were erroneously booked
and later cancelled.

### Exercise 7.

Calculate minimum, mean, median, and maximum average daily rate (`adr`)
grouped by `hotel` type so that you can get these statistics separately
for resort and city hotels. Which type of hotel is higher, on average?

``` r
hotels %>% 
  group_by(hotel) %>% 
  summarize(
    min_rate = min(adr),
    mean_rate = mean(adr),
    median_rate = median(adr),
    max_rate = max(adr)
  )
```

    ## # A tibble: 2 x 5
    ##   hotel        min_rate mean_rate median_rate max_rate
    ## * <chr>           <dbl>     <dbl>       <dbl>    <dbl>
    ## 1 City Hotel       0        105.         99.9     5400
    ## 2 Resort Hotel    -6.38      95.0        75        508

City Hotels are more expensive, on average.

### Exercise 8.

We observe two unusual values in the summary statistics above – a
negative minimum, and a very high maximum). What types of hotels are
these? Locate these observations in the dataset and find out the arrival
date (year and month) as well as how many people (adults, children, and
babies) stayed in the room. You can investigate the data in the viewer
to locate these values, but preferably you should identify them in a
reproducible way with some code.

**Hint:** For example, you can `filter` for the given `adr` amounts and
`select` the relevant columns.

``` r
# negative daily rate (`adr`)
hotels %>% 
  filter(adr < 0) %>% 
  select(hotel, adr, arrival_date_year, arrival_date_month, adults, children, babies)
```

    ## # A tibble: 1 x 7
    ##   hotel          adr arrival_date_year arrival_date_month adults children babies
    ##   <chr>        <dbl>             <dbl> <chr>               <dbl>    <dbl>  <dbl>
    ## 1 Resort Hotel -6.38              2017 March                   2        0      0

``` r
# very high daily rate (`adr`)
hotels %>% 
  filter(adr > 1000) %>% 
  select(hotel, adr, arrival_date_year, arrival_date_month, adults, children, babies)
```

    ## # A tibble: 1 x 7
    ##   hotel        adr arrival_date_year arrival_date_month adults children babies
    ##   <chr>      <dbl>             <dbl> <chr>               <dbl>    <dbl>  <dbl>
    ## 1 City Hotel  5400              2016 March                   2        0      0

## Data dictionary

Below is the full data dictionary. Note that it is long (there are lots
of variables in the data), but we will be using a limited set of the
variables for our analysis.

| variable                          | class     | description                                                                                                                                                                                                                                                                                                                                                                                                                         |
|:----------------------------------|:----------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| hotel                             | character | Hotel (H1 = Resort Hotel or H2 = City Hotel)                                                                                                                                                                                                                                                                                                                                                                                        |
| is\_canceled                      | double    | Value indicating if the booking was canceled (1) or not (0)                                                                                                                                                                                                                                                                                                                                                                         |
| lead\_time                        | double    | Number of days that elapsed between the entering date of the booking into the PMS and the arrival date                                                                                                                                                                                                                                                                                                                              |
| arrival\_date\_year               | double    | Year of arrival date                                                                                                                                                                                                                                                                                                                                                                                                                |
| arrival\_date\_month              | character | Month of arrival date                                                                                                                                                                                                                                                                                                                                                                                                               |
| arrival\_date\_week\_number       | double    | Week number of year for arrival date                                                                                                                                                                                                                                                                                                                                                                                                |
| arrival\_date\_day\_of\_month     | double    | Day of arrival date                                                                                                                                                                                                                                                                                                                                                                                                                 |
| stays\_in\_weekend\_nights        | double    | Number of weekend nights (Saturday or Sunday) the guest stayed or booked to stay at the hotel                                                                                                                                                                                                                                                                                                                                       |
| stays\_in\_week\_nights           | double    | Number of week nights (Monday to Friday) the guest stayed or booked to stay at the hotel                                                                                                                                                                                                                                                                                                                                            |
| adults                            | double    | Number of adults                                                                                                                                                                                                                                                                                                                                                                                                                    |
| children                          | double    | Number of children                                                                                                                                                                                                                                                                                                                                                                                                                  |
| babies                            | double    | Number of babies                                                                                                                                                                                                                                                                                                                                                                                                                    |
| meal                              | character | Type of meal booked. Categories are presented in standard hospitality meal packages: <br> Undefined/SC – no meal package;<br>BB – Bed & Breakfast; <br> HB – Half board (breakfast and one other meal – usually dinner); <br> FB – Full board (breakfast, lunch and dinner)                                                                                                                                                         |
| country                           | character | Country of origin. Categories are represented in the ISO 3155–3:2013 format                                                                                                                                                                                                                                                                                                                                                         |
| market\_segment                   | character | Market segment designation. In categories, the term “TA” means “Travel Agents” and “TO” means “Tour Operators”                                                                                                                                                                                                                                                                                                                      |
| distribution\_channel             | character | Booking distribution channel. The term “TA” means “Travel Agents” and “TO” means “Tour Operators”                                                                                                                                                                                                                                                                                                                                   |
| is\_repeated\_guest               | double    | Value indicating if the booking name was from a repeated guest (1) or not (0)                                                                                                                                                                                                                                                                                                                                                       |
| previous\_cancellations           | double    | Number of previous bookings that were cancelled by the customer prior to the current booking                                                                                                                                                                                                                                                                                                                                        |
| previous\_bookings\_not\_canceled | double    | Number of previous bookings not cancelled by the customer prior to the current booking                                                                                                                                                                                                                                                                                                                                              |
| reserved\_room\_type              | character | Code of room type reserved. Code is presented instead of designation for anonymity reasons                                                                                                                                                                                                                                                                                                                                          |
| assigned\_room\_type              | character | Code for the type of room assigned to the booking. Sometimes the assigned room type differs from the reserved room type due to hotel operation reasons (e.g. overbooking) or by customer request. Code is presented instead of designation for anonymity reasons                                                                                                                                                                    |
| booking\_changes                  | double    | Number of changes/amendments made to the booking from the moment the booking was entered on the PMS until the moment of check-in or cancellation                                                                                                                                                                                                                                                                                    |
| deposit\_type                     | character | Indication on if the customer made a deposit to guarantee the booking. This variable can assume three categories:<br>No Deposit – no deposit was made;<br>Non Refund – a deposit was made in the value of the total stay cost;<br>Refundable – a deposit was made with a value under the total cost of stay.                                                                                                                        |
| agent                             | character | ID of the travel agency that made the booking                                                                                                                                                                                                                                                                                                                                                                                       |
| company                           | character | ID of the company/entity that made the booking or responsible for paying the booking. ID is presented instead of designation for anonymity reasons                                                                                                                                                                                                                                                                                  |
| days\_in\_waiting\_list           | double    | Number of days the booking was in the waiting list before it was confirmed to the customer                                                                                                                                                                                                                                                                                                                                          |
| customer\_type                    | character | Type of booking, assuming one of four categories:<br>Contract - when the booking has an allotment or other type of contract associated to it;<br>Group – when the booking is associated to a group;<br>Transient – when the booking is not part of a group or contract, and is not associated to other transient booking;<br>Transient-party – when the booking is transient, but is associated to at least other transient booking |
| adr                               | double    | Average Daily Rate as defined by dividing the sum of all lodging transactions by the total number of staying nights                                                                                                                                                                                                                                                                                                                 |
| required\_car\_parking\_spaces    | double    | Number of car parking spaces required by the customer                                                                                                                                                                                                                                                                                                                                                                               |
| total\_of\_special\_requests      | double    | Number of special requests made by the customer (e.g. twin bed or high floor)                                                                                                                                                                                                                                                                                                                                                       |
| reservation\_status               | character | Reservation last status, assuming one of three categories:<br>Canceled – booking was canceled by the customer;<br>Check-Out – customer has checked in but already departed;<br>No-Show – customer did not check-in and did inform the hotel of the reason why                                                                                                                                                                       |
| reservation\_status\_date         | double    | Date at which the last status was set. This variable can be used in conjunction with the ReservationStatus to understand when was the booking canceled or when did the customer checked-out of the hotel                                                                                                                                                                                                                            |