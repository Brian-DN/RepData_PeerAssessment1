---
title: "Reproducible Research: Peer Assessment 1"
output:
  html_document:
    keep_md: true
---


## Loading and preprocessing the data

1. Load the data

```r
data<-read.csv("activity.csv")
str(data)
```

```
## 'data.frame':	17568 obs. of  3 variables:
##  $ steps   : int  NA NA NA NA NA NA NA NA NA NA ...
##  $ date    : chr  "2012-10-01" "2012-10-01" "2012-10-01" "2012-10-01" ...
##  $ interval: int  0 5 10 15 20 25 30 35 40 45 ...
```


2. Process/tranform the data into a format suitable for your analysis

```r
data$date<-as.Date(data$date,"%Y-%m-%d")
```


## What is mean total number of steps taken per day?

1. Make a histogram of the total number of steps taken each day

```r
date<-unique(data$date,fromLast = TRUE)
tstep<-vector(mode="numeric")
for(i in date){
       tstep<-c(tstep,sum(data[data$date==i,]$steps,na.rm=TRUE))
}
plot(date,tstep,xlab="Date",ylab="Total number of steps",main="The total number of steps taken each day",type="h",lwd=6,col="blue")
```

![](PA1_template_files/figure-html/2.1-1.png)<!-- -->


2. Calculate and report the mean and median total number of steps taken per day

Here's the **mean** total number of steps taken per day

```r
meanstep<-vector(mode="numeric")
for(i in date){
       meanstep<-c(meanstep,mean(data[data$date==i,]$steps,na.rm=TRUE))
}
print(data.frame(Date=date,Mean.Step=meanstep))
```

```
##          Date  Mean.Step
## 1  2012-10-01        NaN
## 2  2012-10-02  0.4375000
## 3  2012-10-03 39.4166667
## 4  2012-10-04 42.0694444
## 5  2012-10-05 46.1597222
## 6  2012-10-06 53.5416667
## 7  2012-10-07 38.2465278
## 8  2012-10-08        NaN
## 9  2012-10-09 44.4826389
## 10 2012-10-10 34.3750000
## 11 2012-10-11 35.7777778
## 12 2012-10-12 60.3541667
## 13 2012-10-13 43.1458333
## 14 2012-10-14 52.4236111
## 15 2012-10-15 35.2048611
## 16 2012-10-16 52.3750000
## 17 2012-10-17 46.7083333
## 18 2012-10-18 34.9166667
## 19 2012-10-19 41.0729167
## 20 2012-10-20 36.0937500
## 21 2012-10-21 30.6284722
## 22 2012-10-22 46.7361111
## 23 2012-10-23 30.9652778
## 24 2012-10-24 29.0104167
## 25 2012-10-25  8.6527778
## 26 2012-10-26 23.5347222
## 27 2012-10-27 35.1354167
## 28 2012-10-28 39.7847222
## 29 2012-10-29 17.4236111
## 30 2012-10-30 34.0937500
## 31 2012-10-31 53.5208333
## 32 2012-11-01        NaN
## 33 2012-11-02 36.8055556
## 34 2012-11-03 36.7048611
## 35 2012-11-04        NaN
## 36 2012-11-05 36.2465278
## 37 2012-11-06 28.9375000
## 38 2012-11-07 44.7326389
## 39 2012-11-08 11.1770833
## 40 2012-11-09        NaN
## 41 2012-11-10        NaN
## 42 2012-11-11 43.7777778
## 43 2012-11-12 37.3784722
## 44 2012-11-13 25.4722222
## 45 2012-11-14        NaN
## 46 2012-11-15  0.1423611
## 47 2012-11-16 18.8923611
## 48 2012-11-17 49.7881944
## 49 2012-11-18 52.4652778
## 50 2012-11-19 30.6979167
## 51 2012-11-20 15.5277778
## 52 2012-11-21 44.3993056
## 53 2012-11-22 70.9270833
## 54 2012-11-23 73.5902778
## 55 2012-11-24 50.2708333
## 56 2012-11-25 41.0902778
## 57 2012-11-26 38.7569444
## 58 2012-11-27 47.3819444
## 59 2012-11-28 35.3576389
## 60 2012-11-29 24.4687500
## 61 2012-11-30        NaN
```

