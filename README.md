# Google-Data-Analytics-Capstone-Project-1

## INTRODUCTION

### Created to showcase my take on Google Capstone Case Study for Cyclistic Bike Share

### How does a bike-share navigate speedy success?

This capstone case study on Cyclistic bike share is part of Google Data Analytics Professional course by Google on Coursera

### The data exploration, cleaning and analysis are done using:

1. R Studio
2. Tableau

### Case Study Objective

Cyclistic, a bike share company in Chicago wants to understand how casual riders and annual members use Cyclistic bikes differently. These insights will be used to design a new marketing strategy to convert casual riders into annual member as the company believes that the company’s future success depends on maximizing the number of annual memberships

### Brief background and summary of case study company

* Cyclistic is a bike-sharing company, their portfolio features multiple programs and projects. 
* Cyclistic owns a fleet of more than 5,824 bicycles and maintains 692 docking stations. 
* Cyclistic also has a unique value proposition, where they offer reclining bikes, hand tricycles, and cargo bikes. This is part of a wider program that aims to make bike-share more inclusive to people with disabilities and riders who can’t use a standard two-wheeled bike. 
* The majority of users opt for traditional bikes, and about 8% of users opted for the assistive options. 
* Cyclistic users are more likely to ride for leisure, but about 30% use them to commute to work each day.
* Cyclistic operates mainly in the state of Illinois, Chicago City.

The director of marketing, Lily Moreno, believes that maximizing the number of annual members will be key to future growth. Rather than creating a marketing campaign that targets all-new customers, Moreno believes there is a very good chance to convert casual riders into members.

### Questions to explore relating to business task:

> #### Main: 
> How do annual members and casual riders use Cyclistic bikes differently?

>> #### Sub: 
>> 1. What are the biggest differences in behaviours between casual riders and annual members?
>> 2. Are the differences in behaviours the reasons why casual riders stay casual, and annual members are willing to maintain their subscription?
>> 3. What causes the differences in behaviours?

### Deliverables:
* Insights on users behaviours.
* Data Visualisation for easy understanding and punchline.
* RMD file for tracking and replication purposes.

### Data Sources
Historical bike trip data provided by Motivate International Inc. under licence from Divvy Bikes. (The datasets have a different name because Cyclistic is a fictional company for the purpose of the Google Data Analytic Capstone project). Personal identifiable information are not available due to data-privacy.

> Dataset was downloaded from https://divvy-tripdata.s3.amazonaws.com/index.html. For the purpose of this analysis, 12 months of data from May 2021 to April 2022 will be prepared and analysed. The most recent data available is April 2022. Total data size is approximately 1.61GB.

### Dataset was checked for credibility

* The dataset is assumed to be reliable (data is based on a fictitious entity), original, cited as it is provided under licence as above.
* Data is current as the most recent data used is April 2022
* There are missing data points for start station and end station and geographic latitude and longitude in the dataset therefore the data is not as comprehensive as it could have been. We will keep this in mind and account for these during data analysis.

### Documentation, Cleaning and Preparation of data for analysis
The combined size of all the 12 datasets is close to 1.61 GB. Data cleaning in spreadsheets will be time-consuming and slow compared to SQL or R. Chosed R simply because I could do both data wrangling and analysis/ visualizations in the same platform. It is also an opportunity for me to learn R better.

### Limitation/Assumptions made of data available

* No information on where users lives in the Cyclistic area of operations, this is due to data-privacy issues prohibit the use of users’ personally identifiable information.
* Analysis and insights will be limited on the casual rider’s behaviour as there are no data on types of purchase (single pass or full-day pass) and if there are multiple purchases from the same casual rider.

## DATA PREPARATION

### Packages used

> install.packages("tidyverse")
> <br>install.packages("lubridate")
> <br>install.packages("janitor")
> <br>install.packages("data.table")

### Libraries loaded

> library(tidyverse)
> <br>library(lubridate)
> <br>library(janitor)
> <br>library(data.table)

### Loading datasets

