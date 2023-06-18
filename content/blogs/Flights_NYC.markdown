---
title: "Homework 1"
author: "Eugene Nesterenko"
date: 2023-05-14
format: 
  docx: default
  html:
    toc: true
    toc_float: true
    code-fold: true
editor: visual
---




# Data Manipulation

## Problem 1: Use logical operators to find flights that:

    -   Had an arrival delay of two or more hours (\> 120 minutes)
    -   Flew to Houston (IAH or HOU)
    -   Were operated by United (`UA`), American (`AA`), or Delta (`DL`)
    -   Departed in summer (July, August, and September)
    -   Arrived more than two hours late, but didn't leave late
    -   Were delayed by at least an hour, but made up over 30 minutes in flight



```r
glimpse(flights) 
```

```
## Rows: 336,776
## Columns: 19
## $ year           <int> 2013, 2013, 2013, 2013, 2013, 2013, 2013, 2013, 2013, 2…
## $ month          <int> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1…
## $ day            <int> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1…
## $ dep_time       <int> 517, 533, 542, 544, 554, 554, 555, 557, 557, 558, 558, …
## $ sched_dep_time <int> 515, 529, 540, 545, 600, 558, 600, 600, 600, 600, 600, …
## $ dep_delay      <dbl> 2, 4, 2, -1, -6, -4, -5, -3, -3, -2, -2, -2, -2, -2, -1…
## $ arr_time       <int> 830, 850, 923, 1004, 812, 740, 913, 709, 838, 753, 849,…
## $ sched_arr_time <int> 819, 830, 850, 1022, 837, 728, 854, 723, 846, 745, 851,…
## $ arr_delay      <dbl> 11, 20, 33, -18, -25, 12, 19, -14, -8, 8, -2, -3, 7, -1…
## $ carrier        <chr> "UA", "UA", "AA", "B6", "DL", "UA", "B6", "EV", "B6", "…
## $ flight         <int> 1545, 1714, 1141, 725, 461, 1696, 507, 5708, 79, 301, 4…
## $ tailnum        <chr> "N14228", "N24211", "N619AA", "N804JB", "N668DN", "N394…
## $ origin         <chr> "EWR", "LGA", "JFK", "JFK", "LGA", "EWR", "EWR", "LGA",…
## $ dest           <chr> "IAH", "IAH", "MIA", "BQN", "ATL", "ORD", "FLL", "IAD",…
## $ air_time       <dbl> 227, 227, 160, 183, 116, 150, 158, 53, 140, 138, 149, 1…
## $ distance       <dbl> 1400, 1416, 1089, 1576, 762, 719, 1065, 229, 944, 733, …
## $ hour           <dbl> 5, 5, 5, 5, 6, 5, 6, 6, 6, 6, 6, 6, 6, 6, 6, 5, 6, 6, 6…
## $ minute         <dbl> 15, 29, 40, 45, 0, 58, 0, 0, 0, 0, 0, 0, 0, 0, 0, 59, 0…
## $ time_hour      <dttm> 2013-01-01 05:00:00, 2013-01-01 05:00:00, 2013-01-01 0…
```

```r
# Had an arrival delay of two or more hours (> 120 minutes)
flights %>% 
  filter(arr_delay > 120)
```

```
## # A tibble: 10,034 × 19
##     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
##    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
##  1  2013     1     1      811            630       101     1047            830
##  2  2013     1     1      848           1835       853     1001           1950
##  3  2013     1     1      957            733       144     1056            853
##  4  2013     1     1     1114            900       134     1447           1222
##  5  2013     1     1     1505           1310       115     1638           1431
##  6  2013     1     1     1525           1340       105     1831           1626
##  7  2013     1     1     1549           1445        64     1912           1656
##  8  2013     1     1     1558           1359       119     1718           1515
##  9  2013     1     1     1732           1630        62     2028           1825
## 10  2013     1     1     1803           1620       103     2008           1750
## # ℹ 10,024 more rows
## # ℹ 11 more variables: arr_delay <dbl>, carrier <chr>, flight <int>,
## #   tailnum <chr>, origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>,
## #   hour <dbl>, minute <dbl>, time_hour <dttm>
```

```r
# Flew to Houston (IAH or HOU)
flights %>% 
  # filter for multiple destinations using OR operator
  filter(dest == "IAH" | dest == "HOU") 
```

```
## # A tibble: 9,313 × 19
##     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
##    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
##  1  2013     1     1      517            515         2      830            819
##  2  2013     1     1      533            529         4      850            830
##  3  2013     1     1      623            627        -4      933            932
##  4  2013     1     1      728            732        -4     1041           1038
##  5  2013     1     1      739            739         0     1104           1038
##  6  2013     1     1      908            908         0     1228           1219
##  7  2013     1     1     1028           1026         2     1350           1339
##  8  2013     1     1     1044           1045        -1     1352           1351
##  9  2013     1     1     1114            900       134     1447           1222
## 10  2013     1     1     1205           1200         5     1503           1505
## # ℹ 9,303 more rows
## # ℹ 11 more variables: arr_delay <dbl>, carrier <chr>, flight <int>,
## #   tailnum <chr>, origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>,
## #   hour <dbl>, minute <dbl>, time_hour <dttm>
```

