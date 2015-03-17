---
title: "Reproducible Research: Step activity analysis"
author: "Natalia Chodelski"
date: "13 April 2015"
output: html_document
---
<br>
#### Loading and pre-processing the data  


```r
# set working directory to the folder where i have 'activity.csv'
setwd("/Users/Natalia/Coding/Reproducible_Research/RepData_PeerAssessment1/")

# load with read.csv()
activity <- read.csv("activity.csv", header = T)
```
<br>  

  
I processed the data by turning the given dates and time intervals into r-recognizable date-time format.

str_pad() added zeros to the front of shorter time intervals so all time intervals were in 4 digit 24 hr time format. I then pasted the time onto the dates, and processed into r-recognizable times with strptime() 
 


```r
# pad time intervals with zeros 
library(stringr)
activity$time <- str_pad(activity$interval, 4, pad = "0")

# join time and date together, then process 
activity$datetime <- paste(activity$date, activity$time)
activity$R_time <- strptime(activity$datetime, format = "%Y-%m-%d %H%M")
```
<br>  
  

I calculated the mean  number of steps taken per day, using tapply, with simplify = TRUE to the result to an array.  I created a data frame by using column-bind to join an array of the unique dates to the mean number of steps.  I lastly assigned tidy column names.


```r
# calculating means and making data frame
mean_steps <- tapply(X = activity$steps, INDEX = activity$date, FUN = mean, simplify = T)

mean_steps_table <- cbind(unique(as.data.frame(activity$date)), mean_steps)

# the data frame needs nice column names
colnames(mean_steps_table) <- c("Date measured","Mean Steps")
```
<br>  

I used the xtable package to create and print a tidy HTML table of mean steps per day in the markdown document.


```r
library(xtable)

table <- xtable(mean_steps_table, align = c("c","c","c"))
print(table, type="html", include.rownames = FALSE)
```