> tripdata_202105 <- read.csv("202105-divvy-tripdata.csv")
> <br>tripdata_202106 <- read.csv("202106-divvy-tripdata.csv")
> <br>tripdata_202107 <- read.csv("202107-divvy-tripdata.csv")
> <br>tripdata_202108 <- read.csv("202108-divvy-tripdata.csv")
> <br>tripdata_202109 <- read.csv("202109-divvy-tripdata.csv")
> <br>tripdata_202110 <- read.csv("202110-divvy-tripdata.csv")
> <br>tripdata_202111 <- read.csv("202111-divvy-tripdata.csv")
> <br>tripdata_202112 <- read.csv("202112-divvy-tripdata.csv")
> <br>tripdata_202201 <- read.csv("202201-divvy-tripdata.csv")
> <br>tripdata_202202 <- read.csv("202202-divvy-tripdata.csv")
> <br>tripdata_202203 <- read.csv("202203-divvy-tripdata.csv")
> <br>tripdata_202204 <- read.csv("202204-divvy-tripdata.csv")

### colnames() for column names consistency

> colnames(tripdata_202204)
> <br>colnames(tripdata_202203)
> <br>colnames(tripdata_202202)
> <br>colnames(tripdata_202201)
> <br>colnames(tripdata_202112)
> <br>colnames(tripdata_202111)
> <br>colnames(tripdata_202110)
> <br>colnames(tripdata_202109)
> <br>colnames(tripdata_202108)
> <br>colnames(tripdata_202107)
> <br>colnames(tripdata_202106)
> <br>colnames(tripdata_202105)

### str() for data structure and data types consistency

> str(tripdata_202204)
> <br>str(tripdata_202203)
> <br>str(tripdata_202202)
> <br>str(tripdata_202201)
> <br>str(tripdata_202112)
> <br>str(tripdata_202111)
> <br>str(tripdata_202110)
> <br>str(tripdata_202109)
> <br>str(tripdata_202107)
> <br>str(tripdata_202106)
> <br>str(tripdata_202105)

#### *Note - data type for started_at and ended_at were in chr, and needs to be changed to dttm. dateTime format of these 2 column are not consistent throughout the checks as well, I have decided to align all data to y-m-d HMS format.*

### Cleanup Required - Changing dateTime format for tripdata_202105, tripdata_202203 and tripdata_202204

> tripdata_202105_processed <- tripdata_202105
> <br> tripdata_202203_processed <- tripdata_202203
> <br> tripdata_202204_processed <- tripdata_202204
> <br>
> <br> tripdata_202105_processed <- tripdata_202105_processed %>% mutate(across(c(started_at, ended_at), dmy_hm))
> <br> tripdata_202203_processed <- tripdata_202203_processed %>% mutate(across(c(started_at, ended_at), dmy_hm))
> <br> tripdata_202204_processed <- tripdata_202204_processed %>% mutate(across(c(started_at, ended_at), dmy_hm))

### Cleanup Required - Changing datatype from chr to dttm for the rest of the datasets

> tripdata_202106_processed <- tripdata_202106 %>% mutate(across(c(started_at, ended_at), ~ as.POSIXct(.x, format = "%Y-%m-%d %H:%M:%S") %>% ymd_hms())) 
> <br> tripdata_202107_processed <- tripdata_202107 %>% mutate(across(c(started_at, ended_at), ~ as.POSIXct(.x, format = "%Y-%m-%d %H:%M:%S") %>% ymd_hms()))
> <br> tripdata_202108_processed <- tripdata_202108 %>% mutate(across(c(started_at, ended_at), ~ as.POSIXct(.x, format = "%Y-%m-%d %H:%M:%S") %>% ymd_hms()))
> <br> tripdata_202109_processed <- tripdata_202109 %>% mutate(across(c(started_at, ended_at), ~ as.POSIXct(.x, format = "%Y-%m-%d %H:%M:%S") %>% ymd_hms()))
> <br> tripdata_202110_processed <- tripdata_202110 %>% mutate(across(c(started_at, ended_at), ~ as.POSIXct(.x, format = "%Y-%m-%d %H:%M:%S") %>% ymd_hms()))
> <br> tripdata_202111_processed <- tripdata_202111 %>% mutate(across(c(started_at, ended_at), ~ as.POSIXct(.x, format = "%Y-%m-%d %H:%M:%S") %>% ymd_hms()))
> <br> tripdata_202112_processed <- tripdata_202112 %>% mutate(across(c(started_at, ended_at), ~ as.POSIXct(.x, format = "%Y-%m-%d %H:%M:%S") %>% ymd_hms()))
> <br> tripdata_202201_processed <- tripdata_202201 %>% mutate(across(c(started_at, ended_at), ~ as.POSIXct(.x, format = "%Y-%m-%d %H:%M:%S") %>% ymd_hms()))
> <br> tripdata_202202_processed <- tripdata_202202 %>% mutate(across(c(started_at, ended_at), ~ as.POSIXct(.x, format = "%Y-%m-%d %H:%M:%S") %>% ymd_hms()))

