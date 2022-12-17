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

OH BOY, we got some cleaning to do!

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

## Support Vector Machines

## Limitations

## Conclusions

## Inspiration for this project
