Week5
================
Xu Han
2023-08-06

\#Lines 5 through 20 are examples of various file types \#and the code
to read and write them. \#Your tasks begin at line 22.

\#Getting and saving your dataset is typically a two step process \#Read
and write a delimited text file. \#datasetname \<-
read.table(‘file.txt’) \#write.table(datasetname, ‘file.txt’)

\#Read and write a comma separated value file. This is a special case of
read.table/ write.table.  
\#datasetname \<- read.csv(‘file.csv’) \#write.csv(datasetname,
‘file.csv’)

\#Read and write an R data file, a file type special for R.  
\#load(‘file.RData’) \#save(datasetname, file = ‘file.Rdata’)

\#Read and write an R data file from GitHub. \#You need to select ‘raw
data’ on the GitHub page \#and then copy the URL and put in your code,
as below

\#TASK: run the code below to get and save the dataset

``` r
download.file(url = "https://raw.githubusercontent.com/fivethirtyeight/data/master/airline-safety/airline-safety.csv", destfile = "airline_safety.csv")
```

\#Then you need to name your dataset

``` r
airline_safety<- read.csv("airline_safety.csv")
```

\#TASK: take a look at the airline safety data.

``` r
head(airline_safety)
```

    ##                 airline avail_seat_km_per_week incidents_85_99
    ## 1            Aer Lingus              320906734               2
    ## 2             Aeroflot*             1197672318              76
    ## 3 Aerolineas Argentinas              385803648               6
    ## 4           Aeromexico*              596871813               3
    ## 5            Air Canada             1865253802               2
    ## 6            Air France             3004002661              14
    ##   fatal_accidents_85_99 fatalities_85_99 incidents_00_14 fatal_accidents_00_14
    ## 1                     0                0               0                     0
    ## 2                    14              128               6                     1
    ## 3                     0                0               1                     0
    ## 4                     1               64               5                     0
    ## 5                     0                0               2                     0
    ## 6                     4               79               6                     2
    ##   fatalities_00_14
    ## 1                0
    ## 2               88
    ## 3                0
    ## 4                0
    ## 5                0
    ## 6              337

\#TASK: Install and call the dplyr package.

``` r
require("dplyr")
```

    ## Loading required package: dplyr

    ## Warning: package 'dplyr' was built under R version 4.1.3

    ## 
    ## Attaching package: 'dplyr'

    ## The following objects are masked from 'package:stats':
    ## 
    ##     filter, lag

    ## The following objects are masked from 'package:base':
    ## 
    ##     intersect, setdiff, setequal, union

\#Let’s make a random sample of our data and save it

``` r
mysample<-sample_n(airline_safety, size=15, replace = FALSE, weight = NULL, .env = NULL)
```

\#TASK: Save the new sample as a csv file

``` r
write.csv(mysample,"C:/Users/xuhans/data_analytic_program/data_mining/week 5/hw5dataset.csv", row.names = FALSE)
```

\#Now let’s have some fun with *piping*

\#we will use our mysample dataset \#The pipe, %\>%, comes from the
magrittr package. \#Packages in the tidyverse (like dplyr) load %\>% for
you automatically, \#so you don’t usually load magrittr explicitly.

\#Example: Let’s try some piping with our mysample data. Note how the
dataset name is not repeated in each function

``` r
piping<-mysample %>% 
  mutate (seats = avail_seat_km_per_week) %>%
  subset(incidents_85_99 < 24) %>%
  dim()%>%
  print()
```

    ## [1] 14  9

\#TASK: revise this code chunk using piping

``` r
mysample5<-mysample%>%
          arrange(airline)%>%
          filter(incidents_85_99>10) %>%
          rename(seats = avail_seat_km_per_week)%>%
          select(incidents_00_14,incidents_85_99)%>%
          summary()
print(mysample5)
```

    ##  incidents_00_14 incidents_85_99
    ##  Min.   :17.00   Min.   :21.00  
    ##  1st Qu.:18.75   1st Qu.:21.75  
    ##  Median :20.50   Median :22.50  
    ##  Mean   :20.50   Mean   :22.50  
    ##  3rd Qu.:22.25   3rd Qu.:23.25  
    ##  Max.   :24.00   Max.   :24.00