### Combine datasets into one dataframe

> all_trips <- <br>bind_rows(tripdata_202204_processed,tripdata_202203_processed,tripdata_202202_processed,tripdata_202201_processed,tripdata_202112_processed,tripdata_202111_processed,tripdata_202110_processed,tripdata_202109_processed,tripdata_202108_processed,tripdata_202107_processed,tripdata_202106_processed,tripdata_202105_processed)

## DATA PROCESSING

### Quick glimpse to identify if renaming are required

> $ ride_id            <chr> "A847FADBBC638E45", "5405B80E996FF60D", "5DD24A79A4…
> <br>$ rideable_type      <chr> "docked_bike", "docked_bike", "docked_bike", "docke…
> <br>$ started_at         <dttm> 2020-04-26 17:45:14, 2020-04-17 17:08:54, 2020-04-…
> <br>$ ended_at           <dttm> 2020-04-26 18:12:03, 2020-04-17 17:17:03, 2020-04-…
> <br>$ start_station_name <chr> "Eckhart Park", "Drake Ave & Fullerton Ave", "McClu…
> <br>$ start_station_id   <chr> "86", "503", "142", "216", "125", "173", "35", "434…
> <br>$ end_station_name   <chr> "Lincoln Ave & Diversey Pkwy", "Kosciuszko Park", "…
> <br>$ end_station_id     <chr> "152", "499", "255", "657", "323", "35", "635", "38…
> <br>$ start_lat          <dbl> 42.01913, 41.85308, 41.87184, 41.85308, 41.87181, 41.884~
> <br>$ start_lng          <dbl> -87.67353, -87.63193, -87.64664, -87.63193, -87.64657, -~
> <br>$ end_lat            <dbl> 42.05294, 41.88189, 41.88189, 41.86749, 41.88224, 41.879~
> <br>$ end_lng            <dbl> -87.67345, -87.64879, -87.64879, -87.63219, -87.64107, -~
> <br>$ member_casual      <chr> "member", "member", "member", "member", "casual", "…
  
### Rename columns for better readability
 
> all_trips <- all_trips %>% 
<br> rename(ride_type = rideable_type,start_time = started_at,end_time = ended_at,customer_type = member_casual)
  
### Add new columns that will be used for agregation.

> *Day of the week the trip started*
> <br> all_trips$day_of_the_week <- format(as.Date(all_trips$start_time),'%a')
> <br>
> <br> *Month when the trip started*
> <br> all_trips$month <- format(as.Date(all_trips$start_time),'%b_%y')
> <br>
> <br> *Trip duration in min*
> <br> all_trips$trip_duration <- (as.double(difftime(all_trips$end_time, all_trips$start_time)))/60
>> *Time of the day when the trip started*
>> <br> *Note - two-step conversion is needed to get hours-minutes-seconds in POSIXct for ggplot2*
>> <br> all_trips$time <- format(all_trips$start_time, format = "%H:%M")
>> <br> all_trips$time <- as.POSIXct(all_trips$time, format = "%H:%M")

### Check if any trip duration is in the negative.

> nrow(subset(all_trips,trip_duration < 0))
> <br> [1] 139

