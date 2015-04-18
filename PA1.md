# Reproducible Research: Peer Assessment 1

## Load and preprocess the data
Read the data file and print the first few lines for inspection. 

```r
data <- read.csv("activity.csv")
head(data)
```

```
##   steps       date interval
## 1    NA 2012-10-01        0
## 2    NA 2012-10-01        5
## 3    NA 2012-10-01       10
## 4    NA 2012-10-01       15
## 5    NA 2012-10-01       20
## 6    NA 2012-10-01       25
```

There are missing values, so index the vector accordingly. 

```r
bad <- is.nan(data$steps)
```

Combine the date and interval variables into an R time object. Since strptime() cannot handle the hhmm format we will need to

1. Add leading zeros to the interval variable, 
1. Split it up into two segments with substr(), 
1. Feed into strptime() as %h%m, and 
1. Print the top of the array for inspection. 


```r
# Four element time format array: 
time <- sprintf('%04i', data$interval)
datetime <- strptime(paste(data$date, substr(time,1,2), 
            substr(time,3,4)), '%Y-%m-%d %H %M', 
            tz="EST5EDT")
head(datetime)
```

```
## [1] "2012-10-01 00:00:00 EDT" "2012-10-01 00:05:00 EDT"
## [3] "2012-10-01 00:10:00 EDT" "2012-10-01 00:15:00 EDT"
## [5] "2012-10-01 00:20:00 EDT" "2012-10-01 00:25:00 EDT"
```

## What is mean total number of steps taken per day?

Count the number of days in the dataset. Inspect the first and last entry in the dataset to confirm that an integer number of days are recorded. 


```r
datetime[1]; tail(datetime, n=1)
```

```
## [1] "2012-10-01 EDT"
```

```
## [1] "2012-11-30 23:55:00 EST"
```

And count days as the number of entries divided by 24 (hours in a day) times 12 (entries per hour, given the five-minute interval). 


```r
ndays <- length(datetime)/(24*12)
ndays
```

```
## [1] 61
```

**The integer daily average number of steps is:**


```r
round(sum(data$steps, na.rm=TRUE)/ndays)
```

```
## [1] 9354
```

## What is the average daily activity pattern?



## Inputing missing values



## Are there differences in activity patterns between weekdays and weekends?
