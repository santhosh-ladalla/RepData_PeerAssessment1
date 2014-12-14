Reproducible research - Analysis of Activity monitoring data (assignment 1)
========================================================

In this document we will do analysis on the activity monitoring data provided in the assignment.Information about the variables in the data is below

* __steps__: Number of steps taking in a 5-minute interval (missing values are coded as NA)
* __date__: The date on which the measurement was taken in YYYY-MM-DD format
* __interval__: Identifier for the 5-minute interval in which measurement was taken

### Loading and preprocessing the data

Additional required processing is done in the later sections of the analysis.


```r
doc <- read.csv("activity.csv")
```

```
## Warning: cannot open file 'activity.csv': No such file or directory
```

```
## Error: cannot open the connection
```



```r
library(ggplot2)
library(dplyr)
```

```
## 
## Attaching package: 'dplyr'
## 
## The following objects are masked from 'package:stats':
## 
##     filter, lag
## 
## The following objects are masked from 'package:base':
## 
##     intersect, setdiff, setequal, union
```


### What is mean total number of steps taken per day?

The code below calculated the sum of the steps per day and the plots a histogram.


```r
doc_1 <- doc %.%
group_by(date) %.%
summarise(newvar = sum(steps))
```

```
## Error: object 'doc' not found
```

```r
m <- ggplot(doc_1, aes(x=newvar))
```

```
## Error: object 'doc_1' not found
```

```r
m+geom_histogram(binwidth=1000,fill="green",colour="black")+xlab("number of steps taken each day") +ggtitle("Frequency of the number of steps per day")
```

```
## Error: object 'm' not found
```

The mean and median values of the total number of steps per day are:


```r
doc_1  %.% summarise(mean(newvar,na.rm=TRUE))
```

```
## Error: object 'doc_1' not found
```

```r
doc_1  %.% summarise(median(newvar,na.rm=TRUE))
```

```
## Error: object 'doc_1' not found
```

### What is the average daily activity pattern?

The below plot is a time series plot of the 5-minute interval (x-axis) and the average number of steps taken, averaged across all days (y-axis) 



```r
avg <- doc %.% group_by(interval) %.% summarise(avg_num_steps = mean(steps,na.rm =TRUE))
```

```
## Error: object 'doc' not found
```

```r
m1 <- ggplot(avg, aes(x=interval,y=avg_num_steps))
```

```
## Error: object 'avg' not found
```

```r
m1+geom_line(colour="red") + xlab("5 minute time interval") +ylab("average steps for all days")+ ggtitle("Average number of steps for the time intervals")
```

```
## Error: object 'm1' not found
```



```r
max_t <- avg %>%  arrange(desc(avg_num_steps)) %>% top_n(n=1)
```

```
## Error: object 'avg' not found
```

```r
max_t 
```

```
## Error: object 'max_t' not found
```

The time interval with maximum number of steps is 835 (In the morning).

### Imputing missing values



```r
t <- length(which(is.na(doc$steps)))
```

```
## Error: object 'doc' not found
```

```r
t
```

```
## function (x) 
## UseMethod("t")
## <bytecode: 0x7fad6d816bf8>
## <environment: namespace:base>
```