### Check if any testrides were made

> nrow(subset(all_trips, start_station_name %like% "TEST"))
> <br>[1] 0
> <br> nrow(subset(all_trips, start_station_name %like% "test"))
> <br>[1] 0
> <br> nrow(subset(all_trips, start_station_name %like% "Test"))
> <br>[1] 1

### Remove irrelavant data

> *negative trip durations*
> <br> all_trips_v2 <- all_trips[!(all_trips$trip_duration < 0),]
> <br>
> <br> *remove test rides*
> <br> all_trips_v2<- all_trips_v2[!((all_trips_v2$start_station_name %like% "Test" | all_trips_v2$start_station_name %like% "test")),]

### Check if there is only two customer types

> table(all_trips_v2$customer_type)
>> casual  member 
>> <br> 2536297 3221114  

## ANALYSE AND GAIN INSIGHTS

### summary of trip_duration for all trips
summary(all_trips_v2$trip_duration)
| Min. | 1st Qu. | Median | Mean | 3rd Qu. | Max. | 
|---|---|---|---|---|---|
| 0.0 | 6.43 | 11.52 | 21.14 | 21.00 | 55944.15 |

### summary of trip_duration by customer_type
all_trips_v2 %>%
<br> group_by(customer_type) %>%
<br> summarise(min_trip_duration = min(trip_duration),max_trip_duration = max(trip_duration),
<br> median_trip_duration = median(trip_duration), mean_trip_duration = mean(trip_duration))

A tibble: 2 x 5

  | customer_typ | min_trip_duration | max_trip_duration | median_trip_dur~ | mean_trip_durat~ |
|--------------|-------------------|-------------------|------------------|------------------|
| <chr>        | <dbl>             | <dbl>             | <dbl>            | <dbl>            |
| 1 casual     | 0                 | 55944.            | 15.6             | 31.3             |
| 2 member     | 0                 | 1560.             | 9.1              | 13.1             |

*Note - member mean trip duration (13.1) is lower than all trip mean trip duration (21.14), whereas casual riders mean trip duration (31.3) is higher than the the mean trip duration of all trips. This tells us that casual riders statistically take the bikes out for a longer duration compared to members over sample size.*

### Total number of trips by customer type and day of the week

*Order time and month column for easier reference*
> all_trips_v2$day_of_the_week <- ordered(all_trips_v2$day_of_the_week, levels=c("Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"))
><br> 
><br> all_trips_v2$month <- ordered(all_trips_v2$month, levels=c("May_21", "Jun_21", "Jul_21", "Aug_21", "Sep_21", "Oct_21", "Nov_21", "Dec_21", "Jan_22", "Feb_22", "Mar_22", "Apr_22"))

*Summarise into table*

> <p> all_trips_v2 %>% 
> <br> group_by(customer_type, day_of_the_week) %>%  
> <br> summarise(number_of_rides = n(),average_duration_mins = mean(trip_duration)) %>% 
> <br> arrange(customer_type, desc(number_of_rides))

*A tibble: 14 x 4*
*Groups:   customer_type [2]*
|   customer_type |day_of_the_week |number_of_rides |average_duration_mins|
|-----------------|-----------------|---------------|---------------------|
|   <chr>         |<ord>            |         <int> |                <dbl>|
| 1 casual        |Sat              |        558610 |                 34.2|
| 2 casual        |Sun              |        476993 |                 37.0|
| 3 casual        |Fri              |        358197 |                 29.2|
| 4 casual        |Thu              |        298061 |                 27.9|
| 5 casual        |Mon              |        289026 |                 31.1|
| 6 casual        |Wed              |        284866 |                 27.1|
| 7 casual        |Tue              |        270544 |                 26.5|
| 8 member        |Wed              |        506935 |                 12.4|
| 9 member        |Tue              |        498679 |                 12.3|
|10 member        |Thu              |        485840 |                 12.4|
|11 member        |Fri              |        453278 |                 12.9|
|12 member        |Mon              |        445628 |                 12.7|
|13 member        |Sat              |        442737 |                 14.8|
|14 member        |Sun              |        388017 |                 15.1|

