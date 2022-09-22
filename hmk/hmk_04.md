Homework 4
================
Katelyn

## Homework 4

Create your own graph, that is not a scatterplot.

``` r
library(tidyverse)

syn <- read.csv("hmk4.csv")

ggplot(syn, aes(x = day, y = cells.mL)) +
  geom_point() +
  geom_line() +
  scale_y_continuous(trans='log10') +
  theme_minimal() 
```

![](hmk_04_files/figure-gfm/unnamed-chunk-1-1.png)