Here's the **median** total number of steps taken per day

```r
medstep<-vector(mode="numeric")
for(i in date){
       medstep<-c(medstep,median(sort(data[data$date==i,]$steps)))
}
print(data.frame(Date=date,Median.Step=medstep))
```

```
##          Date Median.Step
## 1  2012-10-01          NA
## 2  2012-10-02           0
## 3  2012-10-03           0
## 4  2012-10-04           0
## 5  2012-10-05           0
## 6  2012-10-06           0
## 7  2012-10-07           0
## 8  2012-10-08          NA
## 9  2012-10-09           0
## 10 2012-10-10           0
## 11 2012-10-11           0
## 12 2012-10-12           0
## 13 2012-10-13           0
## 14 2012-10-14           0
## 15 2012-10-15           0
## 16 2012-10-16           0
## 17 2012-10-17           0
## 18 2012-10-18           0
## 19 2012-10-19           0
## 20 2012-10-20           0
## 21 2012-10-21           0
## 22 2012-10-22           0
## 23 2012-10-23           0
## 24 2012-10-24           0
## 25 2012-10-25           0
## 26 2012-10-26           0
## 27 2012-10-27           0
## 28 2012-10-28           0
## 29 2012-10-29           0
## 30 2012-10-30           0
## 31 2012-10-31           0
## 32 2012-11-01          NA
## 33 2012-11-02           0
## 34 2012-11-03           0
## 35 2012-11-04          NA
## 36 2012-11-05           0
## 37 2012-11-06           0
## 38 2012-11-07           0
## 39 2012-11-08           0
## 40 2012-11-09          NA
## 41 2012-11-10          NA
## 42 2012-11-11           0
## 43 2012-11-12           0
## 44 2012-11-13           0
## 45 2012-11-14          NA
## 46 2012-11-15           0
## 47 2012-11-16           0
## 48 2012-11-17           0
## 49 2012-11-18           0
## 50 2012-11-19           0
## 51 2012-11-20           0
## 52 2012-11-21           0
## 53 2012-11-22           0
## 54 2012-11-23           0
## 55 2012-11-24           0
## 56 2012-11-25           0
## 57 2012-11-26           0
## 58 2012-11-27           0
## 59 2012-11-28           0
## 60 2012-11-29           0
## 61 2012-11-30          NA
```


## What is the average daily activity pattern?

1. Make a time series plot of the 5-minute interval and the average number of steps taken, averaged across all days

```r
itv<-unique(data$interval,fromLast = TRUE)
avgstep<-vector(mode="numeric")
for(i in itv){
       avgstep<-c(avgstep,mean(data[data$interval==i,]$steps,na.rm=TRUE))
}
meaninterval<-data.frame(itv,avgstep)
plot(itv,avgstep,xlab="5-minute interval",ylab="Average number of steps",main="Time series plot of 5-minute interval",type="l",lwd=1,col="red")
```

![](PA1_template_files/figure-html/3.1-1.png)<!-- -->

2. Which 5-minute interval, on average across all the days in the dataset, contains the maximum number of steps

```r
itv[which.max(avgstep)]
```

```
## [1] 835
```


## Imputing missing values

1. Calculate and report the total number of missing values in the dataset

```r
sum(is.na(data$steps))
```

```
## [1] 2304
```

```r
sum(is.na(data$date))
```

```
## [1] 0
```

```r
sum(is.na(data$interval))
```

```
## [1] 0
```

```r
sum(is.na(data))
```

```
## [1] 2304
```

2. Filling in all of the missing values in the dataset by mean for that 5-minute interval

```r
newdata<-data
a<-which(is.na(newdata$steps))
for(i in a){
       newdata$steps[i]<-meaninterval[meaninterval$itv==newdata$interval[i],]$avgstep
}
```

3. Creat a new data

```r
str(newdata)
```

```
## 'data.frame':	17568 obs. of  3 variables:
##  $ steps   : num  1.717 0.3396 0.1321 0.1509 0.0755 ...
##  $ date    : Date, format: "2012-10-01" "2012-10-01" ...
##  $ interval: int  0 5 10 15 20 25 30 35 40 45 ...
```

