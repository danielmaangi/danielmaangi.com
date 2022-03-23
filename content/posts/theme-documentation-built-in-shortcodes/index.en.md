---
categories:
- documentation
date: "2022-03-23 19:21:08 EAT"
description: This post provides a simple guide on how to import and combine numerous csv files in R.
draft: false
lastmod: "2020-03-04T16:29:41+08:00"
resources:
- name: featured-image
  src: featured-image.png
tags:
- shortcodes
title: Import and combine numerous .csv files using R
weight: 3
---

**R** provides a simple way of reading and combining multiple csv files.

<!--more-->

I was in a situation where I had more than 50 .csv files of the same structure and I was wondering how I can quickly import and combine all of them into a single data frame in R so that I can perform some transformations I needed on the whole data set.
## 1 figure {#figure}

At first I was thinking of this!

```markdown
# remove # if yo have not installed tidyr
# install.packages ("tidyr")

#load required package
library(readr)

#Read the files individually using readr package
data_1 = read_csv("file1.csv") 
data_2 = read_csv("file2.csv")
.
.
.
data_n = read_csv("file3.csv")

# Combine the files into one dataset using base R's rbind function
data = rbind(data_1, data_2, ..., data_n)
```



This is time consuming, onerous and error-prone. The good thing is that R is a functional programming language and this task can be easily accomplished in just a few seconds using read_csv, list.files (), map(), map_df() and rbind() as shown by the code below.



```markdown
# remove # if yo have not installed tidyr
# install.packages ("tidyr") 

# Load the required package
library(readr) 

# .csv files directory/ folder path
csv_folder <- list.files(path = "C:/Users/../My Csv Files", 
pattern = "*.csv", full.names = T)

# read and combine the individual files in the folder
mydata <- csv_folder %>%
  map(read_csv) %>%
  map_df(rbind)
```

And there you go - all data has been loaded and combined into a single data frame. Note how it's easier to use the pipe "%>%" operator. In my next post, I will focus on .xlsx and .xls files.


Thanks for reading!