```r
# Were operated by United (`UA`), American (`AA`), or Delta (`DL`)
flights %>% 
  # filter for multiple carriers using a vector (list) of possible values
  filter(carrier %in% c("UA","AA","DL"))
```

```
## # A tibble: 139,504 × 19
##     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
##    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
##  1  2013     1     1      517            515         2      830            819
##  2  2013     1     1      533            529         4      850            830
##  3  2013     1     1      542            540         2      923            850
##  4  2013     1     1      554            600        -6      812            837
##  5  2013     1     1      554            558        -4      740            728
##  6  2013     1     1      558            600        -2      753            745
##  7  2013     1     1      558            600        -2      924            917
##  8  2013     1     1      558            600        -2      923            937
##  9  2013     1     1      559            600        -1      941            910
## 10  2013     1     1      559            600        -1      854            902
## # ℹ 139,494 more rows
## # ℹ 11 more variables: arr_delay <dbl>, carrier <chr>, flight <int>,
## #   tailnum <chr>, origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>,
## #   hour <dbl>, minute <dbl>, time_hour <dttm>
```

```r
# Departed in summer (July, August, and September)
flights %>%
  # filter for multiple months using a vector of possible numerical month values
  filter(month %in% c(7,8,9))
```

```
## # A tibble: 86,326 × 19
##     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
##    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
##  1  2013     7     1        1           2029       212      236           2359
##  2  2013     7     1        2           2359         3      344            344
##  3  2013     7     1       29           2245       104      151              1
##  4  2013     7     1       43           2130       193      322             14
##  5  2013     7     1       44           2150       174      300            100
##  6  2013     7     1       46           2051       235      304           2358
##  7  2013     7     1       48           2001       287      308           2305
##  8  2013     7     1       58           2155       183      335             43
##  9  2013     7     1      100           2146       194      327             30
## 10  2013     7     1      100           2245       135      337            135
## # ℹ 86,316 more rows
## # ℹ 11 more variables: arr_delay <dbl>, carrier <chr>, flight <int>,
## #   tailnum <chr>, origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>,
## #   hour <dbl>, minute <dbl>, time_hour <dttm>
```

```r
# Arrived more than two hours late, but didn't leave late
flights %>% 
  # filter with criteria for departure and arrival delay using AND operator
  filter(dep_delay <= 0 & arr_delay > 120)
```

```
## # A tibble: 29 × 19
##     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
##    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
##  1  2013     1    27     1419           1420        -1     1754           1550
##  2  2013    10     7     1350           1350         0     1736           1526
##  3  2013    10     7     1357           1359        -2     1858           1654
##  4  2013    10    16      657            700        -3     1258           1056
##  5  2013    11     1      658            700        -2     1329           1015
##  6  2013     3    18     1844           1847        -3       39           2219
##  7  2013     4    17     1635           1640        -5     2049           1845
##  8  2013     4    18      558            600        -2     1149            850
##  9  2013     4    18      655            700        -5     1213            950
## 10  2013     5    22     1827           1830        -3     2217           2010
## # ℹ 19 more rows
## # ℹ 11 more variables: arr_delay <dbl>, carrier <chr>, flight <int>,
## #   tailnum <chr>, origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>,
## #   hour <dbl>, minute <dbl>, time_hour <dttm>
```

```r
# Were delayed by at least an hour, but made up over 30 minutes in flight
flights %>%
  # filter with criteria for departure and make up time using sequential filters
  filter(dep_delay >= 60) %>% 
  filter((dep_delay - arr_delay) > 30)
```

```
## # A tibble: 1,844 × 19
##     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
##    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
##  1  2013     1     1     2205           1720       285       46           2040
##  2  2013     1     1     2326           2130       116      131             18
##  3  2013     1     3     1503           1221       162     1803           1555
##  4  2013     1     3     1839           1700        99     2056           1950
##  5  2013     1     3     1850           1745        65     2148           2120
##  6  2013     1     3     1941           1759       102     2246           2139
##  7  2013     1     3     1950           1845        65     2228           2227
##  8  2013     1     3     2015           1915        60     2135           2111
##  9  2013     1     3     2257           2000       177       45           2224
## 10  2013     1     4     1917           1700       137     2135           1950
## # ℹ 1,834 more rows
## # ℹ 11 more variables: arr_delay <dbl>, carrier <chr>, flight <int>,
## #   tailnum <chr>, origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>,
## #   hour <dbl>, minute <dbl>, time_hour <dttm>
```


We have found an unusual result for the *Arrived more than two hours late, but didn't leave late* filter. It must be the case of currupted data - we can hardly imagine flights that spent more than additional 1000 minutes in the air (arrival time delay was over 1000 minutes with non-positive departure delay)

## Problem 2: What months had the highest and lowest proportion of cancelled flights? Interpret any seasonal patterns. To determine if a flight was cancelled use the following code

<!-- -->

    flights %>% 
      filter(is.na(dep_time)) 