4. Make a histogram of the total number of steps taken each day and Calculate and report the mean and median total number of steps taken per day

Here's a histogram of total number of steps taken each day in new data

```r
ntstep<-vector(mode="numeric")
for(i in date){
       ntstep<-c(ntstep,sum(newdata[newdata$date==i,]$steps,na.rm=TRUE))
}
plot(date,ntstep,xlab="Date",ylab="Total number of steps",main="The total number of steps taken each day",type="h",lwd=6,col="blue")
```

![](PA1_template_files/figure-html/4.4.1-1.png)<!-- -->

Here's the **mean** total number of steps taken each day

```r
nmeanstep<-vector(mode="numeric")
for(i in date){
       nmeanstep<-c(nmeanstep,mean(newdata[newdata$date==i,]$steps,na.rm=TRUE))
}
print(data.frame(Date=date,Mean.Step=nmeanstep))
```

```
##          Date  Mean.Step
## 1  2012-10-01 37.3825996
## 2  2012-10-02  0.4375000
## 3  2012-10-03 39.4166667
## 4  2012-10-04 42.0694444
## 5  2012-10-05 46.1597222
## 6  2012-10-06 53.5416667
## 7  2012-10-07 38.2465278
## 8  2012-10-08 37.3825996
## 9  2012-10-09 44.4826389
## 10 2012-10-10 34.3750000
## 11 2012-10-11 35.7777778
## 12 2012-10-12 60.3541667
## 13 2012-10-13 43.1458333
## 14 2012-10-14 52.4236111
## 15 2012-10-15 35.2048611
## 16 2012-10-16 52.3750000
## 17 2012-10-17 46.7083333
## 18 2012-10-18 34.9166667
## 19 2012-10-19 41.0729167
## 20 2012-10-20 36.0937500
## 21 2012-10-21 30.6284722
## 22 2012-10-22 46.7361111
## 23 2012-10-23 30.9652778
## 24 2012-10-24 29.0104167
## 25 2012-10-25  8.6527778
## 26 2012-10-26 23.5347222
## 27 2012-10-27 35.1354167
## 28 2012-10-28 39.7847222
## 29 2012-10-29 17.4236111
## 30 2012-10-30 34.0937500
## 31 2012-10-31 53.5208333
## 32 2012-11-01 37.3825996
## 33 2012-11-02 36.8055556
## 34 2012-11-03 36.7048611
## 35 2012-11-04 37.3825996
## 36 2012-11-05 36.2465278
## 37 2012-11-06 28.9375000
## 38 2012-11-07 44.7326389
## 39 2012-11-08 11.1770833
## 40 2012-11-09 37.3825996
## 41 2012-11-10 37.3825996
## 42 2012-11-11 43.7777778
## 43 2012-11-12 37.3784722
## 44 2012-11-13 25.4722222
## 45 2012-11-14 37.3825996
## 46 2012-11-15  0.1423611
## 47 2012-11-16 18.8923611
## 48 2012-11-17 49.7881944
## 49 2012-11-18 52.4652778
## 50 2012-11-19 30.6979167
## 51 2012-11-20 15.5277778
## 52 2012-11-21 44.3993056
## 53 2012-11-22 70.9270833
## 54 2012-11-23 73.5902778
## 55 2012-11-24 50.2708333
## 56 2012-11-25 41.0902778
## 57 2012-11-26 38.7569444
## 58 2012-11-27 47.3819444
## 59 2012-11-28 35.3576389
## 60 2012-11-29 24.4687500
## 61 2012-11-30 37.3825996
```

Here's the **median** total number of steps taken each day

```r
nmedstep<-vector(mode="numeric")
for(i in date){
       nmedstep<-c(nmedstep,median(sort(newdata[newdata$date==i,]$steps)))
}
print(data.frame(Date=date,Median.Step=nmedstep))
```

