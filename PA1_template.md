---
title: "Reproducible Research: Peer Assessment 1"
output: 
  html_document:
    keep_md: true
---

### Loading and preprocessing the data


```r
fileUrl <- "https://d396qusza40orc.cloudfront.net/repdata%2Fdata%2Factivity.zip"
download.file(fileUrl,destfile="activity.zip",method="curl")
unzip("activity.zip")
activity <- read.csv("activity.csv")
act2 <- aggregate(activity$steps, by=list(date=activity$date), FUN=sum)
```

### The histogram of the total number of steps taken each day


```r
hist(act2$x)
```

![plot of chunk unnamed-chunk-2](figure/unnamed-chunk-2-1.png) 

### The mean total number of steps taken per day


```r
mean(act2$x,na.rm=T)
```

```
## [1] 10766.19
```

### The median total number of steps taken per day


```r
median(act2$x,na.rm=T)
```

```
## [1] 10765
```

### Time series plot of the 5-minute interval (x-axis) and the average number of steps taken, averaged across all days


```r
act3 <- aggregate(activity$steps, by=list(interval=activity$interval), FUN=mean, na.rm=T)
plot(act3$interval,act3$x,type="l")
```

![plot of chunk unnamed-chunk-5](figure/unnamed-chunk-5-1.png) 

### Interval containing the maximum number of steps


```r
act3$interval[act3$x==max(act3$x)]
```

```
## [1] 835
```