```r
# What months had the highest and lowest % of cancelled flights?

# First, we create two dataframes - cancelled flights and total flights - with summary statistics

# Cancelled flights dataframe
cancelled_flights <- flights %>%
  
  # filter for NA values
  filter(is.na(dep_time)) %>%   
  
  # grouping dataset by months to calculate summary statistics
  group_by(month) %>%
  
  # dataframe is already for the cancelled flights, we just count the number of cases by month
  summarise(number_cancelled = n())   

# Total flights dataframe
total_flights <- flights %>%
  
  # no need to filter for the cancelled flights
  
  # grouping dataset by months to calculate summary statistics
  group_by(month) %>% 
  
  # dataframe is already for the total flights, we just count the total number of fligths by month
  summarise(number_total = n())   

# Joining two dataframes to have counts of cancelled and total flights in one table
# We expect each month to have non-NA value of cancelled and total flights - hence, use inner join
cancelled_percentage_flights <- inner_join(x = cancelled_flights, y = total_flights, by = "month")

# Adding new variable - percentage of cancelled flights, and arranging to find highest and lowest cases
cancelled_percentage_flights %>% 
  
  # Add a new variable for the percentage as (N of cancelled / N of total)*100, up to 1 digit precision
  mutate(percentage_cancelled = round((number_cancelled/number_total) * 100, digits = 1)) %>%
  
  # Arranging in descending order on percentage of cancelled flights
  arrange(desc(percentage_cancelled))
```

```
## # A tibble: 12 × 4
##    month number_cancelled number_total percentage_cancelled
##    <int>            <int>        <int>                <dbl>
##  1     2             1261        24951                  5.1
##  2     6             1009        28243                  3.6
##  3    12             1025        28135                  3.6
##  4     7              940        29425                  3.2
##  5     3              861        28834                  3  
##  6     4              668        28330                  2.4
##  7     5              563        28796                  2  
##  8     1              521        27004                  1.9
##  9     8              486        29327                  1.7
## 10     9              452        27574                  1.6
## 11    11              233        27268                  0.9
## 12    10              236        28889                  0.8
```


February has **the highest** proportion of cancelled flights (5.1%), while October has **the lowest** (0.8%). **Our hypothesis is that in February weather conditions in NYC often do not permit the plane to take off** (cold weather, ice on the runway, blizzard). Same factors could contribute to higher average delay time (though this hypothesis needs to be verified).

**For October-November** (percentage is similar), **perhaps, weather conditions are most favourable.** We also see the **seasonal factor only for autumn months (September - November), which indicates low percentage of cancelled flights**. Other seasons do not show a clear pattern.

## Problem 3: What plane (specified by the `tailnum` variable) traveled the most times from New York City airports in 2013? Please `left_join()` the resulting table with the table `planes` (also included in the `nycflights13` package).

For the plane with the greatest number of flights and that had more than 50 seats, please create a table where it flew to during 2013.



```r
# Saving and printing a new table for number of flights by plane (tailnum)
(
flights_by_plane <- flights %>%  # use base dataset flights as a starting point
  
  # Selecting only year 2013
  filter(year == 2013) %>%
  
  # Deleting rows with unknown tail number (otherwise distorts statistics)
  drop_na(tailnum) %>%
    
  # Creating a dataframe grouped by plane
  group_by(tailnum) %>%
  
  # Counting number of flights by plane
  summarize(count_flights = n()) %>% 
  
  # Arranging in descending order to find the plane that travelled the most
  arrange(desc(count_flights))
)
```

```
## # A tibble: 4,043 × 2
##    tailnum count_flights
##    <chr>           <int>
##  1 N725MQ            575
##  2 N722MQ            513
##  3 N723MQ            507
##  4 N711MQ            486
##  5 N713MQ            483
##  6 N258JB            427
##  7 N298JB            407
##  8 N353JB            404
##  9 N351JB            402
## 10 N735MQ            396
## # ℹ 4,033 more rows
```

```r
# Joining the data on flight count with planes details. We want to preserve data on number of flights regardless of whether the tailnumber is registered in "planes" dictionary - hence, use the left join.
plane_data_number_flights <- left_join(x = flights_by_plane, y = planes, by = "tailnum")

# Print head rows of new table to take a look at data
head(plane_data_number_flights)
```

```
## # A tibble: 6 × 10
##   tailnum count_flights  year type        manufacturer model engines seats speed
##   <chr>           <int> <int> <chr>       <chr>        <chr>   <int> <int> <int>
## 1 N725MQ            575    NA <NA>        <NA>         <NA>       NA    NA    NA
## 2 N722MQ            513    NA <NA>        <NA>         <NA>       NA    NA    NA
## 3 N723MQ            507    NA <NA>        <NA>         <NA>       NA    NA    NA
## 4 N711MQ            486  1976 Fixed wing… GULFSTREAM … G115…       2    22    NA
## 5 N713MQ            483    NA <NA>        <NA>         <NA>       NA    NA    NA
## 6 N258JB            427  2006 Fixed wing… EMBRAER      ERJ …       2    20    NA
## # ℹ 1 more variable: engine <chr>
```

```r
# We want to include only planes with more than 50 seats
# For this, we would save a new table
plane_data_number_flights_many_seats <- plane_data_number_flights %>%
  
  # Drop cases where number of seats is unknown (probably a redundant action, given the next filter)
  drop_na(seats) %>%
  # Leave only planes with over 50 seats
  filter(seats > 50)

  # dataframe was already arrange from most frequent to least frequent flyers, no need to arrange further

# Find the plane with hightest number of flights that has over 50 seats
head(plane_data_number_flights_many_seats,1)
```