*Visualisation 1*

><p> all_trips_v2 %>%  
><br>     group_by(customer_type, day_of_the_week) %>% 
><br>     summarise(number_of_rides = n()) %>% 
><br>     arrange(customer_type, day_of_the_week)  %>% 
><br>     ggplot(aes(x = day_of_the_week, y = number_of_rides, fill = customer_type)) +
><br>     labs(title ="Total trips by customer type Vs. Day of the week") +
><br>     geom_col(width=0.5, position = position_dodge(width=0.5)) +
><br>     scale_y_continuous(labels = function(x) format(x, scientific = FALSE))

![Total trips by customer type Vs  Day of the week](https://user-images.githubusercontent.com/105503334/169847617-d0521376-e6e1-46f6-964a-32a6119686f8.png)

*Observation - Casual riders see the highest usage on weekends (Saturdays and Sundays) whereas Members are fairly consistent throughout week, although with noticeable lower usages on Sundays. Members are the the dominant users on weekdays whereas Casual Riders are the dominant users on weekends.*

### Average number of trips by customer type and month

><p> unique(all_trips$month)
><br>
><br> "Apr_22" "Mar_22" "Feb_22" "Jan_22" "Dec_21" "Nov_21" "Oct_21" "Sep_21" "Aug_21" "Jul_21" "Jun_21" "May_21"
><br> 
><br> all_trips_v2 %>% 
><br>   group_by(customer_type, month) %>%  
><br>   summarise(number_of_rides = n(),`average_duration_(mins)` = mean(trip_duration)) %>% 
><br>   arrange(customer_type,desc(number_of_rides))%>%View()

![Average number of trips by customer type and month table](https://user-images.githubusercontent.com/105503334/169851198-6e9c7ecc-a88a-489b-9d93-b666cf8d3983.png)

*Visualisation*

><p> all_trips_v2 %>%  
><br> group_by(customer_type, month) %>% 
><br> summarise(number_of_rides = n()) %>% 
><br> arrange(customer_type, month)  %>% 
><br> ggplot(aes(x = month, y = number_of_rides, fill = customer_type)) +
><br> labs(title ="Total trips by customer type Vs. Month") +
><br> theme(axis.text.x = element_text(angle = 30)) +
><br> geom_col(width=0.5, position = position_dodge(width=0.5)) +
><br> scale_y_continuous(labels = function(x) format(x, scientific = FALSE))

![Total trips by customer type Vs  Month](https://user-images.githubusercontent.com/105503334/169853159-14f28653-d9a4-4836-9b22-07dea0663b4e.png)

*Observation - June, July, Auguest and September are the most busy months of the year, with both members and casual riders exceeding 350,000 trips. We could draw a correlation to seasonal effect, in which the period belongs to late spring and summer. Generally we can observe that summer commands the highest ridership whereas winter commands the lowest ridership.*

*Visualisation*

><p> all_trips_v2 %>%  
><br>  group_by(customer_type, day_of_the_week) %>% 
><br>  summarise(average_trip_duration = mean(trip_duration)) %>%
><br>  ggplot(aes(x = day_of_the_week, y = average_trip_duration, fill = customer_type)) +
><br>  geom_col(width=0.5, position = position_dodge(width=0.5)) + 
><br>  labs(title ="Average trip duration by customer type Vs. Day of the week")

![Average trip duration by customer type Vs  Day of the week](https://user-images.githubusercontent.com/105503334/169939956-05218022-81df-472f-8b66-1f649b42271f.png)

*Observation - The average trip duration of a casual rider is more than twice that of a member. this however does not equate to double the distance travelled. It is also indicated that both members and casual riders have longer trip durations over weekends.*

*Visualisation*

><p> all_trips_v2 %>%  
><br>  group_by(customer_type, month) %>% 
><br>  summarise(average_trip_duration = mean(trip_duration)) %>%
><br>  ggplot(aes(x = month, y = average_trip_duration, fill = customer_type)) +
><br>  geom_col(width=0.5, position = position_dodge(width=0.5)) + 
><br>  labs(title ="Average trip duration by customer type Vs. Month") +
><br>  theme(axis.text.x = element_text(angle = 30))

![Average trip duration by customer type Vs  Month](https://user-images.githubusercontent.com/105503334/169943087-dd1110c5-aa15-44f6-99dd-6413feee490c.png)

*Observation - Average trip duration of member riders is anywhere between 10-15 minutes throughout the year, while average trip duration of casual members ranges within 38~23 minutes to more than an hour depending on time of the year. It is does not seems to be a direct correlation between the months and trip durations.*

*Visualisation*

><p> all_trips_v2 %>%  
><br>  group_by(customer_type, time) %>% 
><br>  summarise(number_of_trips = n()) %>%
><br>  ggplot(aes(x = time, y = number_of_trips, color = customer_type, group = customer_type)) +
><br>  geom_line() +
><br>  scale_x_datetime(date_breaks = "1 hour", minor_breaks = NULL,
><br>                   date_labels = "%H:%M", expand = c(0,0)) +
><br>  theme(axis.text.x = element_text(angle = 90)) +
><br>  labs(title ="Demand over 24 hours of a day", x = "Time of the day")

![Demand over 24 hours of a day](https://user-images.githubusercontent.com/105503334/169946121-6996e575-b5f8-4d5b-99f4-c36aa044db52.png)

*Observation - For both casual riders and members, they both experience peak demand hours from 4 to 7pm. The distinction between the two though, is that casual riders steadily picks up in demand as the days passed, peaking at 5pm, whilst members demands picks up early from 5 to 7am, plateau from 7 to 9am before dropping demands from 9 to 10am before slowly picking up demands again till peaking at 5pm. It is possible to draw a correlation to in members demands to office hours.*

*Visualisation*

Find and count unique start_lat and start_lng for casual riders (Marketing efforts are meant for converting casual riders)

> all_trips_v2_Casual <- all_trips_v2[!(all_trips_v2$customer_type %like% "member"),]
><br> start_lat_long_casual <- all_trips_v2_Casual %>% count(start_lat,start_lng)

Extract and save start_lat_long_casual as CSV file to be used in Tableau

> write.csv(start_lat_long_casual,"D:\\Data Analytics Case Study 1\\Projects\\start_lat_long_casual.csv", row.names = FALSE)

Upload start_lat_long_casual.csv into Tableau and set the following parameters

> Set start_lng as columns
><br> Set start_lat as Rows
><br> Set N(No. of times the same starting points was recorded) as Size

![image](https://user-images.githubusercontent.com/105503334/170880748-512a3eb0-d6fa-4fcd-8f58-bf2739d8d464.png)

*Observation - We can safely determine that Downtown Chicago has the highest ridership take up rate and north Chicago rank second. It is interesting to note that Chicago University rank third in ridership take up rate, separate from the rank 1 and 2. Starting points are also concentrated in clear consolidated areas.*

*Visualisation*

Find and count unique end_lat and end_lng for casual riders (Marketing efforts are meant for converting casual riders)

> end_lat_long_casual <- all_trips_v2_Casual %>% count(end_lat,end_lng)

Extract and save end_lat_long_casual as CSV file to be used in Tableau

> write.csv(end_lat_long_casual,"D:\\Data Analytics Case Study 1\\Projects\\end_lat_long_casual.csv", row.names = FALSE)

Upload end_lat_long_casual.csv into Tableau and set the following parameters

> Set end_lng as columns
><br> Set end_lat as Rows
><br> Set N(No. of times the same end points was recorded) as Size

![image](https://user-images.githubusercontent.com/105503334/170880458-b127bdf1-ec48-4f75-b040-74a982062f1b.png)

*Observation - We can safely determine that Downtown Chicago has the highest ridership end destination and north Chicago rank second. unsurprisingly, Chicago University takes up third place. However with end trip, Starting points are also concentrated in clear consolidated areas. We could oso derived that both Start and End points are concentrated in the same locale, this makes it evident the areas ranked 1, 2 and 3 should be targeted to have the most reach to the intended casual riders.*

 