<!-- html table generated in R 3.1.2 by xtable 1.7-4 package -->
<!-- Tue Mar 17 12:09:05 2015 -->
<table border=1>
<tr> <th> Date measured </th> <th> Mean Steps </th>  </tr>
  <tr> <td align="center"> 2012-10-01 </td> <td align="center">  </td> </tr>
  <tr> <td align="center"> 2012-10-02 </td> <td align="center"> 0.44 </td> </tr>
  <tr> <td align="center"> 2012-10-03 </td> <td align="center"> 39.42 </td> </tr>
  <tr> <td align="center"> 2012-10-04 </td> <td align="center"> 42.07 </td> </tr>
  <tr> <td align="center"> 2012-10-05 </td> <td align="center"> 46.16 </td> </tr>
  <tr> <td align="center"> 2012-10-06 </td> <td align="center"> 53.54 </td> </tr>
  <tr> <td align="center"> 2012-10-07 </td> <td align="center"> 38.25 </td> </tr>
  <tr> <td align="center"> 2012-10-08 </td> <td align="center">  </td> </tr>
  <tr> <td align="center"> 2012-10-09 </td> <td align="center"> 44.48 </td> </tr>
  <tr> <td align="center"> 2012-10-10 </td> <td align="center"> 34.38 </td> </tr>
  <tr> <td align="center"> 2012-10-11 </td> <td align="center"> 35.78 </td> </tr>
  <tr> <td align="center"> 2012-10-12 </td> <td align="center"> 60.35 </td> </tr>
  <tr> <td align="center"> 2012-10-13 </td> <td align="center"> 43.15 </td> </tr>
  <tr> <td align="center"> 2012-10-14 </td> <td align="center"> 52.42 </td> </tr>
  <tr> <td align="center"> 2012-10-15 </td> <td align="center"> 35.20 </td> </tr>
  <tr> <td align="center"> 2012-10-16 </td> <td align="center"> 52.38 </td> </tr>
  <tr> <td align="center"> 2012-10-17 </td> <td align="center"> 46.71 </td> </tr>
  <tr> <td align="center"> 2012-10-18 </td> <td align="center"> 34.92 </td> </tr>
  <tr> <td align="center"> 2012-10-19 </td> <td align="center"> 41.07 </td> </tr>
  <tr> <td align="center"> 2012-10-20 </td> <td align="center"> 36.09 </td> </tr>
  <tr> <td align="center"> 2012-10-21 </td> <td align="center"> 30.63 </td> </tr>
  <tr> <td align="center"> 2012-10-22 </td> <td align="center"> 46.74 </td> </tr>
  <tr> <td align="center"> 2012-10-23 </td> <td align="center"> 30.97 </td> </tr>
  <tr> <td align="center"> 2012-10-24 </td> <td align="center"> 29.01 </td> </tr>
  <tr> <td align="center"> 2012-10-25 </td> <td align="center"> 8.65 </td> </tr>
  <tr> <td align="center"> 2012-10-26 </td> <td align="center"> 23.53 </td> </tr>
  <tr> <td align="center"> 2012-10-27 </td> <td align="center"> 35.14 </td> </tr>
  <tr> <td align="center"> 2012-10-28 </td> <td align="center"> 39.78 </td> </tr>
  <tr> <td align="center"> 2012-10-29 </td> <td align="center"> 17.42 </td> </tr>
  <tr> <td align="center"> 2012-10-30 </td> <td align="center"> 34.09 </td> </tr>
  <tr> <td align="center"> 2012-10-31 </td> <td align="center"> 53.52 </td> </tr>
  <tr> <td align="center"> 2012-11-01 </td> <td align="center">  </td> </tr>
  <tr> <td align="center"> 2012-11-02 </td> <td align="center"> 36.81 </td> </tr>
  <tr> <td align="center"> 2012-11-03 </td> <td align="center"> 36.70 </td> </tr>
  <tr> <td align="center"> 2012-11-04 </td> <td align="center">  </td> </tr>
  <tr> <td align="center"> 2012-11-05 </td> <td align="center"> 36.25 </td> </tr>
  <tr> <td align="center"> 2012-11-06 </td> <td align="center"> 28.94 </td> </tr>
  <tr> <td align="center"> 2012-11-07 </td> <td align="center"> 44.73 </td> </tr>
  <tr> <td align="center"> 2012-11-08 </td> <td align="center"> 11.18 </td> </tr>
  <tr> <td align="center"> 2012-11-09 </td> <td align="center">  </td> </tr>
  <tr> <td align="center"> 2012-11-10 </td> <td align="center">  </td> </tr>
  <tr> <td align="center"> 2012-11-11 </td> <td align="center"> 43.78 </td> </tr>
  <tr> <td align="center"> 2012-11-12 </td> <td align="center"> 37.38 </td> </tr>
  <tr> <td align="center"> 2012-11-13 </td> <td align="center"> 25.47 </td> </tr>
  <tr> <td align="center"> 2012-11-14 </td> <td align="center">  </td> </tr>
  <tr> <td align="center"> 2012-11-15 </td> <td align="center"> 0.14 </td> </tr>
  <tr> <td align="center"> 2012-11-16 </td> <td align="center"> 18.89 </td> </tr>
  <tr> <td align="center"> 2012-11-17 </td> <td align="center"> 49.79 </td> </tr>
  <tr> <td align="center"> 2012-11-18 </td> <td align="center"> 52.47 </td> </tr>
  <tr> <td align="center"> 2012-11-19 </td> <td align="center"> 30.70 </td> </tr>
  <tr> <td align="center"> 2012-11-20 </td> <td align="center"> 15.53 </td> </tr>
  <tr> <td align="center"> 2012-11-21 </td> <td align="center"> 44.40 </td> </tr>
  <tr> <td align="center"> 2012-11-22 </td> <td align="center"> 70.93 </td> </tr>
  <tr> <td align="center"> 2012-11-23 </td> <td align="center"> 73.59 </td> </tr>
  <tr> <td align="center"> 2012-11-24 </td> <td align="center"> 50.27 </td> </tr>
  <tr> <td align="center"> 2012-11-25 </td> <td align="center"> 41.09 </td> </tr>
  <tr> <td align="center"> 2012-11-26 </td> <td align="center"> 38.76 </td> </tr>
  <tr> <td align="center"> 2012-11-27 </td> <td align="center"> 47.38 </td> </tr>
  <tr> <td align="center"> 2012-11-28 </td> <td align="center"> 35.36 </td> </tr>
  <tr> <td align="center"> 2012-11-29 </td> <td align="center"> 24.47 </td> </tr>
  <tr> <td align="center"> 2012-11-30 </td> <td align="center">  </td> </tr>
   </table>
<br>
   
I used tapply to calculate the total number of steps taken per day, and specified simplify = TRUE so that the result would be returned as an array.   

I examined the variation in the number of steps taken on different days by plotting a histogram with the base plotting function hist().



```r
total_steps <- tapply(X = activity$steps, INDEX = activity$date, FUN = sum, simplify = T)

# create the histogram
hist(total_steps, breaks = 40, col="orange",  xlab =("Steps per day"), ylab = ("Number of days in frequency range"), main = ("Frequency histogram: total steps taken per day"))
```