```
## # A tibble: 1 × 10
##   tailnum count_flights  year type        manufacturer model engines seats speed
##   <chr>           <int> <int> <chr>       <chr>        <chr>   <int> <int> <int>
## 1 N328AA            393  1986 Fixed wing… BOEING       767-…       2   255    NA
## # ℹ 1 more variable: engine <chr>
```

```r
# Save the most frequent flyer (tailnum) to a separate list (we don't know how to save to a single variable)
frequent_flyer <- plane_data_number_flights_many_seats[1:1,1:1]

# Save and print a table containing destinanations of the most frequent flyer
(
frequent_flyer_destinations <- flights %>% 
  
  # Selecting only the most frequently flying plane using a newly created list
  filter(tailnum %in% frequent_flyer) %>%
    
  # Selecting only year 2013
  filter(year == 2013) %>%
    
  # Showing only columns for plane (tail number) and destination
  select(c("tailnum","dest"))
)
```

```
## # A tibble: 393 × 2
##    tailnum dest 
##    <chr>   <chr>
##  1 N328AA  LAX  
##  2 N328AA  LAX  
##  3 N328AA  LAX  
##  4 N328AA  LAX  
##  5 N328AA  LAX  
##  6 N328AA  LAX  
##  7 N328AA  LAX  
##  8 N328AA  LAX  
##  9 N328AA  LAX  
## 10 N328AA  LAX  
## # ℹ 383 more rows
```


The unconditioned arrangement shows that plane **N725MQ** has the highest number of flights, 575.

However, if we apply the filter on number of seats (*more than 50*), the result changes: now **N328AA** tops the list with 393 flights. The data frame **frequent_flyer_destinations** shows the destinations to which plane with tail number N328AA flew in 2013 - as expected, it has 393 rows.

We have tried to make a code more robust, saving the variable (list) for most frequent flyer and later applying as an input for flights filter. If the dataset changes, so might change the tail number of most frequent flyer - the code supports such case.

## Problem 4: The `nycflights13` package includes a table (`weather`) that describes the weather during 2013. Use that table to answer the following questions:

    -   What is the distribution of temperature (`temp`) in July 2013? Identify any important outliers in terms of the `wind_speed` variable.
    -   What is the relationship between `dewp` and `humid`?
    -   What is the relationship between `precip` and `visib`?



```r
head(weather)
```

```
## # A tibble: 6 × 15
##   origin  year month   day  hour  temp  dewp humid wind_dir wind_speed wind_gust
##   <chr>  <int> <int> <int> <int> <dbl> <dbl> <dbl>    <dbl>      <dbl>     <dbl>
## 1 EWR     2013     1     1     1  39.0  26.1  59.4      270      10.4         NA
## 2 EWR     2013     1     1     2  39.0  27.0  61.6      250       8.06        NA
## 3 EWR     2013     1     1     3  39.0  28.0  64.4      240      11.5         NA
## 4 EWR     2013     1     1     4  39.9  28.0  62.2      250      12.7         NA
## 5 EWR     2013     1     1     5  39.0  28.0  64.4      260      12.7         NA
## 6 EWR     2013     1     1     6  37.9  28.0  67.2      240      11.5         NA
## # ℹ 4 more variables: precip <dbl>, pressure <dbl>, visib <dbl>,
## #   time_hour <dttm>
```

```r
# Save a dataframe for July 2013 only)
weather_july_2013 <- weather %>% 
  filter(year == 2013 & month == 7)

# Get summary statistics for July 2013, which allows to infer data about distribution and outliers for temperature and wind speed
skim(weather_july_2013)
```


Table: <span id="tab:unnamed-chunk-5"></span>Table 1: Data summary

|                         |                  |
|:------------------------|:-----------------|
|Name                     |weather_july_2013 |
|Number of rows           |2228              |
|Number of columns        |15                |
|_______________________  |                  |
|Column type frequency:   |                  |
|character                |1                 |
|numeric                  |13                |
|POSIXct                  |1                 |
|________________________ |                  |
|Group variables          |None              |


**Variable type: character**

|skim_variable | n_missing| complete_rate| min| max| empty| n_unique| whitespace|
|:-------------|---------:|-------------:|---:|---:|-----:|--------:|----------:|
|origin        |         0|             1|   3|   3|     0|        3|          0|


**Variable type: numeric**

