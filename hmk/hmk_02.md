hmk_02
================
Katelyn Houghton

## Homework \#2

Chunk out the messages when a package is loaded.

``` r
library(tidyverse)
```

The rest of the homework

``` r
a <- 103

b <- 3

a > b 
```

    [1] TRUE

``` r
ls()
```

    [1] "a" "b"

``` r
rm(list=ls())

ls()
```

    character(0)

## Question 4: why rm(list = ls()) works

-   **rm()** will remove objects from a specified environment.
-   **list** argument in rm function provides the specific location for
    objects to be removed
-   **ls()** function will list all the objects in an environment that
    we want removed \*outcome = cleared all objects in global
    environment

## Search Function

How R uses search paths to find objects. This is a function in “base” R
that will return a list of packages.

``` r
search()
```

     [1] ".GlobalEnv"        "package:forcats"   "package:stringr"  
     [4] "package:dplyr"     "package:purrr"     "package:readr"    
     [7] "package:tidyr"     "package:tibble"    "package:ggplot2"  
    [10] "package:tidyverse" "tools:quarto"      "package:stats"    
    [13] "package:graphics"  "package:grDevices" "package:utils"    
    [16] "package:datasets"  "package:methods"   "Autoloads"        
    [19] "package:base"     
