---
categories:
- ""
- ""
date: "2017-10-31T21:28:43-05:00"
description: ""
draft: false
image: pic10.jpg
keywords: ""
slug: ipsum
title: Ipsum
---

# Data Manipulation

## Problem 1: Use logical operators to find flights that:

\# For problem 1, I will be using the filter function to select which variables I want
 glimpse(flights)

Rows: 336,776
 Columns: 19
 $ year      <int> 2013, 2013, 2013, 2013, 2013, 2013, 2013, 2013, 2013, 2…
 $ month     <int> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1…
 $ day      <int> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1…
 $ dep_time    <int> 517, 533, 542, 544, 554, 554, 555, 557, 557, 558, 558, …
 $ sched_dep_time <int> 515, 529, 540, 545, 600, 558, 600, 600, 600, 600, 600, …
 $ dep_delay   <dbl> 2, 4, 2, -1, -6, -4, -5, -3, -3, -2, -2, -2, -2, -2, -1…
 $ arr_time    <int> 830, 850, 923, 1004, 812, 740, 913, 709, 838, 753, 849,…
 $ sched_arr_time <int> 819, 830, 850, 1022, 837, 728, 854, 723, 846, 745, 851,…
 $ arr_delay   <dbl> 11, 20, 33, -18, -25, 12, 19, -14, -8, 8, -2, -3, 7, -1…
 $ carrier    <chr> "UA", "UA", "AA", "B6", "DL", "UA", "B6", "EV", "B6", "…
 $ flight     <int> 1545, 1714, 1141, 725, 461, 1696, 507, 5708, 79, 301, 4…
 $ tailnum    <chr> "N14228", "N24211", "N619AA", "N804JB", "N668DN", "N394…
 $ origin     <chr> "EWR", "LGA", "JFK", "JFK", "LGA", "EWR", "EWR", "LGA",…
 $ dest      <chr> "IAH", "IAH", "MIA", "BQN", "ATL", "ORD", "FLL", "IAD",…
 $ air_time    <dbl> 227, 227, 160, 183, 116, 150, 158, 53, 140, 138, 149, 1…
 $ distance    <dbl> 1400, 1416, 1089, 1576, 762, 719, 1065, 229, 944, 733, …
 $ hour      <dbl> 5, 5, 5, 5, 6, 5, 6, 6, 6, 6, 6, 6, 6, 6, 6, 5, 6, 6, 6…
 $ minute     <dbl> 15, 29, 40, 45, 0, 58, 0, 0, 0, 0, 0, 0, 0, 0, 0, 59, 0…
 $ time_hour   <dttm> 2013-01-01 05:00:00, 2013-01-01 05:00:00, 2013-01-01 0…

\# Had an arrival delay of two or more hours (> 120 minutes)
 delay_2hr <- flights %>% 
  filter(arr_delay>=120)
 print(delay_2hr)

\# A tibble: 10,200 × 19
   year month  day dep_time sched_dep_time dep_delay arr_time sched_arr_time
  <int> <int> <int>  <int>     <int>   <dbl>  <int>     <int>
 1 2013   1   1   811      630    101   1047      830
 2 2013   1   1   848      1835    853   1001      1950
 3 2013   1   1   957      733    144   1056      853
 4 2013   1   1   1114      900    134   1447      1222
 5 2013   1   1   1505      1310    115   1638      1431
 6 2013   1   1   1525      1340    105   1831      1626
 7 2013   1   1   1549      1445    64   1912      1656
 8 2013   1   1   1558      1359    119   1718      1515
 9 2013   1   1   1732      1630    62   2028      1825
 10 2013   1   1   1803      1620    103   2008      1750
 \# ℹ 10,190 more rows
 \# ℹ 11 more variables: arr_delay <dbl>, carrier <chr>, flight <int>,
 \#  tailnum <chr>, origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>,
 \#  hour <dbl>, minute <dbl>, time_hour <dttm>

\# Flew to Houston (IAH or HOU)
 dest_IAH_HOU <- flights %>% 
  filter(dest=="IAH"|dest=="HOU")
 print(dest_IAH_HOU)

\# A tibble: 9,313 × 19
   year month  day dep_time sched_dep_time dep_delay arr_time sched_arr_time
  <int> <int> <int>  <int>     <int>   <dbl>  <int>     <int>
 1 2013   1   1   517      515     2   830      819
 2 2013   1   1   533      529     4   850      830
 3 2013   1   1   623      627    -4   933      932
 4 2013   1   1   728      732    -4   1041      1038
 5 2013   1   1   739      739     0   1104      1038
 6 2013   1   1   908      908     0   1228      1219
 7 2013   1   1   1028      1026     2   1350      1339
 8 2013   1   1   1044      1045    -1   1352      1351
 9 2013   1   1   1114      900    134   1447      1222
 10 2013   1   1   1205      1200     5   1503      1505
 \# ℹ 9,303 more rows
 \# ℹ 11 more variables: arr_delay <dbl>, carrier <chr>, flight <int>,
 \#  tailnum <chr>, origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>,
 \#  hour <dbl>, minute <dbl>, time_hour <dttm>

\# we can also do filter(dest %in% c("IAH", "HOU"))
 
 \# Were operated by United (`UA`), American (`AA`), or Delta (`DL`)
 UA_AA_DL <- flights %>% 
  filter(carrier=="UA"| carrier=="AA"| carrier=="DL")
 print(UA_AA_DL)

\# A tibble: 139,504 × 19
   year month  day dep_time sched_dep_time dep_delay arr_time sched_arr_time
  <int> <int> <int>  <int>     <int>   <dbl>  <int>     <int>
 1 2013   1   1   517      515     2   830      819
 2 2013   1   1   533      529     4   850      830
 3 2013   1   1   542      540     2   923      850
 4 2013   1   1   554      600    -6   812      837
 5 2013   1   1   554      558    -4   740      728
 6 2013   1   1   558      600    -2   753      745
 7 2013   1   1   558      600    -2   924      917
 8 2013   1   1    558      600    -2   923      937
 9 2013   1   1   559      600    -1   941      910
 10 2013   1   1   559      600    -1   854      902
 \# ℹ 139,494 more rows
 \# ℹ 11 more variables: arr_delay <dbl>, carrier <chr>, flight <int>,
 \#  tailnum <chr>, origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>,
 \#  hour <dbl>, minute <dbl>, time_hour <dttm>

\# Departed in summer (July, August, and September)
 summer_dep <- flights %>% 
  filter(month=="7"| month=="8"| month=="9")
 print(summer_dep)

\# A tibble: 86,326 × 19
   year month  day dep_time sched_dep_time dep_delay arr_time sched_arr_time
  <int> <int> <int>  <int>     <int>   <dbl>  <int>     <int>
 1 2013   7   1    1      2029    212   236      2359
 2 2013   7   1    2      2359     3   344      344
 3 2013   7   1    29      2245    104   151       1
 4 2013   7   1    43      2130    193   322       14
 5 2013   7   1    44      2150    174   300      100
 6 2013   7   1    46      2051    235   304      2358
 7 2013   7   1    48      2001    287   308      2305
 8 2013   7   1    58      2155    183   335       43
 9 2013   7   1   100      2146    194   327       30
 10 2013   7   1   100      2245    135   337      135
 \# ℹ 86,316 more rows
 \# ℹ 11 more variables: arr_delay <dbl>, carrier <chr>, flight <int>,
 \#  tailnum <chr>, origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>,
 \#  hour <dbl>, minute <dbl>, time_hour <dttm>

\# Arrived more than two hours late, but didn't leave late
 arr_only_delay <-flights %>% 
  filter(arr_delay>=120 & dep_delay<=0)
 print(arr_only_delay)

\# A tibble: 29 × 19
   year month  day dep_time sched_dep_time dep_delay arr_time sched_arr_time
  <int> <int> <int>  <int>     <int>   <dbl>  <int>     <int>
 1 2013   1  27   1419      1420    -1   1754      1550
 2 2013  10   7   1350      1350     0   1736      1526
 3 2013  10   7   1357      1359    -2   1858      1654
 4 2013  10  16   657      700    -3   1258      1056
 5 2013  11   1   658      700    -2   1329      1015
 6 2013   3  18   1844      1847    -3    39      2219
 7 2013   4  17   1635      1640    -5   2049      1845
 8 2013   4  18   558      600    -2   1149      850
 9 2013   4  18   655      700    -5   1213      950
 10 2013   5  22   1827      1830    -3   2217      2010
 \# ℹ 19 more rows
 \# ℹ 11 more variables: arr_delay <dbl>, carrier <chr>, flight <int>,
 \#  tailnum <chr>, origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>,
 \#  hour <dbl>, minute <dbl>, time_hour <dttm>

\# Were delayed by at least an hour, but made up over 30 minutes in flight
 del_made_up <- flights %>% 
  filter(dep_delay>=60 & arr_delay<=60)
 print(del_made_up)

\# A tibble: 3,969 × 19
   year month  day dep_time sched_dep_time dep_delay arr_time sched_arr_time
  <int> <int> <int>  <int>     <int>   <dbl>  <int>     <int>
 1 2013   1   1   826      715    71   1136      1045
 2 2013   1   1   1628      1524    64   1740      1641
 3 2013   1   1   1846      1745    61   2147      2055
 4 2013   1   1   2302      2200    62   2342      2253
 5 2013   1   2   1125      1020    65   1309      1223
 6 2013   1   2   1345      1240    65   1642      1555
 7 2013   1   2   1421      1314    67   1515      1415
 8 2013   1   2   1618      1516    62   1913      1825
 9 2013   1   2   1801      1655    66   1932      1843
 10 2013   1   2   2108      1954    74   2218      2119
 \# ℹ 3,959 more rows
 \# ℹ 11 more variables: arr_delay <dbl>, carrier <chr>, flight <int>,
 \#  tailnum <chr>, origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>,
 \#  hour <dbl>, minute <dbl>, time_hour <dttm>



## Problem 2: What months had the highest and lowest proportion of cancelled flights? Interpret any seasonal patterns. To determine if a flight was cancelled use the following code

flights %>% 
  filter(is.na(dep_time))

\# What months had the highest and lowest % of cancelled flights?
 
 \# I wil group the data by the month variable and then use the summarise function to to find out the mean percentage of cancelled flights per month.
 cancelled_by_month<- flights %>% 
  group_by(month) %>%
  summarise(cancelled_pct = mean(is.na(dep_time)) * 100)
 
 print(cancelled_by_month)