|skim_variable | n_missing| complete_rate|    mean|    sd|      p0|     p25|     p50|     p75|    p100|hist  |
|:-------------|---------:|-------------:|-------:|-----:|-------:|-------:|-------:|-------:|-------:|:-----|
|year          |         0|          1.00| 2013.00|  0.00| 2013.00| 2013.00| 2013.00| 2013.00| 2013.00|▁▁▇▁▁ |
|month         |         0|          1.00|    7.00|  0.00|    7.00|    7.00|    7.00|    7.00|    7.00|▁▁▇▁▁ |
|day           |         0|          1.00|   16.00|  8.93|    1.00|    8.00|   16.00|   24.00|   31.00|▇▇▇▇▇ |
|hour          |         0|          1.00|   11.51|  6.92|    0.00|    6.00|   12.00|   18.00|   23.00|▇▇▆▇▇ |
|temp          |         0|          1.00|   80.07|  7.12|   64.04|   75.02|   78.98|   84.20|  100.04|▂▇▇▃▂ |
|dewp          |         0|          1.00|   67.01|  5.98|   42.98|   64.04|   69.08|   71.06|   78.08|▁▁▂▇▃ |
|humid         |         0|          1.00|   66.90| 16.74|   24.46|   53.18|   66.93|   81.63|  100.00|▁▆▇▇▅ |
|wind_dir      |        46|          0.98|  191.19| 95.11|    0.00|  150.00|  210.00|  250.00|  360.00|▅▂▇▇▃ |
|wind_speed    |         2|          1.00|    9.58|  4.06|    0.00|    6.90|    9.21|   12.66|   25.32|▂▇▇▁▁ |
|wind_gust     |      1975|          0.11|   21.40|  4.26|   16.11|   18.41|   20.71|   23.02|   66.75|▇▁▁▁▁ |
|precip        |         0|          1.00|    0.00|  0.04|    0.00|    0.00|    0.00|    0.00|    0.94|▇▁▁▁▁ |
|pressure      |       264|          0.88| 1016.65|  5.11| 1000.70| 1014.00| 1017.00| 1020.60| 1027.20|▁▂▆▇▃ |
|visib         |         0|          1.00|    9.59|  1.34|    0.50|   10.00|   10.00|   10.00|   10.00|▁▁▁▁▇ |


**Variable type: POSIXct**

|skim_variable | n_missing| complete_rate|min        |max                 |median              | n_unique|
|:-------------|---------:|-------------:|:----------|:-------------------|:-------------------|--------:|
|time_hour     |         0|             1|2013-07-01 |2013-07-31 23:00:00 |2013-07-16 11:30:00 |      744|

```r
# Further check the wind speed outliers. Hypothesis - wind speed of 0 is actually a missed data point
weather_july_2013 %>% 
  filter(wind_speed == 0) %>% 
  summarize(count = n())
```

```
## # A tibble: 1 × 1
##   count
##   <int>
## 1    79
```

```r
# Draw a scatterplot to infer relationship between dew point and humidity
ggplot(weather, aes(x = dewp, y = humid)) +
  geom_point()
```

```
## Warning: Removed 1 rows containing missing values (`geom_point()`).
```

<img src="/blogs/Flights_NYC_files/figure-html/unnamed-chunk-5-1.png" width="672" />

```r
# Draw a scatterplot to infer relationship between precipitation level and visibility
ggplot(weather, aes(x = precip, y = visib)) +
  geom_point()
```

<img src="/blogs/Flights_NYC_files/figure-html/unnamed-chunk-5-2.png" width="672" />

```r
# Draw a scatterplot to infer relationship between precipitation level and visibility for July 2013 only
ggplot(weather_july_2013, aes(x = precip, y = visib)) +
  geom_point()
```

<img src="/blogs/Flights_NYC_files/figure-html/unnamed-chunk-5-3.png" width="672" />


**Temperature in July 2013 has a mean of 80 degrees Fahrenheit and a standard deviation of 7.1**. It also **seems to be skewed to the right**, with median (79 degrees) being less than mean, and 75% percentile and maximum value farther from median than 25% percentile and minimum value respectively.

**Wind speed data seems to be incomplete in July 2013, with 2 missing points and as much as 79 points with wind speed of exactly 0** (unlikely result, looks more like lack of data than true case of 0 speed).

The scatter plot for the (dewp, humid) looks quite cumbersome, but from the shape **we can infer a positive correlation - the higher the dew point, the higher the humidity.** We believe these are related concepts (but not so sure on the definitions), so the correlation is expected.

The **precipitation-visibility** data shows no clear pattern on individual observations across years, and July 2013 data points to **slightly positive correlation**. This is **counterintuitive**, as we would expect rain and snow to reduce distance at which objects are visible.

## Problem 5: Use the `flights` and `planes` tables to answer the following questions:

    -   How many planes have a missing date of manufacture?
    -   What are the five most common manufacturers?
    -   Has the distribution of manufacturer changed over time as reflected by the airplanes flying from NYC in 2013? (Hint: you may need to use case_when() to recode the manufacturer name and collapse rare vendors into a category called Other.)



```r
head(planes)
```

```
## # A tibble: 6 × 9
##   tailnum  year type               manufacturer model engines seats speed engine
##   <chr>   <int> <chr>              <chr>        <chr>   <int> <int> <int> <chr> 
## 1 N10156   2004 Fixed wing multi … EMBRAER      EMB-…       2    55    NA Turbo…
## 2 N102UW   1998 Fixed wing multi … AIRBUS INDU… A320…       2   182    NA Turbo…
## 3 N103US   1999 Fixed wing multi … AIRBUS INDU… A320…       2   182    NA Turbo…
## 4 N104UW   1999 Fixed wing multi … AIRBUS INDU… A320…       2   182    NA Turbo…
## 5 N10575   2002 Fixed wing multi … EMBRAER      EMB-…       2    55    NA Turbo…
## 6 N105UW   1999 Fixed wing multi … AIRBUS INDU… A320…       2   182    NA Turbo…
```

