Investigate FOI Request Timing changes with min max data
================
Peter Jordan
04/10/2020

``` r
library(tidyverse)
```

    ## ── Attaching packages ───────────────────────────────────────── tidyverse 1.3.0 ──

    ## ✓ ggplot2 3.3.2     ✓ purrr   0.3.4
    ## ✓ tibble  3.0.3     ✓ dplyr   1.0.2
    ## ✓ tidyr   1.1.2     ✓ stringr 1.4.0
    ## ✓ readr   1.3.1     ✓ forcats 0.5.0

    ## ── Conflicts ──────────────────────────────────────────── tidyverse_conflicts() ──
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

## Import FOI Request Timing changes with min max data (converted to csv)

``` r
timing_changes <- read_csv("FOI_Request_Timing_changes_with_min_max_data.csv")
```

    ## Parsed with column specification:
    ## cols(
    ##   SCN = col_character(),
    ##   Address = col_character(),
    ##   `Type of installation` = col_character(),
    ##   Latitude = col_double(),
    ##   Longitude = col_double(),
    ##   `Operating Mode before Covid 19` = col_character(),
    ##   `Operating Mode for recovery phase` = col_character(),
    ##   `MIN Vehicle Green (seconds)` = col_character(),
    ##   `MAX Vehicle Green (seconds)` = col_character()
    ## )

``` r
head(timing_changes)
```

    ## # A tibble: 6 x 9
    ##   SCN   Address `Type of instal… Latitude Longitude `Operating Mode…
    ##   <chr> <chr>   <chr>               <dbl>     <dbl> <chr>           
    ## 1 PEL0… [PEL00… Pelican Crossing     51.3    -0.757 VA              
    ## 2 PEL0… [PEL01… Pelican Crossing     51.2    -0.753 VA              
    ## 3 PEL0… [PEL03… Pelican Crossing     51.2    -0.971 VA              
    ## 4 PEL0… [PEL04… Pelican Crossing     51.3    -0.954 VA              
    ## 5 PEL0… [PEL04… Pelican Crossing     51.1    -1.32  SCOOT           
    ## 6 PEL0… [PEL05… Pelican Crossing     50.8    -1.12  VA              
    ## # … with 3 more variables: `Operating Mode for recovery phase` <chr>, `MIN
    ## #   Vehicle Green (seconds)` <chr>, `MAX Vehicle Green (seconds)` <chr>

## Filter on addresses in Winchester

``` r
timing_changes %>% 
filter(str_detect(Address, "Winchester:"))
```

    ## # A tibble: 14 x 9
    ##    SCN   Address `Type of instal… Latitude Longitude `Operating Mode…
    ##    <chr> <chr>   <chr>               <dbl>     <dbl> <chr>           
    ##  1 PEL0… [PEL04… Pelican Crossing     51.1     -1.32 SCOOT           
    ##  2 PUF0… [PUF04… Puffin Crossing      51.1     -1.31 VA              
    ##  3 PUF0… [PUF04… Puffin Crossing      51.1     -1.31 SCOOT           
    ##  4 PUF0… [PUF04… Puffin Crossing      51.1     -1.31 VA              
    ##  5 PUF0… [PUF05… Puffin Crossing      51.1     -1.31 SCOOT           
    ##  6 PUF0… [PUF05… Puffin Crossing      51.1     -1.31 VA              
    ##  7 PUF1… [PUF18… Puffin Crossing      51.0     -1.32 VA              
    ##  8 PUF1… [PUF18… Puffin Crossing      51.1     -1.33 VA              
    ##  9 PUF1… [PUF18… Puffin Crossing      51.1     -1.31 VA              
    ## 10 PUF1… [PUF18… Puffin Crossing      51.1     -1.34 VA              
    ## 11 PUF2… [PUF21… Puffin Crossing      51.1     -1.32 VA              
    ## 12 PUF2… [PUF22… Puffin Crossing      51.1     -1.32 VA              
    ## 13 SIG0… [SIG05… Traffic signal …     51.1     -1.32 SCOOT           
    ## 14 SIG0… [SIG05… Traffic signal …     51.1     -1.32 Fixed time UTC  
    ## # … with 3 more variables: `Operating Mode for recovery phase` <chr>, `MIN
    ## #   Vehicle Green (seconds)` <chr>, `MAX Vehicle Green (seconds)` <chr>
