---
title: "Reproducible Research: Peer Assessment 1"
output:
  html_document:
    keep_md: true
---


### **Loading and preprocessing the data**

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


### **What is mean total number of steps taken per day?**

1. Make a histogram of the total number of steps taken each day

```r
date<-unique(data$date,fromLast = TRUE)
tstep<-vector(mode="numeric")
for(i in date){
       tstep<-c(tstep,sum(data[data$date==i,]$steps,na.rm=TRUE))
}
hist(tstep,col="blue",xlab="Total number of steps per day",main="Histogram of number of steps per day",breaks=seq(0,25000,by=1000))
```

![](PA1_template_files/figure-html/2.1-1.png)<!-- -->


2. Calculate and report the mean and median total number of steps taken per day

Here's the **mean** total number of steps taken per day

```r
mean(tstep)
```

```
## [1] 9354.23
```

Here's the **median** total number of steps taken per day

```r
median(tstep)
```

```
## [1] 10395
```


### **What is the average daily activity pattern?**

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


### **Imputing missing values**

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
hist(ntstep,col="blue",xlab="Total number of steps per day",main="Histogram of number of steps per day",breaks=seq(0,25000,by=1000))
```

![](PA1_template_files/figure-html/4.4.1-1.png)<!-- -->

Here's the **mean** total number of steps taken each day

```r
mean(ntstep)
```

```
## [1] 10766.19
```

Here's the **median** total number of steps taken each day

```r
median(tstep)
```

```
## [1] 10395
```


### **Are there differences in activity patterns between weekdays and weekends?**

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