```r
# Get a dataframe for which year of manufacture is unknown
planes %>% 
  filter(is.na(year))
```

```
## # A tibble: 70 × 9
##    tailnum  year type              manufacturer model engines seats speed engine
##    <chr>   <int> <chr>             <chr>        <chr>   <int> <int> <int> <chr> 
##  1 N14558     NA Fixed wing multi… EMBRAER      EMB-…       2    55    NA Turbo…
##  2 N15555     NA Fixed wing multi… EMBRAER      EMB-…       2    55    NA Turbo…
##  3 N15574     NA Fixed wing multi… EMBRAER      EMB-…       2    55    NA Turbo…
##  4 N174US     NA Fixed wing multi… AIRBUS INDU… A321…       2   199    NA Turbo…
##  5 N177US     NA Fixed wing multi… AIRBUS INDU… A321…       2   199    NA Turbo…
##  6 N181UW     NA Fixed wing multi… AIRBUS INDU… A321…       2   199    NA Turbo…
##  7 N18557     NA Fixed wing multi… EMBRAER      EMB-…       2    55    NA Turbo…
##  8 N194UW     NA Fixed wing multi… AIRBUS       A321…       2   199    NA Turbo…
##  9 N238JB     NA Fixed wing multi… EMBRAER      ERJ …       2    20    NA Turbo…
## 10 N271LV     NA Fixed wing multi… BOEING       737-…       2   149    NA Turbo…
## # ℹ 60 more rows
```

```r
# Basic dataframe of manufacturers and number of planes
planes_number <- planes %>% 
  group_by(manufacturer) %>% 
  summarize(count = n()) %>% 
  arrange(desc(count))

# Take a look at the result
planes_number
```

```
## # A tibble: 35 × 2
##    manufacturer                  count
##    <chr>                         <int>
##  1 BOEING                         1630
##  2 AIRBUS INDUSTRIE                400
##  3 BOMBARDIER INC                  368
##  4 AIRBUS                          336
##  5 EMBRAER                         299
##  6 MCDONNELL DOUGLAS               120
##  7 MCDONNELL DOUGLAS AIRCRAFT CO   103
##  8 MCDONNELL DOUGLAS CORPORATION    14
##  9 CANADAIR                          9
## 10 CESSNA                            9
## # ℹ 25 more rows
```

```r
# Create a new dataset with manufactureres uniformly named. Not popular names are grouped into the "OTHER" category
planes_renamed_manufacturers <- planes %>% 
  mutate(
   manufacturer = case_when(
     manufacturer == "BOEING" ~ "BOEING",
     manufacturer %in%  c("AIRBUS INDUSTRIE", "AIRBUS") ~ "AIRBUS",
     manufacturer %in% c("MCDONNELL DOUGLAS","MCDONNELL DOUGLAS AIRCRAFT CO","MCDONNELL DOUGLAS CORPORATION") ~ "MCDONNELL DOUGLAS",
     manufacturer == "BOMBARDIER INC" ~ "BOMBARDIER INC",
     manufacturer == "EMBRAER" ~ "EMBRAER",
     TRUE  ~ "OTHER"
   ) 
  )

# Precise dataframe of manufacturers (using uniform naming) and number of planes
planes_precise_number <- planes_renamed_manufacturers %>% 
  group_by(manufacturer) %>% 
  summarize(count = n()) %>% 
  arrange(desc(count))

# Take a look at the result
planes_precise_number
```

```
## # A tibble: 6 × 2
##   manufacturer      count
##   <chr>             <int>
## 1 BOEING             1630
## 2 AIRBUS              736
## 3 BOMBARDIER INC      368
## 4 EMBRAER             299
## 5 MCDONNELL DOUGLAS   237
## 6 OTHER                52
```

```r
# Attempt to store distinct planes that flew in 2013 as a list
distinct_flights <- flights %>% 
  filter(year == 2013) %>%
  distinct(tailnum) %>%
  select(tailnum)

# Attempt to recreate the analysis, adding the filter on unique planes that flew in 2013
(
planes_precise_number_2013 <- planes_renamed_manufacturers %>%
  filter(tailnum %in% c(distinct_flights)) %>% 
  group_by(manufacturer) %>% 
  summarize(count = n()) %>% 
  arrange(desc(count))
)
```

```
## # A tibble: 0 × 2
## # ℹ 2 variables: manufacturer <chr>, count <int>
```


Table *planes* only contains information about year of manufacture. Applying the NA filter, we find that 70 planes have unknown year of manufacture.

The list of five most common manufacturer is provided below. Boeing tops the list with 1630 planes

| Manufacturer     | Number of planes |
|------------------|------------------|
| BOEING           | 1630             |
| AIRBUS INDUSTRIE | 400              |
| BOMBARDIER INC   | 368              |
| AIRBUS           | 336              |
| EMBRAER          | 299              |

: Common manufacturers

We need to be aware, however, that grouping by might not recognize same manufacturer under different names (e.g. "AIRBUS INDUSTRIE" is treated separate from "AIRBUS"). To take this into account, manufacturer names in the dataset must be amended to be uniform. The hint on "case_when" might also be useful.