\# A tibble: 12 × 2
  month cancelled_pct
  <int>     <dbl>
 1   1     1.93 
 2   2     5.05 
 3   3     2.99 
 4   4     2.36 
 5   5     1.96 
 6   6     3.57 
 7   7     3.19 
 8   8     1.66 
 9   9     1.64 
 10  10     0.817
 11  11     0.854
 12  12     3.64 

\# Find the month with the highest percentage of cancelled flights
 
 \# I am filtering the percentages of cancelled flights and selecting the the month with the highest percentage
 highest_cancelled_month <- cancelled_by_month %>%
  filter(cancelled_pct == max(cancelled_pct)) %>%
  pull(month)
 
 print(highest_cancelled_month)

[1] 2

\# Find the month with the lowest percentage of cancelled flights
 
 \# I am filtering the percentages of cancelled flights and selecting the the month with the lowest percentage
 lowest_cancelled_month <- cancelled_by_month %>%
  filter(cancelled_pct == min(cancelled_pct)) %>%
  pull(month)
 
 print(lowest_cancelled_month)

[1] 10



## Problem 3: What plane (specified by the tailnum variable) traveled the most times from New York City airports in 2013? Please left_join() the resulting table with the table planes (also included in the nycflights13 package).

For the plane with the greatest number of flights and that had more than 50 seats, please create a table where it flew to during 2013.

\# I will filter for the year 2013, the NYC airports and the tail number, using the !is.na() command to avoid an empty table givien that there are some missing values. I will then group by the tailnumber and use the summarise function to create a table with the number of flights per tailnumber.
 flight_counts <- flights %>%
  filter(year == 2013) %>%
  filter(origin %in% c("JFK", "LGA", "EWR")) %>%
  filter(!is.na(tailnum)) %>% 
  group_by(tailnum) %>%
  summarise(flight_count = n())
 
 print(flight_counts)

\# A tibble: 4,043 × 2
  tailnum flight_count
  <chr>     <int>
 1 D942DN       4
 2 N0EGMQ      371
 3 N10156      153
 4 N102UW      48
 5 N103US      46
 6 N104UW      47
 7 N10575      289
 8 N105UW      45
 9 N107US      41
 10 N108UW      60
 \# ℹ 4,033 more rows

\# I am arranging the previously created table in descending order and using the slice() command to give me the tailnumber with the highest count of flights.
 most_flights <- flight_counts %>%
  arrange(desc(flight_count)) %>%
  slice(1)
 
 print(most_flights)

\# A tibble: 1 × 2
  tailnum flight_count
  <chr>     <int>
 1 N725MQ      575

most_flown_plane <- most_flights$tailnum
 
 print(most_flown_plane)

[1] "N725MQ"

\# I am left joining the the flight counts table with the planes table by the variable they have in common (tailnum), and then arranging it in descending order.
 joining_planes_flights <- left_join(flight_counts,
           planes, 
           by = "tailnum") %>%
  arrange(desc(flight_count))
 print(joining_planes_flights)

\# A tibble: 4,043 × 10
  tailnum flight_count year type    manufacturer model engines seats speed
  <chr>     <int> <int> <chr>    <chr>    <chr>  <int> <int> <int>
 1 N725MQ      575  NA <NA>    <NA>     <NA>    NA  NA  NA
 2 N722MQ      513  NA <NA>    <NA>     <NA>    NA  NA  NA
 3 N723MQ      507  NA <NA>    <NA>     <NA>    NA  NA  NA
 4 N711MQ      486 1976 Fixed wing… GULFSTREAM … G115…    2  22  NA
 5 N713MQ      483  NA <NA>    <NA>     <NA>    NA  NA  NA
 6 N258JB      427 2006 Fixed wing… EMBRAER   ERJ …    2  20  NA
 7 N298JB      407 2009 Fixed wing… EMBRAER   ERJ …    2  20  NA
 8 N353JB      404 2012 Fixed wing… EMBRAER   ERJ …    2  20  NA
 9 N351JB      402 2012 Fixed wing… EMBRAER   ERJ …    2  20  NA
 10 N735MQ      396  NA <NA>    <NA>     <NA>    NA  NA  NA
 \# ℹ 4,033 more rows
 \# ℹ 1 more variable: engine <chr>

\# To find out where the plane with the greatest number of flights and that had more than 50 seats flew to during 2013 I am first filtering for the year 2014, NYC airports of origin and tailnumber, using is.na() to deal with the missing values. I am leftjoining this data with the planes table by the variable they have in common, tailnum.
 flights_planes <- flights %>%
  filter(year == 2013, 
     origin %in% c("JFK", "LGA", "EWR")) %>%
  filter(!is.na(tailnum)) %>%
  left_join(planes, by = "tailnum")
 
 \# Then I am filtering for the planes which have more tham 50 seats, grouping them by tailnumber and creating a table with their flight counts. I arrange it in descending order and select the tailnumber with the highest count (using the slice(1) command.)
 most_flights_over_50_seats <- flights_planes %>%
  filter(seats > 50) %>%
  group_by(tailnum) %>%
  summarise(flight_count = n()) %>%
  arrange(desc(flight_count)) %>%
  slice(1)
 
 print(most_flights_over_50_seats)

\# A tibble: 1 × 2
  tailnum flight_count
  <chr>     <int>
 1 N328AA      393

\# Now, get the destinations for this plane
 most_flown_plane_over_50_seats <- most_flights_over_50_seats$tailnum[1]
 
 \# I am using the leftjoined flights_planes table to filter out for the previously found most flown plane with over 50 seats. I then select the dest variable to get the plane's destinations and use the unique() command to avoid repetitions.
 destinations <- flights_planes %>%
  filter(tailnum == most_flown_plane_over_50_seats) %>%
  select(dest) %>%
  unique()
 
 print(destinations)

\# A tibble: 6 × 1
  dest 
  <chr>
 1 LAX 
 2 SFO 
 3 SJU 
 4 MIA 
 5 MCO 
 6 BOS 



## Problem 4: The nycflights13 package includes a table (weather) that describes the weather during 2013. Use that table to answer the following questions:

glimpse(weather)

Rows: 26,115
 Columns: 15
 $ origin   <chr> "EWR", "EWR", "EWR", "EWR", "EWR", "EWR", "EWR", "EWR", "EW…
 $ year    <int> 2013, 2013, 2013, 2013, 2013, 2013, 2013, 2013, 2013, 2013,…
 $ month   <int> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1,…
 $ day    <int> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1,…
 $ hour    <int> 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 13, 14, 15, 16, 17, 18, …
 $ temp    <dbl> 39.02, 39.02, 39.02, 39.92, 39.02, 37.94, 39.02, 39.92, 39.…
 $ dewp    <dbl> 26.06, 26.96, 28.04, 28.04, 28.04, 28.04, 28.04, 28.04, 28.…
 $ humid   <dbl> 59.37, 61.63, 64.43, 62.21, 64.43, 67.21, 64.43, 62.21, 62.…
 $ wind_dir  <dbl> 270, 250, 240, 250, 260, 240, 240, 250, 260, 260, 260, 330,…
 $ wind_speed <dbl> 10.35702, 8.05546, 11.50780, 12.65858, 12.65858, 11.50780, …
 $ wind_gust <dbl> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, 20.…
 $ precip   <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,…
 $ pressure  <dbl> 1012.0, 1012.3, 1012.5, 1012.2, 1011.9, 1012.4, 1012.2, 101…
 $ visib   <dbl> 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10,…
 $ time_hour <dttm> 2013-01-01 01:00:00, 2013-01-01 02:00:00, 2013-01-01 03:00…

\# What is the distribution of temperature (`temp`) in July 2013? Identify any important outliers in terms of the `wind_speed` variable.
 
 \# I first filter for the month of July.
 july_weather <- weather %>%
  filter(month == 7) 
 
 \# Histogram of temperature
 \# I am creating a histogram to find out the distribution, making the x axis the temperature. 
 ggplot(july_weather, aes(x = temp)) +
  geom_histogram(binwidth = 1, fill = "blue", color = "black") +
  theme_minimal() +
  labs(title = "The temperature in July 2013 has a normal distribution, \n slightly right skewed", 
    x = "Temperature", 
    y = "Frequency")

