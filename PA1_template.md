---
title: "Reproducible Research: Peer Assessment 1"
output: 
  html_document:
    keep_md: true
---


## Loading and preprocessing the data

Load the activity data and save the date in Date format

```r
activity <- read.csv(unzip("activity.zip"))
activity$date <- as.Date(activity$date)
```


## What is mean total number of steps taken per day?

See how many days there are

```r
length(unique(activity$date))
```

```
## [1] 61
```

1. Calculate the total number of steps taken per day

```r
StepsPerDay <- with(activity, tapply(steps, date, sum, na.rm = FALSE))
```
Quick check that we have 61 values (for the 61 days)

```r
length(StepsPerDay)
```

```
## [1] 61
```


2. Make a histogram of the total number of steps taken each day

```r
barplot(StepsPerDay)
```

![](PA1_template_files/figure-html/unnamed-chunk-5-1.png)<!-- -->

3. Calculate and report the mean and median of the total number of steps taken per day
- Mean

```r
mean(StepsPerDay, na.rm = TRUE)
```

```
## [1] 10766.19
```
- Median

```r
median(StepsPerDay, na.rm = TRUE)
```

```
## [1] 10765
```

## What is the average daily activity pattern?

1. Make a time series plot (i.e. type = "l") of the 5-minute interval (x-axis) and the average number of steps taken, averaged across all days (y-axis)

```r
# calculate average steps per interval
AvgStepsPerInterval <- aggregate(list(steps = activity$steps), list(interval = activity$interval), mean, na.rm = TRUE)
# plot
plot(AvgStepsPerInterval, type = "l", xlab = "Time Interval", ylab= "Average Steps")
```

![](PA1_template_files/figure-html/unnamed-chunk-8-1.png)<!-- -->

2. Which 5-minute interval, on average across all the days in the dataset, contains the maximum number of steps?

```r
maxSteps <- max(AvgStepsPerInterval$steps)
AvgStepsPerInterval[which(AvgStepsPerInterval$steps == maxSteps), ]
```

```
##     interval    steps
## 104      835 206.1698
```


## Imputing missing values




## Are there differences in activity patterns between weekdays and weekends?