Indeed, applying the case_when and grouping all manufactures with less than 10 planes into the "OTHER" category, we get the top-5 manufacturers:

| Manufacturer      | Number of planes |
|-------------------|------------------|
| BOEING            | 1630             |
| AIRBUS            | 736              |
| BOMBARDIER INC    | 368              |
| EMBRAER           | 299              |
| MCDONNELL DOUGLAS | 237              |

Others total in 52 planes

The general idea to understand changes in 2013 is the following:

1.  Find and save a distinct list of unique planes that flew in 2013 (tailnum from flights table)
2.  Use this list as an input to %in% filter for the planes_renamed_manufacturers table
3.  Group the dataframe by manufacturer, summarize (count) and arrange in descending order

However, tibble from point 1 (list of unique planes) does not serve as a filter input well, and we don't know how to actually save variable as a list (vector)

## Problem 6: Use the `flights` and `planes` tables to answer the following questions:

    -   What is the oldest plane (specified by the tailnum variable) that flew from New York City airports in 2013?
    -   How many airplanes that flew from New York City are included in the planes table?



```r
# mutate planes table to have a uniquely named column for year of manufacture
planes_1 <- planes %>% 
  mutate(year_manufactured = year)

# mutate planes table to have a uniquely named column for year of flight
flights_1 <- flights %>% 
  mutate(year_flight = year)

# join the two tables to have a dataframe with both year of manufacture (to sort) and year of flight (to filter)
# We want to preserve flight data, hence we use left join
flights_planes <- left_join(x = flights_1, y = planes_1, by = "tailnum")

# Filtering for planes with known year of manufacture that flew in 2013, arranging by year of manufacture
fights_planes_2013 <- flights_planes %>% 
  drop_na(year_manufactured) %>% 
  filter(year_flight == 2013) %>% 
  arrange(year_manufactured)

# Printing the row for top 1 (the oldest plane)
head(fights_planes_2013,1)
```

```
## # A tibble: 1 × 29
##   year.x month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
##    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
## 1   2013     1    30      741            745        -4     1059           1125
## # ℹ 21 more variables: arr_delay <dbl>, carrier <chr>, flight <int>,
## #   tailnum <chr>, origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>,
## #   hour <dbl>, minute <dbl>, time_hour <dttm>, year_flight <int>,
## #   year.y <int>, type <chr>, manufacturer <chr>, model <chr>, engines <int>,
## #   seats <int>, speed <int>, engine <chr>, year_manufactured <int>
```

```r
# Creating a new dataframe that contains only those planes from planes table that are also listed in flights table
flights_planes_semi_joined <- semi_join(x = planes, y = flights, by = "tailnum")

# Count number of planes in <potentially> reduced data. Planes table already has distinct values for planes
count(flights_planes_semi_joined)
```

```
## # A tibble: 1 × 1
##       n
##   <int>
## 1  3322
```

```r
# Compare to number of planes in original (not reduced) data
count(planes)
```

```
## # A tibble: 1 × 1
##       n
##   <int>
## 1  3322
```


N381AA is the oldest plane (manufactured in 1956) that flew from NYC in 2013. Technically, it might not be the only plane that was manufactured in 2013 (ordering does not indicate distinct values), but there is definitely no older plane.

3322 is the number of planes that flew from NYC and are included in the planes table (we used semi_join to reduce the planes table). However, it is precisely the same number that the whole planes table has - meaning that planes table is made of planes that flew from NYC.

## Problem 7: Use the `nycflights13` to answer the following questions:

    -   What is the median arrival delay on a month-by-month basis in each airport?
    -   For each airline, plot the median arrival delay for each month and origin airport.



```r
# Way 1 - save a dataframe grouped by origin and month
flights_by_month <- flights %>% 
  group_by(origin, month)

# Way 1 - save the dataframe with summarized valued for median
flights_median <- flights_by_month %>% 
  summarize(median_arr_delay = median(arr_delay))
```

```
## `summarise()` has grouped output by 'origin'. You can override using the
## `.groups` argument.
```

```r
# Way 1 - try to build faceted scatterplot
ggplot(flights_median, aes(x = month, y = median_arr_delay)) +
geom_point() +
facet_wrap(~ origin)
```

```
## Warning: Removed 36 rows containing missing values (`geom_point()`).
```

<img src="/blogs/Flights_NYC_files/figure-html/unnamed-chunk-8-1.png" width="672" />

```r
# Way 2 - do the grouping, summarizing and building a graph in one piece of code
flights %>% 
  group_by(origin, month) %>% 
  summarize(median_arr_delay = median(arr_delay)) %>% 
  ggplot() +
  aes(x = month, y = median_arr_delay) +
  geom_point() +
  facet_wrap(~ origin)
```

```
## `summarise()` has grouped output by 'origin'. You can override using the
## `.groups` argument.
```

```
## Warning: Removed 36 rows containing missing values (`geom_point()`).
```

<img src="/blogs/Flights_NYC_files/figure-html/unnamed-chunk-8-2.png" width="672" />


For some reason, R does not calculate the median for arr_delay variable in summarize section. I have used multiple ways to get to the result, but the problem seems to be narrowed down to non-calculating median value.