![plot of chunk histogram1](figure/histogram1-1.png) 
<br>  

I then calculated the mean and median total number of steps. I had to use na.rm = TRUE since there were NA values for the number of steps on some days.


```r
mean_step_amount <- as.integer(mean(total_steps, na.rm = TRUE))
median_step_amount <- median(total_steps, na.rm = TRUE)
```
<br>  

The mean number of steps the subject walked per day was 10766, while the median was 10765 steps per day.   


I then used lapply to calculate the average number of steps taken in each 5-minute time interval, for all days.  I created a time series plot showing the mean number of steps taken over the course of an average day. 

I had to make a vector of the first 288 time intervals from my r-formatted time column (produced in pre-processing, to use as the x values (because the raw interval values have a large jump from 0055 - 1000 each hour, which would negativly affect the acccuracy of the graph).


```r
# the average step values per time interval
average_per_time <- tapply(X = activity$steps, INDEX =  activity$interval, FUN = mean, na.rm = TRUE, simplify = TRUE)

# Time intervals to use for graphing
real_time_intervals <- activity$R_time[1:288]

# graph data
plot(real_time_intervals, average_per_time, type = "l", col = "darkviolet", lwd = 2.2,  xlab =("Time interval (minutes)"), ylab = ("Average number of steps"), cex.main = 1, cex.lab = 1.2) #, xaxt = "n")
```

![plot of chunk timeseriesplot1](figure/timeseriesplot1-1.png) 

```r
# find the max average activitiy: sort interval averages by total number of steps
max_num_steps <- max(average_per_time)

# and find and record the time interval at which this max number of steps occured 
max_interval <- names(average_per_time[average_per_time == max_num_steps])
```

On average, the subject took the most steps each day at 835, which is the five minute period from 8:35 to 8:40 am. This might be when the subject walked to work, or perhaps took an early morning walk. 
<br>  


#### Imputing missing values



```r
# to count number of NA's in step data, create and store a T/F logical vector using is.na
is_an_na <- is.na(activity$steps)

# then measure the number of items the logical vector that were TRUE (ie were NA values)
number_na <- length(is_an_na[is_an_na == TRUE])
```
<br> 

Some entire days were missing data on the number of steps taken. The total number of missing values in the data set was 2304.

My strategy for replacing the missign values was cycle through the steps column of the data using a for loop, checking to see if each value was an NA.  For any value that was missing, I replaced it with the average total number of steps for that time interval. 

I also ran some checks after to ensure that all missing values had been filled. 


```r
# average_per_time is an array, i need it to be a dataframe to use it properly for replacment
averages <- data.frame(rownames(average_per_time), average_per_time)
colnames(averages) <- c("interval", "average_steps")

# making a new data set  with activity data. the NAs in this will be filled in, leaving the original activity data set untouched
activity_no_NAs <- activity

# keep track of how many NAs were replaced
count_replaced <- 0

# store length of dataset for the for-loop
length_data <- length(activity_no_NAs$steps)

for (x in (1:length_data)) {
     if (is.na(activity_no_NAs$steps[x]) == TRUE) {
          replacment_value <- (averages$average_steps[averages$interval == activity_no_NAs$interval[x]])
          activity_no_NAs$steps[x] <-  as.vector(replacment_value)
          count_replaced <<- count_replaced + 1
     } 
}

## checks: were the correct number of NAs were found and replaced?  (there were 2304 NA values)
print(count_replaced)
```

```
## [1] 2304
```
<br>

I calculated the mean and median total number of steps taken each day, using the new dataset with all missing values filled in. 


```r
# calculating the total steps taken each day
total_steps_replacement <- tapply(X = activity_no_NAs$steps, INDEX = activity_no_NAs$date, FUN = sum, simplify = T)

# finding the mean and median number of steps taken each day
mean_steps_replacement <- as.integer(mean(total_steps_replacement))
median_steps_replacement <- median(total_steps_replacement)
```

The mean number of steps for the original data was 10766 steps, while the mean number of steps for the NA's replaced data set is 10766 steps."

The median for original data was 10765 steps, the median for the replaced data set is 1.0766189 &times; 10<sup>4</sup> steps.

The mean and median for the total number of steps has remained the same after replacing the NA values. I believe this is because I used overall means from the data to fill in the missing values, and therefore my additions display the same mean and median as the previous data. 

<br>
To examine whether the frequency of the total number of steps taken per day had changed, I created a frequency histogram of the total steps per day from the filled-in dataset.  


```r
hist(total_steps_replacement, breaks = 40, col="lightblue", xlab =("Steps per day"), ylab = ("Number of days in step freq range"), main = ("Frequency histogram: total steps taken per day (NAs replaced)"))
```

![plot of chunk histogram2](figure/histogram2-1.png) 
<br>

Replacing the missing values with the average step values per time interval  has changed the overall frequency of step amounts.   The number of days with total steps amounts between 10,500-11,000 steps per day has increased from 7 days to 11 days. In the original data set, the most common step frequency was 10,000-10,500, but with replacment of NAs, the most common frequency has shifted to the next step range.  The comparative frequency of other ranges of steps per day have decreased, compared to the 10,500-11,000 column.

<br>
#### Comparing weekdays with weekends

To examine whether there were differences in activity patterns between weekdays and weekends, I used the weekdays() function on the column of R-formatted time and date values I created at the start of the analysis. This let me calculate what day of the week each date & time was from. 

I then used the weekdays to create a new factor variable is_weekday in the dataset with two levels – “weekday” and “weekend”, which indicates whether a given date is a weekday or weekend day.


```r
# this code first creates a new column with day of the week for each measurment
activity_no_NAs$day_of_week <- weekdays(activity_no_NAs$R_time)

# then i created a new column in the dataset to record whether a day was a weekend
activity_no_NAs$is_weekday <- character(length = length_data)

# I used the day of week to assign a label of "weekday" or "weekend" in a new column
for (x in (1:length_data)) {
     if (activity_no_NAs$day_of_week[x] %in% c("Saturday","Sunday")) { 
          activity_no_NAs$is_weekday[x] <- "weekend"
          } else {
               activity_no_NAs$is_weekday[x] <- "weekday"
          }
}

# convert is_weekday column to a factor variable
activity_no_NAs$is_weekday <- as.factor(activity_no_NAs$is_weekday)
```
<br>

Lastly, I calculated the average number of steps taken per time interval on weekdays, and the average number of steps taken per time interval on weekend days. 

I created a 2 panel time series plot comparing the average step activity on weekdays with the average step activity on weekends. 

I had to create a column of r-time values to graph steps by, because interval jumps from 55min to 100 min, meaning the resulting graph would be distorted. I created a column of actual time intervals, using of one full day's times & date info from my pre-processing. This was repeated twice (one  24 hrs of time data for graphing weekend, and another 24 hrs of data for graphing weekedays)


```r
# calculate avg steps per time interval for weekdays, weekends
average_weekday_steps <- tapply(X = activity_no_NAs$steps[activity_no_NAs$is_weekday=="weekday"], INDEX = activity_no_NAs$interval[activity_no_NAs$is_weekday=="weekday"], FUN = mean, simplify = T)

average_wkend_steps <- tapply(X = activity_no_NAs$steps[activity_no_NAs$is_weekday=="weekend"], INDEX = activity_no_NAs$interval[activity_no_NAs$is_weekday=="weekend"], FUN = mean, simplify = T)


# combine the average step values into a single array, then turn into a data frame (s wont be a factor)
avg_steps <- as.numeric(c(average_weekday_steps,average_wkend_steps))
avg_steps <- as.data.frame(avg_steps)

#create a vector of matcing weekday/weekend lables
is_weekend <- c(rep("weekday", 288), rep("weekend", 288))

# used column bind to create a data frame to graph with
all_avg_ <- as.data.frame(cbind(avg_steps, is_weekend))


# I also need to create an  altered  time interval for graphing, because the integer interval goes 55, 60, 100, 105 (not evenly spaced b/c not true times).  Instead i filled the 'time_interval' column with one full day's times values from my pre-processed r-time values. I repeated this twice (one full 24 hrs for graphing weekend, and one full day of 24hrs for graphing weekedays)
times <- rep(activity$R_time[1:288], 2)

all_avg_$time_interval <- times

# plot with ggplot, using facet_wrap to create two panels
library(ggplot2)
g <- ggplot(data = all_avg_, aes(x = time_interval, y = avg_steps, group = is_weekend)) +
     facet_wrap( ~ is_weekend, ncol = 1) + geom_line(color = "blue", lwd = .8) + theme_bw(base_size = 14) +
     xlab("time (sampled at 5 minute intervals)") + ylab("steps per time interval") 

# adding correctly formatted time x axis with package 'scales'
library(scales)
g <- g + scale_x_datetime(breaks = date_breaks("4 hour"), labels = date_format("%H:%M"))

#print the graph
print(g)
```

![plot of chunk timeseriesplot2](figure/timeseriesplot2-1.png) 
