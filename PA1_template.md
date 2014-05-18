package ‘RCurl’ successfully unpacked and MD5 sums checked

The downloaded binary packages are in
  C:\Users\santalaoren57\AppData\Local\Temp\RtmpA1tXnk\downloaded_packages
> library(RCurl)
Loading required package: bitops
> library(bitops)
> library(RCurl)
file_name = "activity.csv"
setInternet2(use = TRUE)  #required to support SSL in the url
url_source = "https://raw.githubusercontent.com/WUVsUQkP/RepData_PeerAssessment1/master/activity.zip"
if (!file.exists(file_name)) {
    download.file(url_source, destfile = file_name, method = "auto")
}

> mydata = "activity.csv"
> setInternet2(use = TRUE)
> my_data <- read.csv("activity.csv")
> data_day <- aggregate(steps ~ date, data = my_data, FUN = sum)
> data_inv <- aggregate(my_data$steps, by = list(interval = my_data$interval), FUN = mean, na.rm = T)
> colnames(data_inv) <- c("interval", "steps")
> data_inv$interval <- as.integer(data_inv$interval)
What is mean total number of steps taken per day?

This is a histogram of the total number of steps taken each day
library(ggplot2)  #ggplot2 is used for plotting


> library(ggplot2)
> steps_mean <- round(mean(data_day$steps), 0)
> steps_median <- round(median(data_day$steps), 0)
> point_labels <- c(paste(" Mean:", steps_mean), paste(" Median:", steps_median))
> color_names <- c("red", "black")
> ggplot(data_day, aes(x = steps)) + geom_histogram(fill = "orange", binwidth = 800) + geom_point(aes(x = steps_mean, y = 0, color = color_names[1]), size = 4, shape = 12) + geom_point(aes(x = steps_median, y = 0, color = color_names[2]), size = 4, shape = 10) + scale_color_manual(name = element_blank(), labels = point_labels, values = color_names) + labs(title = "Histogram of Steps per Day", x = "Number of Steps", y = "Count") + theme_bw() + theme(legend.position = "bottom")
> 
> 
> steps_max <- which.max(data_inv$steps)
> interval_max <- data_inv[steps_max, ]$interval
> point_labels <- c(paste(" Maximun Activity Interval:", interval_max))
> ggplot(data_inv, aes(x = interval, y = steps)) + geom_line(color = "orange", size = 1) + geom_point(aes(x = interval_max, y = 0, color = "red"), size = 4,shape = 12) + scale_color_manual(name = element_blank(), labels = point_labels, values = c("red")) + labs(title = "Average daily activity pattern", x = "5-minute Interval", y = "Average Steps") + theme_bw() + theme(legend.position = "bottom")
