Hilliary vs. Trump: Number of Campaign Stops
================

# The Setup

``` r
library(tidyverse)
```

    ## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.1 ──

    ## ✓ ggplot2 3.3.5     ✓ purrr   0.3.4
    ## ✓ tibble  3.1.6     ✓ dplyr   1.0.7
    ## ✓ tidyr   1.1.4     ✓ stringr 1.4.0
    ## ✓ readr   2.1.1     ✓ forcats 0.5.1

    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

``` r
library(fivethirtyeight)
```

    ## Some larger datasets need to be installed separately, like senators and
    ## house_district_forecast. To install these, we recommend you install the
    ## fivethirtyeightdata package by running:
    ## install.packages('fivethirtyeightdata', repos =
    ## 'https://fivethirtyeightdata.github.io/drat/', type = 'source')

``` r
library(dplyr)
library(lubridate)
```

    ## 
    ## Attaching package: 'lubridate'

    ## The following objects are masked from 'package:base':
    ## 
    ##     date, intersect, setdiff, union

# The Code

``` r
pres_2016_trail
```

    ## # A tibble: 177 × 5
    ##    candidate date       location                     lat   lng
    ##    <chr>     <date>     <chr>                      <dbl> <dbl>
    ##  1 Clinton   2016-09-05 Cleveland, Ohio             41.5 -81.7
    ##  2 Clinton   2016-09-05 Hampton, Illinois           41.6 -90.4
    ##  3 Clinton   2016-09-06 Tampa, Florida              28.0 -82.5
    ##  4 Clinton   2016-09-07 New York City, New York     40.7 -74.0
    ##  5 Clinton   2016-09-08 Charlotte, North Carolina   35.2 -80.8
    ##  6 Clinton   2016-09-08 Kansas City, Missouri       39.1 -94.6
    ##  7 Clinton   2016-09-09 New York City, New York     40.7 -74.0
    ##  8 Clinton   2016-09-12 New York City, New York     40.7 -74.0
    ##  9 Clinton   2016-09-15 Greensboro, North Carolina  36.1 -79.8
    ## 10 Clinton   2016-09-15 Washington, DC              38.9 -77.0
    ## # … with 167 more rows

``` r
weekly_campaign_stops <- pres_2016_trail %>% 
  mutate(week = floor_date(date, unit = "week")) %>%
  group_by(candidate, week) %>% 
  summarize(number_of_stops = n())
```

    ## `summarise()` has grouped output by 'candidate'. You can override using the `.groups` argument.

# The Visualization

```{r pressure, echo=FALSE}
ggplot(data = weekly_campaign_stops, mapping = aes(x = candidate, y = number_of_stops)) + geom_col() + labs(x = "Candidate", y = "Number of Stops")
```

![](README_files/figure-gfm/pressure-1.png)<!-- -->
