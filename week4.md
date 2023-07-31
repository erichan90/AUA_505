Week4
================
Xu Han
2023-07-30

\#Task: Write the code to get a dataset from Base R: ChickWeight \#and
save it as a dataframe with a new name that includes your first name

``` r
xudata<-data.frame(ChickWeight)
```

\#See the top rows of the data \#TASK: Write the code to see the top
rows of the data

``` r
head(xudata)
```

    ##   weight Time Chick Diet
    ## 1     42    0     1    1
    ## 2     51    2     1    1
    ## 3     59    4     1    1
    ## 4     64    6     1    1
    ## 5     76    8     1    1
    ## 6     93   10     1    1

\#Install and call the package dplyr \#TASK: Write the code to install
and call dplyr \#The following code will first check whether the package
is installed, installed it if not and then import the library

``` r
packages = c("ggplot2","dplyr","psych")
#check for missing packages; load and install as needed.
package.check <- lapply(packages, FUN = function(x){
    if (!require(x, character.only = TRUE)) {
        install.packages(x, dependencies = TRUE)
        library(x, character.only = TRUE)
    }
})
```

    ## Loading required package: ggplot2

    ## Warning: package 'ggplot2' was built under R version 4.1.3

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

    ## Loading required package: psych

    ## 
    ## Attaching package: 'psych'

    ## The following objects are masked from 'package:ggplot2':
    ## 
    ##     %+%, alpha

\#Let’s just see the weight and Time columns \#Task: Write the code to
‘select’ just the weight and Time columns \#(hint: use the ‘select’
function)

``` r
xudata_subset<-xudata%>%
    select(weight,Time)

head(xudata_subset)
```

    ##   weight Time
    ## 1     42    0
    ## 2     51    2
    ## 3     59    4
    ## 4     64    6
    ## 5     76    8
    ## 6     93   10

\#Let’s name the dataset with just the two columns, weight and Time
\#TASK: Write the code to save the two columns as a new dataframe \#and
give it a new name

``` r
newdata=data.frame(weight=xudata$weight,time=xudata$Time)
head(newdata)
```

    ##   weight time
    ## 1     42    0
    ## 2     51    2
    ## 3     59    4
    ## 4     64    6
    ## 5     76    8
    ## 6     93   10

\#Let’s get rid of the Time column in the new dataframe created above
\#TASK: Write the code that deselects the Time column \#(hint: use the
‘select’ function to not select a -column)

``` r
newdata=newdata%>%
        select(-time)
head(newdata)
```

    ##   weight
    ## 1     42
    ## 2     51
    ## 3     59
    ## 4     64
    ## 5     76
    ## 6     93

head(newdata)

\#Let’s rename a column name \#TASK: Write the code that renames
‘weight’ to ‘ounces’

``` r
newdata=newdata%>%
               dplyr::rename(ounces=weight)
head(newdata)
```

    ##   ounces
    ## 1     42
    ## 2     51
    ## 3     59
    ## 4     64
    ## 5     76
    ## 6     93

\#Let’s make a new dataframe with the new column name \#TASK: Write the
code that names a new dataframe that includes the ‘ounces’ column

``` r
newdata2=newdata
head(newdata2)
```

    ##   ounces
    ## 1     42
    ## 2     51
    ## 3     59
    ## 4     64
    ## 5     76
    ## 6     93

\#Let’s ‘filter’ our dataframe to only those with a 1 in the Chick
column \#TASK: Write the code that includes only rows where Chick = 1

``` r
xudata2=xudata%>%
        filter(Chick==1)
table(xudata2$Chick)
```

    ## 
    ## 18 16 15 13  9 20 10  8 17 19  4  6 11  3  1 12  2  5 14  7 24 30 22 23 27 28 
    ##  0  0  0  0  0  0  0  0  0  0  0  0  0  0 12  0  0  0  0  0  0  0  0  0  0  0 
    ## 26 25 29 21 33 37 36 31 39 38 32 40 34 35 44 45 43 41 47 49 46 50 42 48 
    ##  0  0  0  0  0  0  0  0  0  0  0  0  0  0  0  0  0  0  0  0  0  0  0  0

\#Let’s ‘group’ our data by Diet \#TASK: Write the code to group the
data by Diet (hint: group_by)

``` r
xudata3=xudata%>%
        group_by(Diet)
head(xudata3)
```

    ## # A tibble: 6 x 4
    ## # Groups:   Diet [1]
    ##   weight  Time Chick Diet 
    ##    <dbl> <dbl> <ord> <fct>
    ## 1     42     0 1     1    
    ## 2     51     2 1     1    
    ## 3     59     4 1     1    
    ## 4     64     6 1     1    
    ## 5     76     8 1     1    
    ## 6     93    10 1     1

\#Task: add one of the other codes (not in the tasks above) \#you
learned about from the dplyr package-replacing the missing values with
zero

``` r
print("Count of missing values by column wise")
```

    ## [1] "Count of missing values by column wise"

``` r
sapply(xudata, function(x) sum(is.na(x)))
```

    ## weight   Time  Chick   Diet 
    ##      0      0      0      0

``` r
xudata3=xudata %>% replace(is.na(.), 0)
```
