<<<<<<< HEAD
---
title: "Reproducible Research: Peer Assessment 1"
output: 
  html_document:
    keep_md: true
---
# Project Week-2 Reproducible Research

## Loading and preprocessing the data


#Task-1
##Loading the Data

```r
if(!file.exists("activity.csv")){
  t <- tempfile()
  download.file("https://d396qusza40orc.cloudfront.net/repdata%2Fdata%2Factivity.zip",t)
  unzip(t)
  unlink(t)
}

activity <- read.csv("activity.csv")
```



## What is mean total number of steps taken per day?


#Task-2
##Calculating Number of Steps in a Day


```r
steps_per_day <- aggregate(steps ~ date,activity,FUN=sum,na.rm=TRUE)
```

## Plotting Histogram for Number of Steps on Each Day


```r
hist(steps_per_day$steps, main = "Total Steps on Each Day", col = "orange",xlab = "Number of Days",ylab = "Number of Steps")
```

![plot of chunk unnamed-chunk-3](figure/unnamed-chunk-3-1.png)

## Calculating the Mean and Median of Total Number of Steps Taken per Day

```r
Mean_Steps <- mean(steps_per_day$steps)
Median_steps <- median(steps_per_day$steps)
```

#### The Mean of Number of Steps is : ``1.0766189 &times; 10<sup>4</sup>`` 
#### The Median of Number of Steps is : ``10765``


## What is the average daily activity pattern?

#Task-3
## Calculate the average activity pattern each day.


```r
avg_steps_per_day <- aggregate(steps ~ interval,activity,FUN=mean,na.rm=TRUE)
```

## Plot the Average Daily Activity Pattern


```r
plot(avg_steps_per_day$interval, avg_steps_per_day$steps, type ='l',main = "Average Steps on Each Day by Interval", col = "orange",xlab = "Interval",ylab = "Number of Steps")
```

![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-1.png)

## Calculate the Interval with the maximum steps

```r
interval_for_max_steps <- avg_steps_per_day[which.max(avg_steps_per_day$steps),1]
```

#### The interval with maximum number of steps is : ``835``


## Imputing missing values

##Task-4
## Impute Missing Values

### Count Number of NA Values


```r
na_count <- length(which(is.na(activity$steps)))
```

#### The Number of NA values are : ``2304``

### Fill in NA Values


```r
Imputed_Activity_Data <- merge(activity,avg_steps_per_day,by="interval",suffixes = c("",".interval.mean"))

nas <- is.na(Imputed_Activity_Data$steps)

Imputed_Activity_Data$steps[nas] <- Imputed_Activity_Data$steps.interval.mean[nas]


total_steps_per_day_imputed <- aggregate(steps ~ date,Imputed_Activity_Data, sum)
```

### Plot the histogram with imputed steps per day


```r
hist(total_steps_per_day_imputed$steps, main="Total Number of Steps Per Day",col= "orange",xlab="Number of Steps",ylab = "Count")
```

![plot of chunk unnamed-chunk-10](figure/unnamed-chunk-10-1.png)


### Calculate the mean and median of the imputed values.


```r
Mean_imputed_Steps <- mean(total_steps_per_day_imputed$steps)
Median_imputed_steps <- median(total_steps_per_day_imputed$steps)
```

#### The Mean of Number of Steps is : ``1.0766189 &times; 10<sup>4</sup>``
#### The Median of Number of Steps is : ``1.0766189 &times; 10<sup>4</sup>``

### Calculate the Diff between the Imputed and Non-Imputed Data


```r
diff_mean <- Mean_imputed_Steps - Mean_Steps
diff_median <- Median_imputed_steps - Median_steps
```


#### The Difference between the Means of Number of Steps is : ``0``
#### The Difference between the Median of Number of Steps is : ``1.1886792``


### Calculate the Diff between the Imputed and Non-Imputed Data


```r
total_diff_steps <- sum(total_steps_per_day_imputed$steps) - sum(steps_per_day$steps)
```

#### The Difference between the Number of Steps of imputed and non-imputed data is : ``8.6129509 &times; 10<sup>4</sup>``

## Are there differences in activity patterns between weekdays and weekends?

## Task-5



```r
weekdays <- c("Monday", "Tuesday", "Wednesday", "Thursday", 
              "Friday")
Imputed_Activity_Data$dow = as.factor(ifelse(is.element(weekdays(as.Date(Imputed_Activity_Data$date)),weekdays), "Weekday", "Weekend"))

avg_imputed_steps_per_day <- aggregate(steps ~ interval + dow, Imputed_Activity_Data, mean)

library(lattice)

xyplot(avg_imputed_steps_per_day$steps ~ avg_imputed_steps_per_day$interval|avg_imputed_steps_per_day$dow, main="Average Number of Steps per Day by Interval",xlab="Interval", ylab="Number of Steps",layout=c(1,2), type="l",col="orange")
```

![plot of chunk unnamed-chunk-14](figure/unnamed-chunk-14-1.png)


