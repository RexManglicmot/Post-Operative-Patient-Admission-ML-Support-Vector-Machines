Post Operative Patient Admission ML Support Vector Machines
================
Rex Manglicmot

-   <a href="#status-continuing-working-document"
    id="toc-status-continuing-working-document">Status: Continuing Working
    Document</a>
-   <a href="#introduction" id="toc-introduction">Introduction</a>
-   <a href="#loading-the-libraries" id="toc-loading-the-libraries">Loading
    the Libraries</a>
-   <a href="#loading-the-data" id="toc-loading-the-data">Loading the
    Data</a>
-   <a href="#cleaning-the-data" id="toc-cleaning-the-data">Cleaning the
    Data</a>
-   <a href="#support-vector-machines"
    id="toc-support-vector-machines">Support Vector Machines</a>
-   <a href="#limitations" id="toc-limitations">Limitations</a>
-   <a href="#conclusions" id="toc-conclusions">Conclusions</a>
-   <a href="#inspiration-for-this-project"
    id="toc-inspiration-for-this-project">Inspiration for this project</a>

## Status: Continuing Working Document

## Introduction

The attributes are as follows:

1.  L-CORE (patient’s internal temperature in C): high (\> 37), mid (\>=
    36 and \<= 37), low (\< 36)

2.  L-SURF (patient’s surface temperature in C): high (\> 36.5), mid
    (\>= 36.5 and \<= 35), low (\< 35)

3.  L-O2 (oxygen saturation in %): excellent (\>= 98), good (\>= 90 and
    \< 98), fair (\>= 80 and \< 90), poor (\< 80)

4.  L-BP (last measurement of blood pressure): high (\> 130/90), mid
    (\<= 130/90 and \>= 90/70), low (\< 90/70)

5.  SURF-STBL (stability of patient’s surface temperature): stable,
    mod-stable, unstable

6.  CORE-STBL (stability of patient’s core temperature) stable,
    mod-stable, unstable

7.  BP-STBL (stability of patient’s blood pressure) stable, mod-stable,
    unstable

8.  COMFORT (patient’s perceived comfort at discharge, measured as an
    integer between 0 and 20)

9.  decision ADM-DECS (discharge decision): I (patient sent to Intensive
    Care Unit), S (patient prepared to go home), A (patient sent to
    general hospital floor)

## Loading the Libraries

``` r
library(tidyverse)
```

## Loading the Data

``` r
#create object to load files from the web
url <- 'https://archive.ics.uci.edu/ml/machine-learning-databases/postoperative-patient-data/post-operative.data'

#load the data
data <- read.csv(url, header=TRUE)
```

## Cleaning the Data

**OH BOY**, we got some cleaning to do!

``` r
#view the first few rows of the data
head(data)
```

    ##    mid  low excellent mid.1 stable stable.1   stable.2 X15  A
    ## 1  mid high excellent  high stable   stable     stable  10  S
    ## 2 high  low excellent  high stable   stable mod-stable  10  A
    ## 3  mid  low      good  high stable unstable mod-stable  15 A 
    ## 4  mid  mid excellent  high stable   stable     stable  10  A
    ## 5 high  low      good   mid stable   stable   unstable  15  S
    ## 6  mid  low excellent  high stable   stable mod-stable  05  S

``` r
dim(data)
```

    ## [1] 89  9

Calling the dim function, we have 89 rows and 9 columns. According to
the UCI website, there should be 90 rows. It would seem that the column
names are actually an observation and adding that back to the dataframe
would make the dataset whole. Let’s create a new row.

Also, because the original column names are missing from the dataset, we
would have to assume that the column names go in the order in which it
was presented on the UCI website. As such, I will rename the columns
accordingly.

``` r
#add another row the the dataset filled with values from the column
#row will added to the bottom of the dataset
data[nrow(data) +1,] <- c('mid', 'low', 'excellent', 'mid', 'stable', 'stable', 'stable', '15', 'A')

#check the last row
tail(data, 1)
```

    ##    mid low excellent mid.1 stable stable.1 stable.2 X15 A
    ## 90 mid low excellent   mid stable   stable   stable  15 A

``` r
#change column names and make them shorter
colnames(data) <- c('itemp', 'stemp', 'osat', 'bp', 'stabitemp', 'stabstep', 'stabosat', 'comf', 'deci')

#check if it worked
names(data)
```

    ## [1] "itemp"     "stemp"     "osat"      "bp"        "stabitemp" "stabstep" 
    ## [7] "stabosat"  "comf"      "deci"

Looks good!

``` r
#since most of the columns are fators lets change to factor class
data <- as.data.frame(unclass(data), stringsAsFactors = TRUE)

#change comf column to a numeric class
data$comf <- as.numeric(data$comf)

#check the class of all columns 
sapply(data, class)
```

    ##     itemp     stemp      osat        bp stabitemp  stabstep  stabosat      comf 
    ##  "factor"  "factor"  "factor"  "factor"  "factor"  "factor"  "factor" "numeric" 
    ##      deci 
    ##  "factor"

Looks good!

Let’s look for any NA values

``` r
#check for NAs
sum(is.na(data))
```

    ## [1] 0

``` r
#check for NAs via another way
any(is.na(data))
```

    ## [1] FALSE

``` r
#check for NAs a third way
which(is.na(data))
```

    ## integer(0)

``` r
#check a furth way #need to figure why a "2" is there
apply(is.na(data),2,sum)
```

    ##     itemp     stemp      osat        bp stabitemp  stabstep  stabosat      comf 
    ##         0         0         0         0         0         0         0         0 
    ##      deci 
    ##         0

``` r
#last check with sapply
sapply(data, function(x) sum(is.na(x)))
```

    ##     itemp     stemp      osat        bp stabitemp  stabstep  stabosat      comf 
    ##         0         0         0         0         0         0         0         0 
    ##      deci 
    ##         0

Looks good!

Convert the factors to numbers for model

## Support Vector Machines

## Limitations

## Conclusions

## Inspiration for this project