![img](file:///C:/Users/c14cc/AppData/Local/Temp/msohtmlclip1/01/clip_image001.png)

\# The histogram shows a normal distribution with a mean around 76, skewed to the right.
 
 \# Boxplot for outliers in wind_speed
 \# I am creating a boxplot to find out the outliers, making the y axis the wind speed.
 ggplot(july_weather, aes(y = wind_speed)) +
  geom_boxplot(fill = "blue", color = "black") +
  theme_minimal() +
  labs(title = "There are 3 wind speed outliers in July 2013, \n between the values of 20 and 26",
    y = "Wind Speed")

Warning: Removed 2 rows containing non-finite values (`stat_boxplot()`).

![img](file:///C:/Users/c14cc/AppData/Local/Temp/msohtmlclip1/01/clip_image002.png)

\# What is the relationship between `dewp` and `humid`?
 \# I am creating a dotplot with the variable dewp in the x axis and humid in the y axis to determine whether they are correlated.
 ggplot(weather, aes(x = dewp, y = humid)) +
  geom_point(alpha = 0.1) +
  theme_minimal() +
  labs(x = "Dew Point (°F)", y = "Humidity (%)",
    title = "There is a positive relationship between \n Dew Point and Humidity, as they increase together")

Warning: Removed 1 rows containing missing values (`geom_point()`).

![img](file:///C:/Users/c14cc/AppData/Local/Temp/msohtmlclip1/01/clip_image003.png)

\# What is the relationship between `precip` and `visib`?
 \# I am creating a dotplot with the variable precip in the x axis and visib in the y axis to determine whether they are correlated.
 ggplot(weather, aes(x = precip, y = visib)) +
  geom_point(alpha = 0.1) +
  theme_minimal() +
  labs(x = "Precipitation (inches)", y = "Visibility (miles)",
    title = "There seems to be no relationship between \n Precipitation and Visibility")

![img](file:///C:/Users/c14cc/AppData/Local/Temp/msohtmlclip1/01/clip_image004.png)



## Problem 5: Use the flights and planes tables to answer the following questions:

\# How many planes have a missing date of manufacture?
 \# I am using the sum(is.na(year) to return the number of planes that are missing a manufacure date.)
 planes %>%
  summarise(missing_manufacture_date = sum(is.na(year)))

\# A tibble: 1 × 1
  missing_manufacture_date
           <int>
 1            70

\# What are the five most common manufacturers?
 \# I am creating a table with the manufacurer variable and the number of planes they have produced, I then use the head() command to only show the top 5.
 five_common_man<-planes %>%
  count(manufacturer, sort = TRUE) %>%
  head(5)
 
 print(five_common_man)

\# A tibble: 5 × 2
  manufacturer     n
  <chr>      <int>
 1 BOEING      1630
 2 AIRBUS INDUSTRIE  400
 3 BOMBARDIER INC   368
 4 AIRBUS       336
 5 EMBRAER      299

\# Has the distribution of manufacturer changed over time as reflected by the airplanes flying from NYC in 2013? (Hint: you may need to use case_when() to recode the manufacturer name and collapse rare vendors into a category called Other.)
 
 \# I am first adding a service_year variable to the planes table
 planes <- planes %>%
  mutate(service_year = year)
 
 \# I then join the flights and planes tables
 flights_planes <- flights %>%
  filter(year == 2013, 
     origin %in% c("JFK", "LGA", "EWR")) %>%
  left_join(planes, by = "tailnum")
 
 \# Now I can group by service_year and manufacturer
 flights_planes %>%
  filter(!is.na(manufacturer), 
     !is.na(service_year)) %>%
  group_by(service_year, 
      manufacturer) %>%
  summarise(count = n()) %>%
  ggplot(aes(x = service_year, 
       y = count, 
       fill = manufacturer)) +
  geom_bar(stat = "identity", 
      position = "stack") +
  labs(x = "Service Year", 
    y = "Count", 
    fill = "Manufacturer",
    title = "Distribution of Manufacturer Over Time") +
  theme_minimal()

`summarise()` has grouped output by 'service_year'. You can override using the
 `.groups` argument.

![img](file:///C:/Users/c14cc/AppData/Local/Temp/msohtmlclip1/01/clip_image005.png)

top_manufacturers <- flights %>%
  filter(year == 2013, origin %in% c("JFK", "LGA", "EWR")) %>%
  left_join(planes, by = "tailnum") %>%
  filter(!is.na(manufacturer)) %>%
  group_by(manufacturer) %>%
  summarise(n = n()) %>%
  arrange(desc(n)) %>%
  top_n(5) %>%
  pull(manufacturer)

Selecting by n

flights %>%
  filter(year == 2013, origin %in% c("JFK", "LGA", "EWR")) %>%
  left_join(planes, by = "tailnum") %>%
  filter(!is.na(manufacturer)) %>%
  mutate(manufacturer_recode = case_when(
   manufacturer %in% top_manufacturers ~ manufacturer,
   TRUE ~ "Other"
  )) %>%
  group_by(manufacturer_recode) %>%
  summarise(n = n()) %>%
  ggplot(aes(x = reorder(manufacturer_recode, n), y = n)) +
  geom_col() +
  labs(x = "Manufacturer", y = "Number of flights",
    title = "Distribution of manufacturer over time (2013)",
    subtitle = "Manufacturers with fewer flights are categorized as 'Other'") +
  coord_flip()

![img](file:///C:/Users/c14cc/AppData/Local/Temp/msohtmlclip1/01/clip_image006.png)

\# First, I identify the top 5 manufacturers based on the number of planes they have manufactured and group the data by manufacturer, then use the summarise command to count the number of planes from each manufacturer. I then arrange the data in descending order and use top_n() to show the top 5 manufacturers. I use the pull() function to show the manufacturer names as a vector.
 
 top_manufacturers <- planes %>%
  filter(!is.na(manufacturer)) %>%
  group_by(manufacturer) %>%
  summarise(n = n(), .groups = "drop") %>%
  arrange(desc(n)) %>%
  top_n(5) %>%
  pull(manufacturer)

Selecting by n

\# I crate a new column, manufacturer_recode, in the planes dataframe. If a plane's manufacturer is in the top 5 manufacturers, I will retain its original manufacturer name; otherwise, it will be labeled as "Other" by using the case_when() command
 planes_recode <- planes %>%
  mutate(manufacturer_recode = case_when(
   manufacturer %in% top_manufacturers ~ manufacturer,
   TRUE ~ "Other"
  ))
 
 \# I create a stacked bar plot that shows the distribution of plane manufacturers over time. I first filter out rows where the year or the recoded manufacturer is missing and then group by year and manufacturer, and count the number of planes from each manufacturer for each year. I use the ggplot() function to create the plot.
 planes_recode %>%
  filter(!is.na(year), !is.na(manufacturer_recode)) %>%
  group_by(year, manufacturer_recode) %>%
  summarise(n = n(), .groups = "drop") %>%
  ggplot(aes(x = year, y = n, fill = manufacturer_recode)) +
  geom_col() +
  labs(title = "Distribution of plane manufacturers over time",
    x = "Year of manufacture",
    y = "Number of planes",
    fill = "Manufacturer")

![img](file:///C:/Users/c14cc/AppData/Local/Temp/msohtmlclip1/01/clip_image007.png)



## Problem 6: Use the flights and planes tables to answer the following questions:

\# What is the oldest plane (specified by the tailnum variable) that flew from New York City airports in 2013?
 
 \# I first filter for the year 2013 and the NY airports
 oldest_plane <- flights %>%
  filter(year == 2013, 
     origin %in% c("JFK", "LGA", "EWR")) %>%
  
 \# Then I join the planes table with the flights table with left_join, by the variable "tailnum", which they have in common
  left_join(planes, 
       by = "tailnum", 
       suffix = c("_flights", "_planes")) %>%
 
 \# I am getting rid of the planes that don't have a manufacture year
  filter(!is.na(year_planes)) %>%
 
 \# I now arrange the planes in ascending order by their year and use slice(1) to select the oldest plane
  arrange(year_planes) %>%
  slice(1) %>%
  select(tailnum, year_planes)
 
 print(oldest_plane)

\# A tibble: 1 × 2
  tailnum year_planes
  <chr>     <int>
 1 N381AA     1956

\# How many airplanes that flew from New York City are included in the planes table?
 
 \# I filter for the year 2013 and the NYC airports for origin
 planes_in_nyc <- flights %>%
  filter(year == 2013, 
     origin %in% c("JFK", "LGA", "EWR")) %>%
 
 \# I select the planes by their tailnumber and use the unique funcion to avoid repeats
  select(tailnum) %>%
  unique() %>%
 
  \# I match the tailnum column from both data frames and return only the rows from the unique tailnum values that have matches in the planes data
  semi_join(planes, by = "tailnum")
 
 \#I count the number of rows to get the number of planes that flew New York City airports 
 nrow(planes_in_nyc)

[1] 3322



## Problem 7: Use the nycflights13 to answer the following questions:

\-  What is the median arrival delay on a month-by-month basis in each airport?
 \-  For each airline, plot the median arrival delay for each month and origin airport.

\# What is the median arrival delay on a month-by-month basis in each airport?
 
 \# I group the data by month and origin and calculate the median arrival delay for each group. With the na.rm = TRUE argument I remove the missing values before calculating the median.
 flights %>%
  group_by(month, 
      origin) %>%
  summarise(median_arr_delay = median(arr_delay, 
                    na.rm = TRUE))

`summarise()` has grouped output by 'month'. You can override using the
 `.groups` argument.

\# A tibble: 36 × 3
 \# Groups:  month [12]
  month origin median_arr_delay
  <int> <chr>       <dbl>
 1   1 EWR          0
 2   1 JFK         -7
 3   1 LGA         -4
 4   2 EWR         -2
 5   2 JFK         -5
 6   2 LGA         -4
 7   3 EWR         -4
 8   3 JFK         -7
 9   3 LGA         -7
 10   4 EWR         -1
 \# ℹ 26 more rows

\# For each airline, plot the median arrival delay for each month and origin airport
 
 \# I first group the data by carrier, month and origin and calculate the median arrival delay for each group.
 flights %>%
  group_by(carrier, 
      month, 
       origin) %>%
  summarise(median_arr_delay = median(arr_delay, 
                    na.rm = TRUE)) %>%
  
 \# I do a line plot with month in the x axis and the median arrival delay in the y axis, select the carrier variable as the group and making the colors different for the carriers. I use facet wrap to create separate subplots for each origin airport. 
  ggplot(aes(x = month, 
       y = median_arr_delay, 
       group = carrier, 
       color = carrier)) +
  geom_line() +
  facet_wrap(~origin) +
  labs(x = "Month", 
    y = "Median Arrival Delay (minutes)",
    title = "Median Arrival Delay by Month and Origin for Each Airline",
    color = "Airline") +
  theme_minimal()

`summarise()` has grouped output by 'carrier', 'month'. You can override using
 the `.groups` argument.

![img](file:///C:/Users/c14cc/AppData/Local/Temp/msohtmlclip1/01/clip_image008.png)



## Problem 8: Let’s take a closer look at what carriers service the route to San Francisco International (SFO). Join the flights and airlines tables and count which airlines flew the most to SFO. Produce a new dataframe, fly_into_sfo that contains three variables: the name of the airline, e.g., United Air Lines Inc. not UA, the count (number) of times it flew to SFO, and the percent of the trips that that particular airline flew to SFO.

fly_into_sfo <- flights %>%
  
 \# I filter the flights for those that flew to San Francisco. I then left join this with the airlines data frame, matching the carrier column from both data frames.
  filter(dest == 'SFO') %>%
  left_join(airlines, 
       by = c("carrier" = "carrier")) %>%
 
 \# I group by the name of the plane and count the number of rows.
  group_by(name) %>%
  summarise(count = n()) %>%
  
 \# I add a new column called percent to the data frame, which calculates the percentage of flights for each airline. This gives the percentage representation of each airline's flights to SFO and assigns it to fly_into_sfo.
  mutate(percent = count / sum(count) * 100)
 
 print(fly_into_sfo)

\# A tibble: 5 × 3
  name          count percent
  <chr>         <int>  <dbl>
 1 American Airlines Inc. 1422  10.7 
 2 Delta Air Lines Inc.  1858  13.9 
 3 JetBlue Airways     1035  7.76
 4 United Air Lines Inc.  6819  51.2 
 5 Virgin America     2197  16.5 

And here is some bonus ggplot code to plot your dataframe

fly_into_sfo %>% 
  
  \# sort 'name' of airline by the numbers it times to flew to SFO
  mutate(name = fct_reorder(name, count)) %>% 
  
  ggplot() +
  
  aes(x = count, 
    y = name) +
  
  \# a simple bar/column plot
  geom_col() +
  
  \# add labels, so each bar shows the % of total flights 
  geom_text(aes(label = percent),
       hjust = 1, 
       colour = "white", 
       size = 5)+
  
  \# add labels to help our audience 
  labs(title="Which airline dominates the NYC to SFO route?", 
    subtitle = "as % of total flights in 2013",
    x= "Number of flights",
    y= NULL) +
  
  theme_minimal() + 
  
  \# change the theme-- i just googled those , but you can use the ggThemeAssist add-in
  \# https://cran.r-project.org/web/packages/ggThemeAssist/index.html
  
  theme(#
   \# so title is left-aligned
   plot.title.position = "plot",
   
   \# text in axes appears larger    
   axis.text = element_text(size=12),
   
   \# title text is bigger
   plot.title = element_text(size=18)
    ) +
 
  \# add one final layer of NULL, so if you comment out any lines
  \# you never end up with a hanging `+` that awaits another ggplot layer
  NULL

![img](file:///C:/Users/c14cc/AppData/Local/Temp/msohtmlclip1/01/clip_image009.png)



## Problem 9: Let’s take a look at cancellations of flights to SFO. We create a new dataframe cancellations as follows

cancellations <- flights %>% 
  
  \# just filter for destination == 'SFO'
  filter(dest == 'SFO') %>% 
  
  \# a cancelled flight is one with no `dep_time` 
  filter(is.na(dep_time))

I want you to think how we would organise our data manipulation to create the following plot. No need to write the code, just explain in words how you would go about it.

I first filter for destination SFO, and then for the missing dep_time values to get the cancelled flights.I would group the date by departure airport and carrier. Then I can create a bar graph of the cancellations over time using facet wrap, with the cancellations on the y axis and the month on the x axis.

![img](file:///C:/Users/c14cc/AppData/Local/Temp/msohtmlclip1/01/clip_image011.png)



## Problem 10: On your own – Hollywood Age Gap

The website https://hollywoodagegap.com is a record of *THE AGE DIFFERENCE IN YEARS BETWEEN MOVIE LOVE INTERESTS*. This is an informational site showing the age gap between movie love interests and the data follows certain rules:

•      The two (or more) actors play actual love interests (not just friends, coworkers, or some other non-romantic type of relationship)

•      The youngest of the two actors is at least 17 years old

•      No animated characters

age_gaps <- readr::read_csv('https://raw.githubusercontent.com/rfordatascience/tidytuesday/master/data/2023/2023-02-14/age_gaps.csv')

Rows: 1155 Columns: 13
 ── Column specification ────────────────────────────────────────────────────────
 Delimiter: ","
 chr (6): movie_name, director, actor_1_name, actor_2_name, character_1_gend...
 dbl (5): release_year, age_difference, couple_number, actor_1_age, actor_2_age
 date (2): actor_1_birthdate, actor_2_birthdate
 
 ℹ Use `spec()` to retrieve the full column specification for this data.
 ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

glimpse(age_gaps)

Rows: 1,155
 Columns: 13
 $ movie_name     <chr> "Harold and Maude", "Venus", "The Quiet American", …
 $ release_year    <dbl> 1971, 2006, 2002, 1998, 2010, 1992, 2009, 1999, 199…
 $ director      <chr> "Hal Ashby", "Roger Michell", "Phillip Noyce", "Joe…
 $ age_difference   <dbl> 52, 50, 49, 45, 43, 42, 40, 39, 38, 38, 36, 36, 35,…
 $ couple_number   <dbl> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, …
 $ actor_1_name    <chr> "Ruth Gordon", "Peter O'Toole", "Michael Caine", "D…
 $ actor_2_name    <chr> "Bud Cort", "Jodie Whittaker", "Do Thi Hai Yen", "T…
 $ character_1_gender <chr> "woman", "man", "man", "man", "man", "man", "man", …
 $ character_2_gender <chr> "man", "woman", "woman", "woman", "man", "woman", "…
 $ actor_1_birthdate <date> 1896-10-30, 1932-08-02, 1933-03-14, 1930-09-17, 19…
 $ actor_2_birthdate <date> 1948-03-29, 1982-06-03, 1982-10-01, 1975-11-08, 19…
 $ actor_1_age    <dbl> 75, 74, 69, 68, 81, 59, 62, 69, 57, 77, 59, 56, 65,…
 $ actor_2_age    <dbl> 23, 24, 20, 23, 38, 17, 22, 30, 19, 39, 23, 20, 30,…

\# How is age_difference distributed? What's the 'typical' age_difference in movies?
 
 \# I create a histogram with the age difference in the x axis. I am also adding vertical lines that reflects the median and mean age differences. 
 ggplot(age_gaps, aes(x = age_difference)) +
  geom_histogram(binwidth = 1, fill = "pink", color = "black") +
  geom_vline(aes(xintercept=mean(age_difference)), size=0.75, color="red", clip="off")+
  geom_vline(aes(xintercept=median(age_difference)), size=0.75, color="purple")+
   geom_text(aes(x=10, label="Mean Age Difference", y=-5), colour="red", size=3)+
  theme_minimal() +
  geom_text(aes(x=7, label="Median Age Difference", y=-9), colour="purple", size=3)+
  theme_minimal() +
  labs(title = "The Age Difference Distribution is right-skewed, \n with the mean age difference being 10 and median 8", 
    x = "Age Difference", 
    y = "Frequency",
    )

Warning: Using `size` aesthetic for lines was deprecated in ggplot2 3.4.0.
 ℹ Please use `linewidth` instead.

Warning in geom_vline(aes(xintercept = mean(age_difference)), size = 0.75, :
 Ignoring unknown parameters: `clip`

![img](file:///C:/Users/c14cc/AppData/Local/Temp/msohtmlclip1/01/clip_image012.png)

\# The half plus seven\ rule. 
 
 \# I filter the data in the values to the ones that comply with the half plus seven rule formula and then count the number of rows in the filtered table.
 actors_complying_with_min_age <- age_gaps %>%
 filter(actor_1_age>=(actor_1_age/ 2) + 7) %>% 
  filter(actor_1_age<=(actor_2_age-7)*2) %>% 
  nrow() %>% 
  print()

[1] 829

\# I then calculate the percentage of actors that comply with the half plus seven rules by dividing the number of rows in the filtered table with the original table and multiplying by 100.
 pct_7_age_rule<- (actors_complying_with_min_age/nrow(age_gaps))*100
 
 \# I display the percentage to 2 decimal points.
 print(sprintf("The percentage of actors complying with the half plus seven rule is %.2f%%", pct_7_age_rule))

[1] "The percentage of actors complying with the half plus seven rule is 71.77%"

\# Which movie has the greatest number of love interests?
 
 \# I group the data by the movie names, count the number of couples in the movie and arrange in descending order. I use slice(1) to select the movie with the most couples.
 movie_with_most_love_interests <- age_gaps %>% 
  group_by(movie_name) %>% 
  summarise(couple_number=n()) %>% 
  arrange(desc(couple_number)) %>% 
  slice(1)
 
 \#Which actors/ actresses have the greatest number of love interests in this dataset?
 
 \# I combine the age gaps data frame with the actor_1_name and actor_2_name columns into a new column called actor_names
 age_gaps_names_merged <- age_gaps %>% 
  unite(actor_names, actor_1_name, actor_2_name, sep = " ")
 
 \# I group by the actor names and count the number of couples the actors are in, then arrange by descending order.
 actors_with_greates_love_interests<-age_gaps_names_merged %>% 
  group_by(actor_names) %>% 
  summarise(couple_number=n()) %>% 
   arrange(desc(couple_number))
 
 
 \#Is the mean/median age difference staying constant over the years (1935 - 2022)?
 
 \# I create a bar graph with the movie release year in the x axis and the mean age difference in the y axis.
 age_gaps %>% 
  ggplot(aes(x = release_year, y = mean(age_difference)))+
  geom_col(fill="purple", color="white")+
  theme_minimal()+
  labs(title = "The distribution of mean age difference over time is left \n skewed as the age difference has increased over time",
    x = "Release year",
    y = "Mean age difference")

![img](file:///C:/Users/c14cc/AppData/Local/Temp/msohtmlclip1/01/clip_image013.png)

\#How frequently does Hollywood depict same-gender love interests?
 
 \# I create a same gender variable that returns the number of times when the character 1's gender is the same as character 2's.
 age_gaps$same_gender <- age_gaps$character_1_gender == age_gaps$character_2_gender
 table(age_gaps$same_gender)


 FALSE TRUE 
 1132  23 

\# Calculate the proportion of same sex couples
 same_gender_pct <- mean(age_gaps$same_gender)*100
 
 print(sprintf("The percentage of same gender love interests in Hollywood is %.2f%%", same_gender_pct))

[1] "The percentage of same gender love interests in Hollywood is 1.99%"



# Deliverables

There is a lot of explanatory text, comments, etc. You do not need these, so delete them and produce a stand-alone document that you could share with someone. Render the edited and completed Quarto Markdown (qmd) file as a Word document (use the “Render” button at the top of the script editor window) and upload it to Canvas. You must be commiting and pushing tour changes to your own Github repo as you go along.



# Details

•      Who did you collaborate with: Nobody

•      Approximately how much time did you spend on this problem set: 5 hours

•      What, if anything, gave you the most trouble: I think I struggled a bit with figuring out how to approach the questions, particularly the few last problems.

**Please seek out help when you need it,** and remember the [*15-minute rule*](https://mam2022.netlify.app/syllabus/#the-15-minute-rule). You know enough R (and have enough examples of code from class and your readings) to be able to do this. If you get stuck, ask for help from others, post a question on Slack– and remember that I am here to help too!

As a true test to yourself, do you understand the code you submitted and are you able to explain it to someone else? Yes



# Rubric

13/13: Problem set is 100% completed. Every question was attempted and answered, and most answers are correct. Code is well-documented (both self-documented and with additional comments as necessary). Used tidyverse, instead of base R. Graphs and tables are properly labelled. Analysis is clear and easy to follow, either because graphs are labeled clearly or you’ve written additional text to describe how you interpret the output. Multiple Github commits. Work is exceptional. I will not assign these often.

8/13: Problem set is 60–80% complete and most answers are correct. This is the expected level of performance. Solid effort. Hits all the elements. No clear mistakes. Easy to follow (both the code and the output). A few Github commits.

5/13: Problem set is less than 60% complete and/or most answers are incorrect. This indicates that you need to improve next time. I will hopefully not assign these often. Displays minimal effort. Doesn’t complete all components. Code is poorly written and not documented. Uses the same type of plot for each graph, or doesn’t use plots appropriate for the variables being analyzed. No Github commits.Data Manipulation

## Problem 1: Use logical operators to find flights that:

\# For problem 1, I will be using the filter function to select which variables I want
 glimpse(flights)

Rows: 336,776
 Columns: 19
 $ year      <int> 2013, 2013, 2013, 2013, 2013, 2013, 2013, 2013, 2013, 2…
 $ month     <int> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1…
 $ day      <int> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1…
 $ dep_time    <int> 517, 533, 542, 544, 554, 554, 555, 557, 557, 558, 558, …
 $ sched_dep_time <int> 515, 529, 540, 545, 600, 558, 600, 600, 600, 600, 600, …
 $ dep_delay   <dbl> 2, 4, 2, -1, -6, -4, -5, -3, -3, -2, -2, -2, -2, -2, -1…
 $ arr_time    <int> 830, 850, 923, 1004, 812, 740, 913, 709, 838, 753, 849,…
 $ sched_arr_time <int> 819, 830, 850, 1022, 837, 728, 854, 723, 846, 745, 851,…
 $ arr_delay   <dbl> 11, 20, 33, -18, -25, 12, 19, -14, -8, 8, -2, -3, 7, -1…
 $ carrier    <chr> "UA", "UA", "AA", "B6", "DL", "UA", "B6", "EV", "B6", "…
 $ flight     <int> 1545, 1714, 1141, 725, 461, 1696, 507, 5708, 79, 301, 4…
 $ tailnum    <chr> "N14228", "N24211", "N619AA", "N804JB", "N668DN", "N394…
 $ origin     <chr> "EWR", "LGA", "JFK", "JFK", "LGA", "EWR", "EWR", "LGA",…
 $ dest      <chr> "IAH", "IAH", "MIA", "BQN", "ATL", "ORD", "FLL", "IAD",…
 $ air_time    <dbl> 227, 227, 160, 183, 116, 150, 158, 53, 140, 138, 149, 1…
 $ distance    <dbl> 1400, 1416, 1089, 1576, 762, 719, 1065, 229, 944, 733, …
 $ hour      <dbl> 5, 5, 5, 5, 6, 5, 6, 6, 6, 6, 6, 6, 6, 6, 6, 5, 6, 6, 6…
 $ minute     <dbl> 15, 29, 40, 45, 0, 58, 0, 0, 0, 0, 0, 0, 0, 0, 0, 59, 0…
 $ time_hour   <dttm> 2013-01-01 05:00:00, 2013-01-01 05:00:00, 2013-01-01 0…

\# Had an arrival delay of two or more hours (> 120 minutes)
 delay_2hr <- flights %>% 
  filter(arr_delay>=120)
 print(delay_2hr)

\# A tibble: 10,200 × 19
   year month  day dep_time sched_dep_time dep_delay arr_time sched_arr_time
  <int> <int> <int>  <int>     <int>   <dbl>  <int>     <int>
 1 2013   1   1   811      630    101   1047      830
 2 2013   1   1   848      1835    853   1001      1950
 3 2013   1   1   957      733    144   1056      853
 4 2013   1   1   1114      900    134   1447      1222
 5 2013   1   1   1505      1310    115   1638      1431
 6 2013   1   1   1525      1340    105   1831      1626
 7 2013   1   1   1549      1445    64   1912      1656
 8 2013   1   1   1558      1359    119   1718      1515
 9 2013   1   1   1732      1630    62   2028      1825
 10 2013   1   1   1803      1620    103   2008      1750
 \# ℹ 10,190 more rows
 \# ℹ 11 more variables: arr_delay <dbl>, carrier <chr>, flight <int>,
 \#  tailnum <chr>, origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>,
 \#  hour <dbl>, minute <dbl>, time_hour <dttm>

\# Flew to Houston (IAH or HOU)
 dest_IAH_HOU <- flights %>% 
  filter(dest=="IAH"|dest=="HOU")
 print(dest_IAH_HOU)

\# A tibble: 9,313 × 19
   year month  day dep_time sched_dep_time dep_delay arr_time sched_arr_time
  <int> <int> <int>  <int>     <int>   <dbl>  <int>     <int>
 1 2013   1   1   517      515     2   830      819
 2 2013   1   1   533      529     4   850      830
 3 2013   1   1   623      627    -4   933      932
 4 2013   1   1   728      732    -4   1041      1038
 5 2013   1   1   739      739     0   1104      1038
 6 2013   1   1   908      908     0   1228      1219
 7 2013   1   1   1028      1026     2   1350      1339
 8 2013   1   1   1044      1045    -1   1352      1351
 9 2013   1   1   1114      900    134   1447      1222
 10 2013   1   1   1205      1200     5   1503      1505
 \# ℹ 9,303 more rows
 \# ℹ 11 more variables: arr_delay <dbl>, carrier <chr>, flight <int>,
 \#  tailnum <chr>, origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>,
 \#  hour <dbl>, minute <dbl>, time_hour <dttm>

\# we can also do filter(dest %in% c("IAH", "HOU"))
 
 \# Were operated by United (`UA`), American (`AA`), or Delta (`DL`)
 UA_AA_DL <- flights %>% 
  filter(carrier=="UA"| carrier=="AA"| carrier=="DL")
 print(UA_AA_DL)

\# A tibble: 139,504 × 19
   year month  day dep_time sched_dep_time dep_delay arr_time sched_arr_time
  <int> <int> <int>  <int>     <int>   <dbl>  <int>     <int>
 1 2013   1   1   517      515     2   830      819
 2 2013   1   1   533      529     4   850      830
 3 2013   1   1   542      540     2   923      850
 4 2013   1   1   554      600    -6   812      837
 5 2013   1   1   554      558    -4   740      728
 6 2013   1   1   558      600    -2   753      745
 7 2013   1   1   558      600    -2   924      917
 8 2013   1   1    558      600    -2   923      937
 9 2013   1   1   559      600    -1   941      910
 10 2013   1   1   559      600    -1   854      902
 \# ℹ 139,494 more rows
 \# ℹ 11 more variables: arr_delay <dbl>, carrier <chr>, flight <int>,
 \#  tailnum <chr>, origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>,
 \#  hour <dbl>, minute <dbl>, time_hour <dttm>

\# Departed in summer (July, August, and September)
 summer_dep <- flights %>% 
  filter(month=="7"| month=="8"| month=="9")
 print(summer_dep)

\# A tibble: 86,326 × 19
   year month  day dep_time sched_dep_time dep_delay arr_time sched_arr_time
  <int> <int> <int>  <int>     <int>   <dbl>  <int>     <int>
 1 2013   7   1    1      2029    212   236      2359
 2 2013   7   1    2      2359     3   344      344
 3 2013   7   1    29      2245    104   151       1
 4 2013   7   1    43      2130    193   322       14
 5 2013   7   1    44      2150    174   300      100
 6 2013   7   1    46      2051    235   304      2358
 7 2013   7   1    48      2001    287   308      2305
 8 2013   7   1    58      2155    183   335       43
 9 2013   7   1   100      2146    194   327       30
 10 2013   7   1   100      2245    135   337      135
 \# ℹ 86,316 more rows
 \# ℹ 11 more variables: arr_delay <dbl>, carrier <chr>, flight <int>,
 \#  tailnum <chr>, origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>,
 \#  hour <dbl>, minute <dbl>, time_hour <dttm>

\# Arrived more than two hours late, but didn't leave late
 arr_only_delay <-flights %>% 
  filter(arr_delay>=120 & dep_delay<=0)
 print(arr_only_delay)

\# A tibble: 29 × 19
   year month  day dep_time sched_dep_time dep_delay arr_time sched_arr_time
  <int> <int> <int>  <int>     <int>   <dbl>  <int>     <int>
 1 2013   1  27   1419      1420    -1   1754      1550
 2 2013  10   7   1350      1350     0   1736      1526
 3 2013  10   7   1357      1359    -2   1858      1654
 4 2013  10  16   657      700    -3   1258      1056
 5 2013  11   1   658      700    -2   1329      1015
 6 2013   3  18   1844      1847    -3    39      2219
 7 2013   4  17   1635      1640    -5   2049      1845
 8 2013   4  18   558      600    -2   1149      850
 9 2013   4  18   655      700    -5   1213      950
 10 2013   5  22   1827      1830    -3   2217      2010
 \# ℹ 19 more rows
 \# ℹ 11 more variables: arr_delay <dbl>, carrier <chr>, flight <int>,
 \#  tailnum <chr>, origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>,
 \#  hour <dbl>, minute <dbl>, time_hour <dttm>

\# Were delayed by at least an hour, but made up over 30 minutes in flight
 del_made_up <- flights %>% 
  filter(dep_delay>=60 & arr_delay<=60)
 print(del_made_up)

\# A tibble: 3,969 × 19
   year month  day dep_time sched_dep_time dep_delay arr_time sched_arr_time
  <int> <int> <int>  <int>     <int>   <dbl>  <int>     <int>
 1 2013   1   1   826      715    71   1136      1045
 2 2013   1   1   1628      1524    64   1740      1641
 3 2013   1   1   1846      1745    61   2147      2055
 4 2013   1   1   2302      2200    62   2342      2253
 5 2013   1   2   1125      1020    65   1309      1223
 6 2013   1   2   1345      1240    65   1642      1555
 7 2013   1   2   1421      1314    67   1515      1415
 8 2013   1   2   1618      1516    62   1913      1825
 9 2013   1   2   1801      1655    66   1932      1843
 10 2013   1   2   2108      1954    74   2218      2119
 \# ℹ 3,959 more rows
 \# ℹ 11 more variables: arr_delay <dbl>, carrier <chr>, flight <int>,
 \#  tailnum <chr>, origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>,
 \#  hour <dbl>, minute <dbl>, time_hour <dttm>



## Problem 2: What months had the highest and lowest proportion of cancelled flights? Interpret any seasonal patterns. To determine if a flight was cancelled use the following code

flights %>% 
  filter(is.na(dep_time))

\# What months had the highest and lowest % of cancelled flights?
 
 \# I wil group the data by the month variable and then use the summarise function to to find out the mean percentage of cancelled flights per month.
 cancelled_by_month<- flights %>% 
  group_by(month) %>%
  summarise(cancelled_pct = mean(is.na(dep_time)) * 100)
 
 print(cancelled_by_month)

\# A tibble: 12 × 2
  month cancelled_pct
  <int>     <dbl>
 1   1     1.93 
 2   2     5.05 
 3   3     2.99 
 4   4     2.36 
 5   5     1.96 
 6   6     3.57 
 7   7     3.19 
 8   8     1.66 
 9   9     1.64 
 10  10     0.817
 11  11     0.854
 12  12     3.64 

\# Find the month with the highest percentage of cancelled flights
 
 \# I am filtering the percentages of cancelled flights and selecting the the month with the highest percentage
 highest_cancelled_month <- cancelled_by_month %>%
  filter(cancelled_pct == max(cancelled_pct)) %>%
  pull(month)
 
 print(highest_cancelled_month)

[1] 2

\# Find the month with the lowest percentage of cancelled flights
 
 \# I am filtering the percentages of cancelled flights and selecting the the month with the lowest percentage
 lowest_cancelled_month <- cancelled_by_month %>%
  filter(cancelled_pct == min(cancelled_pct)) %>%
  pull(month)
 
 print(lowest_cancelled_month)

[1] 10



## Problem 3: What plane (specified by the tailnum variable) traveled the most times from New York City airports in 2013? Please left_join() the resulting table with the table planes (also included in the nycflights13 package).

For the plane with the greatest number of flights and that had more than 50 seats, please create a table where it flew to during 2013.

\# I will filter for the year 2013, the NYC airports and the tail number, using the !is.na() command to avoid an empty table givien that there are some missing values. I will then group by the tailnumber and use the summarise function to create a table with the number of flights per tailnumber.
 flight_counts <- flights %>%
  filter(year == 2013) %>%
  filter(origin %in% c("JFK", "LGA", "EWR")) %>%
  filter(!is.na(tailnum)) %>% 
  group_by(tailnum) %>%
  summarise(flight_count = n())
 
 print(flight_counts)

\# A tibble: 4,043 × 2
  tailnum flight_count
  <chr>     <int>
 1 D942DN       4
 2 N0EGMQ      371
 3 N10156      153
 4 N102UW      48
 5 N103US      46
 6 N104UW      47
 7 N10575      289
 8 N105UW      45
 9 N107US      41
 10 N108UW      60
 \# ℹ 4,033 more rows

\# I am arranging the previously created table in descending order and using the slice() command to give me the tailnumber with the highest count of flights.
 most_flights <- flight_counts %>%
  arrange(desc(flight_count)) %>%
  slice(1)
 
 print(most_flights)

\# A tibble: 1 × 2
  tailnum flight_count
  <chr>     <int>
 1 N725MQ      575

most_flown_plane <- most_flights$tailnum
 
 print(most_flown_plane)

[1] "N725MQ"

\# I am left joining the the flight counts table with the planes table by the variable they have in common (tailnum), and then arranging it in descending order.
 joining_planes_flights <- left_join(flight_counts,
           planes, 
           by = "tailnum") %>%
  arrange(desc(flight_count))
 print(joining_planes_flights)

\# A tibble: 4,043 × 10
  tailnum flight_count year type    manufacturer model engines seats speed
  <chr>     <int> <int> <chr>    <chr>    <chr>  <int> <int> <int>
 1 N725MQ      575  NA <NA>    <NA>     <NA>    NA  NA  NA
 2 N722MQ      513  NA <NA>    <NA>     <NA>    NA  NA  NA
 3 N723MQ      507  NA <NA>    <NA>     <NA>    NA  NA  NA
 4 N711MQ      486 1976 Fixed wing… GULFSTREAM … G115…    2  22  NA
 5 N713MQ      483  NA <NA>    <NA>     <NA>    NA  NA  NA
 6 N258JB      427 2006 Fixed wing… EMBRAER   ERJ …    2  20  NA
 7 N298JB      407 2009 Fixed wing… EMBRAER   ERJ …    2  20  NA
 8 N353JB      404 2012 Fixed wing… EMBRAER   ERJ …    2  20  NA
 9 N351JB      402 2012 Fixed wing… EMBRAER   ERJ …    2  20  NA
 10 N735MQ      396  NA <NA>    <NA>     <NA>    NA  NA  NA
 \# ℹ 4,033 more rows
 \# ℹ 1 more variable: engine <chr>

\# To find out where the plane with the greatest number of flights and that had more than 50 seats flew to during 2013 I am first filtering for the year 2014, NYC airports of origin and tailnumber, using is.na() to deal with the missing values. I am leftjoining this data with the planes table by the variable they have in common, tailnum.
 flights_planes <- flights %>%
  filter(year == 2013, 
     origin %in% c("JFK", "LGA", "EWR")) %>%
  filter(!is.na(tailnum)) %>%
  left_join(planes, by = "tailnum")
 
 \# Then I am filtering for the planes which have more tham 50 seats, grouping them by tailnumber and creating a table with their flight counts. I arrange it in descending order and select the tailnumber with the highest count (using the slice(1) command.)
 most_flights_over_50_seats <- flights_planes %>%
  filter(seats > 50) %>%
  group_by(tailnum) %>%
  summarise(flight_count = n()) %>%
  arrange(desc(flight_count)) %>%
  slice(1)
 
 print(most_flights_over_50_seats)

\# A tibble: 1 × 2
  tailnum flight_count
  <chr>     <int>
 1 N328AA      393

\# Now, get the destinations for this plane
 most_flown_plane_over_50_seats <- most_flights_over_50_seats$tailnum[1]
 
 \# I am using the leftjoined flights_planes table to filter out for the previously found most flown plane with over 50 seats. I then select the dest variable to get the plane's destinations and use the unique() command to avoid repetitions.
 destinations <- flights_planes %>%
  filter(tailnum == most_flown_plane_over_50_seats) %>%
  select(dest) %>%
  unique()
 
 print(destinations)

\# A tibble: 6 × 1
  dest 
  <chr>
 1 LAX 
 2 SFO 
 3 SJU 
 4 MIA 
 5 MCO 
 6 BOS 



## Problem 4: The nycflights13 package includes a table (weather) that describes the weather during 2013. Use that table to answer the following questions:

glimpse(weather)

Rows: 26,115
 Columns: 15
 $ origin   <chr> "EWR", "EWR", "EWR", "EWR", "EWR", "EWR", "EWR", "EWR", "EW…
 $ year    <int> 2013, 2013, 2013, 2013, 2013, 2013, 2013, 2013, 2013, 2013,…
 $ month   <int> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1,…
 $ day    <int> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1,…
 $ hour    <int> 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 13, 14, 15, 16, 17, 18, …
 $ temp    <dbl> 39.02, 39.02, 39.02, 39.92, 39.02, 37.94, 39.02, 39.92, 39.…
 $ dewp    <dbl> 26.06, 26.96, 28.04, 28.04, 28.04, 28.04, 28.04, 28.04, 28.…
 $ humid   <dbl> 59.37, 61.63, 64.43, 62.21, 64.43, 67.21, 64.43, 62.21, 62.…
 $ wind_dir  <dbl> 270, 250, 240, 250, 260, 240, 240, 250, 260, 260, 260, 330,…
 $ wind_speed <dbl> 10.35702, 8.05546, 11.50780, 12.65858, 12.65858, 11.50780, …
 $ wind_gust <dbl> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, 20.…
 $ precip   <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,…
 $ pressure  <dbl> 1012.0, 1012.3, 1012.5, 1012.2, 1011.9, 1012.4, 1012.2, 101…
 $ visib   <dbl> 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10,…
 $ time_hour <dttm> 2013-01-01 01:00:00, 2013-01-01 02:00:00, 2013-01-01 03:00…

\# What is the distribution of temperature (`temp`) in July 2013? Identify any important outliers in terms of the `wind_speed` variable.
 
 \# I first filter for the month of July.
 july_weather <- weather %>%
  filter(month == 7) 
 
 \# Histogram of temperature
 \# I am creating a histogram to find out the distribution, making the x axis the temperature. 
 ggplot(july_weather, aes(x = temp)) +
  geom_histogram(binwidth = 1, fill = "blue", color = "black") +
  theme_minimal() +
  labs(title = "The temperature in July 2013 has a normal distribution, \n slightly right skewed", 
    x = "Temperature", 
    y = "Frequency")

![img](file:///C:/Users/c14cc/AppData/Local/Temp/msohtmlclip1/01/clip_image001.png)

\# The histogram shows a normal distribution with a mean around 76, skewed to the right.
 
 \# Boxplot for outliers in wind_speed
 \# I am creating a boxplot to find out the outliers, making the y axis the wind speed.
 ggplot(july_weather, aes(y = wind_speed)) +
  geom_boxplot(fill = "blue", color = "black") +
  theme_minimal() +
  labs(title = "There are 3 wind speed outliers in July 2013, \n between the values of 20 and 26",
    y = "Wind Speed")

Warning: Removed 2 rows containing non-finite values (`stat_boxplot()`).

![img](file:///C:/Users/c14cc/AppData/Local/Temp/msohtmlclip1/01/clip_image002.png)

\# What is the relationship between `dewp` and `humid`?
 \# I am creating a dotplot with the variable dewp in the x axis and humid in the y axis to determine whether they are correlated.
 ggplot(weather, aes(x = dewp, y = humid)) +
  geom_point(alpha = 0.1) +
  theme_minimal() +
  labs(x = "Dew Point (°F)", y = "Humidity (%)",
    title = "There is a positive relationship between \n Dew Point and Humidity, as they increase together")

Warning: Removed 1 rows containing missing values (`geom_point()`).

![img](file:///C:/Users/c14cc/AppData/Local/Temp/msohtmlclip1/01/clip_image003.png)

\# What is the relationship between `precip` and `visib`?
 \# I am creating a dotplot with the variable precip in the x axis and visib in the y axis to determine whether they are correlated.
 ggplot(weather, aes(x = precip, y = visib)) +
  geom_point(alpha = 0.1) +
  theme_minimal() +
  labs(x = "Precipitation (inches)", y = "Visibility (miles)",
    title = "There seems to be no relationship between \n Precipitation and Visibility")

![img](file:///C:/Users/c14cc/AppData/Local/Temp/msohtmlclip1/01/clip_image004.png)



## Problem 5: Use the flights and planes tables to answer the following questions:

\# How many planes have a missing date of manufacture?
 \# I am using the sum(is.na(year) to return the number of planes that are missing a manufacure date.)
 planes %>%
  summarise(missing_manufacture_date = sum(is.na(year)))

\# A tibble: 1 × 1
  missing_manufacture_date
           <int>
 1            70

\# What are the five most common manufacturers?
 \# I am creating a table with the manufacurer variable and the number of planes they have produced, I then use the head() command to only show the top 5.
 five_common_man<-planes %>%
  count(manufacturer, sort = TRUE) %>%
  head(5)
 
 print(five_common_man)

\# A tibble: 5 × 2
  manufacturer     n
  <chr>      <int>
 1 BOEING      1630
 2 AIRBUS INDUSTRIE  400
 3 BOMBARDIER INC   368
 4 AIRBUS       336
 5 EMBRAER      299

\# Has the distribution of manufacturer changed over time as reflected by the airplanes flying from NYC in 2013? (Hint: you may need to use case_when() to recode the manufacturer name and collapse rare vendors into a category called Other.)
 
 \# I am first adding a service_year variable to the planes table
 planes <- planes %>%
  mutate(service_year = year)
 
 \# I then join the flights and planes tables
 flights_planes <- flights %>%
  filter(year == 2013, 
     origin %in% c("JFK", "LGA", "EWR")) %>%
  left_join(planes, by = "tailnum")
 
 \# Now I can group by service_year and manufacturer
 flights_planes %>%
  filter(!is.na(manufacturer), 
     !is.na(service_year)) %>%
  group_by(service_year, 
      manufacturer) %>%
  summarise(count = n()) %>%
  ggplot(aes(x = service_year, 
       y = count, 
       fill = manufacturer)) +
  geom_bar(stat = "identity", 
      position = "stack") +
  labs(x = "Service Year", 
    y = "Count", 
    fill = "Manufacturer",
    title = "Distribution of Manufacturer Over Time") +
  theme_minimal()

`summarise()` has grouped output by 'service_year'. You can override using the
 `.groups` argument.

![img](file:///C:/Users/c14cc/AppData/Local/Temp/msohtmlclip1/01/clip_image005.png)

top_manufacturers <- flights %>%
  filter(year == 2013, origin %in% c("JFK", "LGA", "EWR")) %>%
  left_join(planes, by = "tailnum") %>%
  filter(!is.na(manufacturer)) %>%
  group_by(manufacturer) %>%
  summarise(n = n()) %>%
  arrange(desc(n)) %>%
  top_n(5) %>%
  pull(manufacturer)

Selecting by n

flights %>%
  filter(year == 2013, origin %in% c("JFK", "LGA", "EWR")) %>%
  left_join(planes, by = "tailnum") %>%
  filter(!is.na(manufacturer)) %>%
  mutate(manufacturer_recode = case_when(
   manufacturer %in% top_manufacturers ~ manufacturer,
   TRUE ~ "Other"
  )) %>%
  group_by(manufacturer_recode) %>%
  summarise(n = n()) %>%
  ggplot(aes(x = reorder(manufacturer_recode, n), y = n)) +
  geom_col() +
  labs(x = "Manufacturer", y = "Number of flights",
    title = "Distribution of manufacturer over time (2013)",
    subtitle = "Manufacturers with fewer flights are categorized as 'Other'") +
  coord_flip()

![img](file:///C:/Users/c14cc/AppData/Local/Temp/msohtmlclip1/01/clip_image006.png)

\# First, I identify the top 5 manufacturers based on the number of planes they have manufactured and group the data by manufacturer, then use the summarise command to count the number of planes from each manufacturer. I then arrange the data in descending order and use top_n() to show the top 5 manufacturers. I use the pull() function to show the manufacturer names as a vector.
 
 top_manufacturers <- planes %>%
  filter(!is.na(manufacturer)) %>%
  group_by(manufacturer) %>%
  summarise(n = n(), .groups = "drop") %>%
  arrange(desc(n)) %>%
  top_n(5) %>%
  pull(manufacturer)

Selecting by n

\# I crate a new column, manufacturer_recode, in the planes dataframe. If a plane's manufacturer is in the top 5 manufacturers, I will retain its original manufacturer name; otherwise, it will be labeled as "Other" by using the case_when() command
 planes_recode <- planes %>%
  mutate(manufacturer_recode = case_when(
   manufacturer %in% top_manufacturers ~ manufacturer,
   TRUE ~ "Other"
  ))
 
 \# I create a stacked bar plot that shows the distribution of plane manufacturers over time. I first filter out rows where the year or the recoded manufacturer is missing and then group by year and manufacturer, and count the number of planes from each manufacturer for each year. I use the ggplot() function to create the plot.
 planes_recode %>%
  filter(!is.na(year), !is.na(manufacturer_recode)) %>%
  group_by(year, manufacturer_recode) %>%
  summarise(n = n(), .groups = "drop") %>%
  ggplot(aes(x = year, y = n, fill = manufacturer_recode)) +
  geom_col() +
  labs(title = "Distribution of plane manufacturers over time",
    x = "Year of manufacture",
    y = "Number of planes",
    fill = "Manufacturer")

![img](file:///C:/Users/c14cc/AppData/Local/Temp/msohtmlclip1/01/clip_image007.png)



## Problem 6: Use the flights and planes tables to answer the following questions:

\# What is the oldest plane (specified by the tailnum variable) that flew from New York City airports in 2013?
 
 \# I first filter for the year 2013 and the NY airports
 oldest_plane <- flights %>%
  filter(year == 2013, 
     origin %in% c("JFK", "LGA", "EWR")) %>%
  
 \# Then I join the planes table with the flights table with left_join, by the variable "tailnum", which they have in common
  left_join(planes, 
       by = "tailnum", 
       suffix = c("_flights", "_planes")) %>%
 
 \# I am getting rid of the planes that don't have a manufacture year
  filter(!is.na(year_planes)) %>%
 
 \# I now arrange the planes in ascending order by their year and use slice(1) to select the oldest plane
  arrange(year_planes) %>%
  slice(1) %>%
  select(tailnum, year_planes)
 
 print(oldest_plane)

\# A tibble: 1 × 2
  tailnum year_planes
  <chr>     <int>
 1 N381AA     1956

\# How many airplanes that flew from New York City are included in the planes table?
 
 \# I filter for the year 2013 and the NYC airports for origin
 planes_in_nyc <- flights %>%
  filter(year == 2013, 
     origin %in% c("JFK", "LGA", "EWR")) %>%
 
 \# I select the planes by their tailnumber and use the unique funcion to avoid repeats
  select(tailnum) %>%
  unique() %>%
 
  \# I match the tailnum column from both data frames and return only the rows from the unique tailnum values that have matches in the planes data
  semi_join(planes, by = "tailnum")
 
 \#I count the number of rows to get the number of planes that flew New York City airports 
 nrow(planes_in_nyc)

[1] 3322



## Problem 7: Use the nycflights13 to answer the following questions:

\-  What is the median arrival delay on a month-by-month basis in each airport?
 \-  For each airline, plot the median arrival delay for each month and origin airport.

\# What is the median arrival delay on a month-by-month basis in each airport?
 
 \# I group the data by month and origin and calculate the median arrival delay for each group. With the na.rm = TRUE argument I remove the missing values before calculating the median.
 flights %>%
  group_by(month, 
      origin) %>%
  summarise(median_arr_delay = median(arr_delay, 
                    na.rm = TRUE))

`summarise()` has grouped output by 'month'. You can override using the
 `.groups` argument.

\# A tibble: 36 × 3
 \# Groups:  month [12]
  month origin median_arr_delay
  <int> <chr>       <dbl>
 1   1 EWR          0
 2   1 JFK         -7
 3   1 LGA         -4
 4   2 EWR         -2
 5   2 JFK         -5
 6   2 LGA         -4
 7   3 EWR         -4
 8   3 JFK         -7
 9   3 LGA         -7
 10   4 EWR         -1
 \# ℹ 26 more rows

\# For each airline, plot the median arrival delay for each month and origin airport
 
 \# I first group the data by carrier, month and origin and calculate the median arrival delay for each group.
 flights %>%
  group_by(carrier, 
      month, 
       origin) %>%
  summarise(median_arr_delay = median(arr_delay, 
                    na.rm = TRUE)) %>%
  
 \# I do a line plot with month in the x axis and the median arrival delay in the y axis, select the carrier variable as the group and making the colors different for the carriers. I use facet wrap to create separate subplots for each origin airport. 
  ggplot(aes(x = month, 
       y = median_arr_delay, 
       group = carrier, 
       color = carrier)) +
  geom_line() +
  facet_wrap(~origin) +
  labs(x = "Month", 
    y = "Median Arrival Delay (minutes)",
    title = "Median Arrival Delay by Month and Origin for Each Airline",
    color = "Airline") +
  theme_minimal()

`summarise()` has grouped output by 'carrier', 'month'. You can override using
 the `.groups` argument.

![img](file:///C:/Users/c14cc/AppData/Local/Temp/msohtmlclip1/01/clip_image008.png)



## Problem 8: Let’s take a closer look at what carriers service the route to San Francisco International (SFO). Join the flights and airlines tables and count which airlines flew the most to SFO. Produce a new dataframe, fly_into_sfo that contains three variables: the name of the airline, e.g., United Air Lines Inc. not UA, the count (number) of times it flew to SFO, and the percent of the trips that that particular airline flew to SFO.

fly_into_sfo <- flights %>%
  
 \# I filter the flights for those that flew to San Francisco. I then left join this with the airlines data frame, matching the carrier column from both data frames.
  filter(dest == 'SFO') %>%
  left_join(airlines, 
       by = c("carrier" = "carrier")) %>%
 
 \# I group by the name of the plane and count the number of rows.
  group_by(name) %>%
  summarise(count = n()) %>%
  
 \# I add a new column called percent to the data frame, which calculates the percentage of flights for each airline. This gives the percentage representation of each airline's flights to SFO and assigns it to fly_into_sfo.
  mutate(percent = count / sum(count) * 100)
 
 print(fly_into_sfo)

\# A tibble: 5 × 3
  name          count percent
  <chr>         <int>  <dbl>
 1 American Airlines Inc. 1422  10.7 
 2 Delta Air Lines Inc.  1858  13.9 
 3 JetBlue Airways     1035  7.76
 4 United Air Lines Inc.  6819  51.2 
 5 Virgin America     2197  16.5 

And here is some bonus ggplot code to plot your dataframe

fly_into_sfo %>% 
  
  \# sort 'name' of airline by the numbers it times to flew to SFO
  mutate(name = fct_reorder(name, count)) %>% 
  
  ggplot() +
  
  aes(x = count, 
    y = name) +
  
  \# a simple bar/column plot
  geom_col() +
  
  \# add labels, so each bar shows the % of total flights 
  geom_text(aes(label = percent),
       hjust = 1, 
       colour = "white", 
       size = 5)+
  
  \# add labels to help our audience 
  labs(title="Which airline dominates the NYC to SFO route?", 
    subtitle = "as % of total flights in 2013",
    x= "Number of flights",
    y= NULL) +
  
  theme_minimal() + 
  
  \# change the theme-- i just googled those , but you can use the ggThemeAssist add-in
  \# https://cran.r-project.org/web/packages/ggThemeAssist/index.html
  
  theme(#
   \# so title is left-aligned
   plot.title.position = "plot",
   
   \# text in axes appears larger    
   axis.text = element_text(size=12),
   
   \# title text is bigger
   plot.title = element_text(size=18)
    ) +
 
  \# add one final layer of NULL, so if you comment out any lines
  \# you never end up with a hanging `+` that awaits another ggplot layer
  NULL

![img](file:///C:/Users/c14cc/AppData/Local/Temp/msohtmlclip1/01/clip_image009.png)



## Problem 9: Let’s take a look at cancellations of flights to SFO. We create a new dataframe cancellations as follows

cancellations <- flights %>% 
  
  \# just filter for destination == 'SFO'
  filter(dest == 'SFO') %>% 
  
  \# a cancelled flight is one with no `dep_time` 
  filter(is.na(dep_time))

I want you to think how we would organise our data manipulation to create the following plot. No need to write the code, just explain in words how you would go about it.

I first filter for destination SFO, and then for the missing dep_time values to get the cancelled flights.I would group the date by departure airport and carrier. Then I can create a bar graph of the cancellations over time using facet wrap, with the cancellations on the y axis and the month on the x axis.

![img](file:///C:/Users/c14cc/AppData/Local/Temp/msohtmlclip1/01/clip_image011.png)



## Problem 10: On your own – Hollywood Age Gap

The website https://hollywoodagegap.com is a record of *THE AGE DIFFERENCE IN YEARS BETWEEN MOVIE LOVE INTERESTS*. This is an informational site showing the age gap between movie love interests and the data follows certain rules:

•      The two (or more) actors play actual love interests (not just friends, coworkers, or some other non-romantic type of relationship)

•      The youngest of the two actors is at least 17 years old

•      No animated characters

age_gaps <- readr::read_csv('https://raw.githubusercontent.com/rfordatascience/tidytuesday/master/data/2023/2023-02-14/age_gaps.csv')

Rows: 1155 Columns: 13
 ── Column specification ────────────────────────────────────────────────────────
 Delimiter: ","
 chr (6): movie_name, director, actor_1_name, actor_2_name, character_1_gend...
 dbl (5): release_year, age_difference, couple_number, actor_1_age, actor_2_age
 date (2): actor_1_birthdate, actor_2_birthdate
 
 ℹ Use `spec()` to retrieve the full column specification for this data.
 ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

glimpse(age_gaps)

Rows: 1,155
 Columns: 13
 $ movie_name     <chr> "Harold and Maude", "Venus", "The Quiet American", …
 $ release_year    <dbl> 1971, 2006, 2002, 1998, 2010, 1992, 2009, 1999, 199…
 $ director      <chr> "Hal Ashby", "Roger Michell", "Phillip Noyce", "Joe…
 $ age_difference   <dbl> 52, 50, 49, 45, 43, 42, 40, 39, 38, 38, 36, 36, 35,…
 $ couple_number   <dbl> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, …
 $ actor_1_name    <chr> "Ruth Gordon", "Peter O'Toole", "Michael Caine", "D…
 $ actor_2_name    <chr> "Bud Cort", "Jodie Whittaker", "Do Thi Hai Yen", "T…
 $ character_1_gender <chr> "woman", "man", "man", "man", "man", "man", "man", …
 $ character_2_gender <chr> "man", "woman", "woman", "woman", "man", "woman", "…
 $ actor_1_birthdate <date> 1896-10-30, 1932-08-02, 1933-03-14, 1930-09-17, 19…
 $ actor_2_birthdate <date> 1948-03-29, 1982-06-03, 1982-10-01, 1975-11-08, 19…
 $ actor_1_age    <dbl> 75, 74, 69, 68, 81, 59, 62, 69, 57, 77, 59, 56, 65,…
 $ actor_2_age    <dbl> 23, 24, 20, 23, 38, 17, 22, 30, 19, 39, 23, 20, 30,…

\# How is age_difference distributed? What's the 'typical' age_difference in movies?
 
 \# I create a histogram with the age difference in the x axis. I am also adding vertical lines that reflects the median and mean age differences. 
 ggplot(age_gaps, aes(x = age_difference)) +
  geom_histogram(binwidth = 1, fill = "pink", color = "black") +
  geom_vline(aes(xintercept=mean(age_difference)), size=0.75, color="red", clip="off")+
  geom_vline(aes(xintercept=median(age_difference)), size=0.75, color="purple")+
   geom_text(aes(x=10, label="Mean Age Difference", y=-5), colour="red", size=3)+
  theme_minimal() +
  geom_text(aes(x=7, label="Median Age Difference", y=-9), colour="purple", size=3)+
  theme_minimal() +
  labs(title = "The Age Difference Distribution is right-skewed, \n with the mean age difference being 10 and median 8", 
    x = "Age Difference", 
    y = "Frequency",
    )

Warning: Using `size` aesthetic for lines was deprecated in ggplot2 3.4.0.
 ℹ Please use `linewidth` instead.

Warning in geom_vline(aes(xintercept = mean(age_difference)), size = 0.75, :
 Ignoring unknown parameters: `clip`

![img](file:///C:/Users/c14cc/AppData/Local/Temp/msohtmlclip1/01/clip_image012.png)

\# The half plus seven\ rule. 
 
 \# I filter the data in the values to the ones that comply with the half plus seven rule formula and then count the number of rows in the filtered table.
 actors_complying_with_min_age <- age_gaps %>%
 filter(actor_1_age>=(actor_1_age/ 2) + 7) %>% 
  filter(actor_1_age<=(actor_2_age-7)*2) %>% 
  nrow() %>% 
  print()

[1] 829

\# I then calculate the percentage of actors that comply with the half plus seven rules by dividing the number of rows in the filtered table with the original table and multiplying by 100.
 pct_7_age_rule<- (actors_complying_with_min_age/nrow(age_gaps))*100
 
 \# I display the percentage to 2 decimal points.
 print(sprintf("The percentage of actors complying with the half plus seven rule is %.2f%%", pct_7_age_rule))

[1] "The percentage of actors complying with the half plus seven rule is 71.77%"

\# Which movie has the greatest number of love interests?
 
 \# I group the data by the movie names, count the number of couples in the movie and arrange in descending order. I use slice(1) to select the movie with the most couples.
 movie_with_most_love_interests <- age_gaps %>% 
  group_by(movie_name) %>% 
  summarise(couple_number=n()) %>% 
  arrange(desc(couple_number)) %>% 
  slice(1)
 
 \#Which actors/ actresses have the greatest number of love interests in this dataset?
 
 \# I combine the age gaps data frame with the actor_1_name and actor_2_name columns into a new column called actor_names
 age_gaps_names_merged <- age_gaps %>% 
  unite(actor_names, actor_1_name, actor_2_name, sep = " ")
 
 \# I group by the actor names and count the number of couples the actors are in, then arrange by descending order.
 actors_with_greates_love_interests<-age_gaps_names_merged %>% 
  group_by(actor_names) %>% 
  summarise(couple_number=n()) %>% 
   arrange(desc(couple_number))
 
 
 \#Is the mean/median age difference staying constant over the years (1935 - 2022)?
 
 \# I create a bar graph with the movie release year in the x axis and the mean age difference in the y axis.
 age_gaps %>% 
  ggplot(aes(x = release_year, y = mean(age_difference)))+
  geom_col(fill="purple", color="white")+
  theme_minimal()+
  labs(title = "The distribution of mean age difference over time is left \n skewed as the age difference has increased over time",
    x = "Release year",
    y = "Mean age difference")

![img](file:///C:/Users/c14cc/AppData/Local/Temp/msohtmlclip1/01/clip_image013.png)

\#How frequently does Hollywood depict same-gender love interests?
 
 \# I create a same gender variable that returns the number of times when the character 1's gender is the same as character 2's.
 age_gaps$same_gender <- age_gaps$character_1_gender == age_gaps$character_2_gender
 table(age_gaps$same_gender)


 FALSE TRUE 
 1132  23 

\# Calculate the proportion of same sex couples
 same_gender_pct <- mean(age_gaps$same_gender)*100
 
 print(sprintf("The percentage of same gender love interests in Hollywood is %.2f%%", same_gender_pct))

[1] "The percentage of same gender love interests in Hollywood is 1.99%"



# Deliverables

There is a lot of explanatory text, comments, etc. You do not need these, so delete them and produce a stand-alone document that you could share with someone. Render the edited and completed Quarto Markdown (qmd) file as a Word document (use the “Render” button at the top of the script editor window) and upload it to Canvas. You must be commiting and pushing tour changes to your own Github repo as you go along.



# Details

•      Who did you collaborate with: Nobody

•      Approximately how much time did you spend on this problem set: 5 hours

•      What, if anything, gave you the most trouble: I think I struggled a bit with figuring out how to approach the questions, particularly the few last problems.

**Please seek out help when you need it,** and remember the [*15-minute rule*](https://mam2022.netlify.app/syllabus/#the-15-minute-rule). You know enough R (and have enough examples of code from class and your readings) to be able to do this. If you get stuck, ask for help from others, post a question on Slack– and remember that I am here to help too!

As a true test to yourself, do you understand the code you submitted and are you able to explain it to someone else? Yes



# Rubric

13/13: Problem set is 100% completed. Every question was attempted and answered, and most answers are correct. Code is well-documented (both self-documented and with additional comments as necessary). Used tidyverse, instead of base R. Graphs and tables are properly labelled. Analysis is clear and easy to follow, either because graphs are labeled clearly or you’ve written additional text to describe how you interpret the output. Multiple Github commits. Work is exceptional. I will not assign these often.

8/13: Problem set is 60–80% complete and most answers are correct. This is the expected level of performance. Solid effort. Hits all the elements. No clear mistakes. Easy to follow (both the code and the output). A few Github commits.

5/13: Problem set is less than 60% complete and/or most answers are incorrect. This indicates that you need to improve next time. I will hopefully not assign these often. Displays minimal effort. Doesn’t complete all components. Code is poorly written and not documented. Uses the same type of plot for each graph, or doesn’t use plots appropriate for the variables being analyzed. No Github commits