```
##          Date Median.Step
## 1  2012-10-01    34.11321
## 2  2012-10-02     0.00000
## 3  2012-10-03     0.00000
## 4  2012-10-04     0.00000
## 5  2012-10-05     0.00000
## 6  2012-10-06     0.00000
## 7  2012-10-07     0.00000
## 8  2012-10-08    34.11321
## 9  2012-10-09     0.00000
## 10 2012-10-10     0.00000
## 11 2012-10-11     0.00000
## 12 2012-10-12     0.00000
## 13 2012-10-13     0.00000
## 14 2012-10-14     0.00000
## 15 2012-10-15     0.00000
## 16 2012-10-16     0.00000
## 17 2012-10-17     0.00000
## 18 2012-10-18     0.00000
## 19 2012-10-19     0.00000
## 20 2012-10-20     0.00000
## 21 2012-10-21     0.00000
## 22 2012-10-22     0.00000
## 23 2012-10-23     0.00000
## 24 2012-10-24     0.00000
## 25 2012-10-25     0.00000
## 26 2012-10-26     0.00000
## 27 2012-10-27     0.00000
## 28 2012-10-28     0.00000
## 29 2012-10-29     0.00000
## 30 2012-10-30     0.00000
## 31 2012-10-31     0.00000
## 32 2012-11-01    34.11321
## 33 2012-11-02     0.00000
## 34 2012-11-03     0.00000
## 35 2012-11-04    34.11321
## 36 2012-11-05     0.00000
## 37 2012-11-06     0.00000
## 38 2012-11-07     0.00000
## 39 2012-11-08     0.00000
## 40 2012-11-09    34.11321
## 41 2012-11-10    34.11321
## 42 2012-11-11     0.00000
## 43 2012-11-12     0.00000
## 44 2012-11-13     0.00000
## 45 2012-11-14    34.11321
## 46 2012-11-15     0.00000
## 47 2012-11-16     0.00000
## 48 2012-11-17     0.00000
## 49 2012-11-18     0.00000
## 50 2012-11-19     0.00000
## 51 2012-11-20     0.00000
## 52 2012-11-21     0.00000
## 53 2012-11-22     0.00000
## 54 2012-11-23     0.00000
## 55 2012-11-24     0.00000
## 56 2012-11-25     0.00000
## 57 2012-11-26     0.00000
## 58 2012-11-27     0.00000
## 59 2012-11-28     0.00000
## 60 2012-11-29     0.00000
## 61 2012-11-30    34.11321
```

First, we find the day had NAs filled

```r
unique(data$date[which(is.na(data$steps))])
```

```
## [1] "2012-10-01" "2012-10-08" "2012-11-01" "2012-11-04" "2012-11-09"
## [6] "2012-11-10" "2012-11-14" "2012-11-30"
```
So, the impact of imputing missing data on the estimates of the total daily number of steps is on that day.


## Are there differences in activity patterns between weekdays and weekends?

1. Create a new factor variable in the dataset with two levels -- "weekday" and "weekend" indicating whether a given date is a weekday or weekend day

```r
wd<-vector(mode="character")
nr<-nrow(newdata)
for (i in 1:nr){
       ifelse(weekdays(newdata$date[i])!="Saturday"&weekdays(newdata$date[i])!="Sunday",wd<-c(wd,"weekday"),wd<-c(wd,"weekend"))
}
newdata<-data.frame(newdata,wd)
str(newdata)
```

```
## 'data.frame':	17568 obs. of  4 variables:
##  $ steps   : num  1.717 0.3396 0.1321 0.1509 0.0755 ...
##  $ date    : Date, format: "2012-10-01" "2012-10-01" ...
##  $ interval: int  0 5 10 15 20 25 30 35 40 45 ...
##  $ wd      : chr  "weekday" "weekday" "weekday" "weekday" ...
```

2. Make a panel plot containing a time series plot of the 5-minute interval

```r
library(lattice)
numstep<-vector(mode="numeric")
for(i in itv){
       for (j in c("weekday","weekend")){
              numstep<-c(numstep,mean(newdata[newdata$interval==i&newdata$wd==j,]$steps))
       }
}
d<-data.frame(interval=rep(itv,each=2),wd=rep(c("weekday","weekend"),times=length(itv)),numstep)
xyplot(numstep~itv|wd,data=d,layout=c(1,2),xlab="Interval",ylab="Number of steps",type="l",lwd=1,col="blue")
```

![](PA1_template_files/figure-html/5.2-1.png)<!-- -->