## Problem 8: Let's take a closer look at what carriers service the route to San Francisco International (SFO). Join the `flights` and `airlines` tables and count which airlines flew the most to SFO. Produce a new dataframe, `fly_into_sfo` that contains three variables: the `name` of the airline, e.g., `United Air Lines Inc.` not `UA`, the count (number) of times it flew to SFO, and the `percent` of the trips that that particular airline flew to SFO.



```r
# Join the two tables to enrich flights data with airlines data
# We want to preserve flights data, hence left join
flights_enriched <- left_join(x = flights, y = airlines, by = "carrier")

# Take a look at data
flights_enriched
```

```
## # A tibble: 336,776 × 20
##     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
##    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
##  1  2013     1     1      517            515         2      830            819
##  2  2013     1     1      533            529         4      850            830
##  3  2013     1     1      542            540         2      923            850
##  4  2013     1     1      544            545        -1     1004           1022
##  5  2013     1     1      554            600        -6      812            837
##  6  2013     1     1      554            558        -4      740            728
##  7  2013     1     1      555            600        -5      913            854
##  8  2013     1     1      557            600        -3      709            723
##  9  2013     1     1      557            600        -3      838            846
## 10  2013     1     1      558            600        -2      753            745
## # ℹ 336,766 more rows
## # ℹ 12 more variables: arr_delay <dbl>, carrier <chr>, flight <int>,
## #   tailnum <chr>, origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>,
## #   hour <dbl>, minute <dbl>, time_hour <dttm>, name <chr>
```

```r
# Interim table to count flights to SFO only by airline
fly_into_sfo_only <- flights_enriched %>% 
  filter(dest == "SFO") %>%
  group_by(name) %>% 
  summarize(flights_to_sfo = n()) 

# Interim table to count total flights by airline
fly_total <- flights_enriched %>% 
  group_by(name) %>% 
  summarize(flights_total = n())

# Join two interim tables to have total flights and flights to SFO in one dataframe
fly_into_sfo <- left_join(y = fly_total, x = fly_into_sfo_only, by = "name")

# Create a percent variable as ratio of flights to SFO to total flights, arrange from highest to lowest number of flights
fly_into_sfo %>% 
  mutate(percent = round((flights_to_sfo/flights_total)*100,1)) %>% 
  arrange(desc(flights_to_sfo))
```

```
## # A tibble: 5 × 4
##   name                   flights_to_sfo flights_total percent
##   <chr>                           <int>         <int>   <dbl>
## 1 United Air Lines Inc.            6819         58665    11.6
## 2 Virgin America                   2197          5162    42.6
## 3 Delta Air Lines Inc.             1858         48110     3.9
## 4 American Airlines Inc.           1422         32729     4.3
## 5 JetBlue Airways                  1035         54635     1.9
```


Only 5 carriers fly to SFO, with United Air Lines Inc. making most flights (6819), but Virgin America focusing on San Francisco destination most (42.6% of its flights).



```r
#fly_into_sfo %>% 
  
  # sort 'name' of airline by the numbers it times to flew to SFO
#  mutate(name = fct_reorder(name, count)) %>% 
  
 # ggplot() +
  
#  aes(x = count, 
 #     y = name) +
  
  # a simple bar/column plot
#  geom_col() +
  
  # add labels, so each bar shows the % of total flights 
#  geom_text(aes(label = percent),
 #            hjust = 1, 
  #           colour = "white", 
   #          size = 5)+
  
  # add labels to help our audience  
#  labs(title="Which airline dominates the NYC to SFO route?", 
 #      subtitle = "as % of total flights in 2013",
  #     x= "Number of flights",
   #    y= NULL) +
  
#  theme_minimal() + 
  
  # change the theme-- i just googled those , but you can use the ggThemeAssist add-in
  # https://cran.r-project.org/web/packages/ggThemeAssist/index.html
  
 # theme(#
    # so title is left-aligned
  #  plot.title.position = "plot",
    
    # text in axes appears larger        
   # axis.text = element_text(size=12),
    
    # title text is bigger
#    plot.title = element_text(size=18)
 #     ) +

  # add one final layer of NULL, so if you comment out any lines
  # you never end up with a hanging `+` that awaits another ggplot layer
#  NULL
```


## Problem 9: Let's take a look at cancellations of flights to SFO. We create a new dataframe `cancellations` as follows



```r
cancellations <- flights %>% 
  
  # just filter for destination == 'SFO'
  filter(dest == 'SFO') %>% 
  
  # a cancelled flight is one with no `dep_time` 
  filter(is.na(dep_time))
```


*I want you to think how we would organise our data manipulation to create the following plot. No need to write the code, just explain in words how you would go about it.*

I believe that the graph is a bar chart on absolute number (not percentage) of cancellations by month, faceted by carrier (vertically) and airport of origin (horizontally). To build this graph, we would need the following:

1.  Filter for only "SFO" airport in "dest" variable to get only flights to San Francisco
2.  Filter for only NA values in dep_time to get only cancelled flights
3.  Group by carrier, origin (airport of origin) and month
4.  Summarize (count) number of cancelled flights in each group with n()
5.  Plot the bar chart with x = months and y = count
6.  Facet graphs by carrier and origin
7.  Another feature of graph is label the value in each bar - probably, some additional method in ggplot2 library.

![](images/sfo-cancellations.png)