=======
---
title: "Reproducible Research: Peer Assessment 1"
output: 
  html_document:
    keep_md: true
---
# Project Week-2 Reproducible Research

## Loading and preprocessing the data


#Task-1
##Loading the Data

```r
if(!file.exists("activity.csv")){
  t <- tempfile()
  download.file("https://d396qusza40orc.cloudfront.net/repdata%2Fdata%2Factivity.zip",t)
  unzip(t)
  unlink(t)
}

activity <- read.csv("activity.csv")
```



## What is mean total number of steps taken per day?


#Task-2
##Calculating Number of Steps in a Day


```r
steps_per_day <- aggregate(steps ~ date,activity,FUN=sum,na.rm=TRUE)
```

## Plotting Histogram for Number of Steps on Each Day


```r
hist(steps_per_day$steps, main = "Total Steps on Each Day", col = "orange",xlab = "Number of Days",ylab = "Number of Steps")
```

![plot of chunk unnamed-chunk-17](figure/unnamed-chunk-17-1.png)

## Calculating the Mean and Median of Total Number of Steps Taken per Day

```r
Mean_Steps <- mean(steps_per_day$steps)
Median_steps <- median(steps_per_day$steps)
```

#### The Mean of Number of Steps is : ``1.0766189 &times; 10<sup>4</sup>`` 
#### The Median of Number of Steps is : ``10765``


## What is the average daily activity pattern?

#Task-3
## Calculate the average activity pattern each day.


```r
avg_steps_per_day <- aggregate(steps ~ interval,activity,FUN=mean,na.rm=TRUE)
```

## Plot the Average Daily Activity Pattern


```r
plot(avg_steps_per_day$interval, avg_steps_per_day$steps, type ='l',main = "Average Steps on Each Day by Interval", col = "orange",xlab = "Interval",ylab = "Number of Steps")
```

![plot of chunk unnamed-chunk-20](figure/unnamed-chunk-20-1.png)

## Calculate the Interval with the maximum steps

```r
interval_for_max_steps <- avg_steps_per_day[which.max(avg_steps_per_day$steps),1]
```

#### The interval with maximum number of steps is : ``835``


## Imputing missing values

##Task-4
## Impute Missing Values

### Count Number of NA Values


```r
na_count <- length(which(is.na(activity$steps)))
```

#### The Number of NA values are : ``2304``

### Fill in NA Values


```r
Imputed_Activity_Data <- merge(activity,avg_steps_per_day,by="interval",suffixes = c("",".interval.mean"))

nas <- is.na(Imputed_Activity_Data$steps)

Imputed_Activity_Data$steps[nas] <- Imputed_Activity_Data$steps.interval.mean[nas]


total_steps_per_day_imputed <- aggregate(steps ~ date,Imputed_Activity_Data, sum)
```

### Plot the histogram with imputed steps per day


```r
hist(total_steps_per_day_imputed$steps, main="Total Number of Steps Per Day",col= "orange",xlab="Number of Steps",ylab = "Count")
```

![plot of chunk unnamed-chunk-24](figure/unnamed-chunk-24-1.png)


### Calculate the mean and median of the imputed values.


```r
Mean_imputed_Steps <- mean(total_steps_per_day_imputed$steps)
Median_imputed_steps <- median(total_steps_per_day_imputed$steps)
```

#### The Mean of Number of Steps is : ``1.0766189 &times; 10<sup>4</sup>``
#### The Median of Number of Steps is : ``1.0766189 &times; 10<sup>4</sup>``

### Calculate the Diff between the Imputed and Non-Imputed Data


```r
diff_mean <- Mean_imputed_Steps - Mean_Steps
diff_median <- Median_imputed_steps - Median_steps
```


#### The Difference between the Means of Number of Steps is : ``0``
#### The Difference between the Median of Number of Steps is : ``1.1886792``


### Calculate the Diff between the Imputed and Non-Imputed Data


```r
total_diff_steps <- sum(total_steps_per_day_imputed$steps) - sum(steps_per_day$steps)
```

#### The Difference between the Number of Steps of imputed and non-imputed data is : ``8.6129509 &times; 10<sup>4</sup>``

## Are there differences in activity patterns between weekdays and weekends?

## Task-5



```r
weekdays <- c("Monday", "Tuesday", "Wednesday", "Thursday", 
              "Friday")
Imputed_Activity_Data$dow = as.factor(ifelse(is.element(weekdays(as.Date(Imputed_Activity_Data$date)),weekdays), "Weekday", "Weekend"))

avg_imputed_steps_per_day <- aggregate(steps ~ interval + dow, Imputed_Activity_Data, mean)

library(lattice)

xyplot(avg_imputed_steps_per_day$steps ~ avg_imputed_steps_per_day$interval|avg_imputed_steps_per_day$dow, main="Average Number of Steps per Day by Interval",xlab="Interval", ylab="Number of Steps",layout=c(1,2), type="l",col="orange")
```

![plot of chunk unnamed-chunk-28](figure/unnamed-chunk-28-1.png)


>>>>>>> origin/master
