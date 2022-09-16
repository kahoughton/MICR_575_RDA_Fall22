Homework 3
================
Katelyn

# Data input/output

Use the tidyverse `read_csv()` function to read a .csv file of your own
data. If you don’t have any data of your own, make up an excel file with
fake data.

``` r
library(tidyverse)

#Load my data file 
pups <- read.csv("hmk_03_data.csv")
```

# Investigating the properties of data frames

Use two different functions that both give some kind of summary or
overview of the data frame. Which one do you think is more useful?

``` r
head(pups)
```

      Pups Age Weight.lbs Fluff.factor Fetch.skills
    1 Sage  10         35           10            5
    2 Blue   7         40            9           10

``` r
glimpse(pups)
```

    Rows: 2
    Columns: 5
    $ Pups         <chr> "Sage", "Blue"
    $ Age          <int> 10, 7
    $ Weight.lbs   <int> 35, 40
    $ Fluff.factor <int> 10, 9
    $ Fetch.skills <int> 5, 10

I found the \#head function more helpful because it arranged the summary
in a table style that was easy to view. Also we can use “summary” or
“str”

``` r
summary(pups)
```

         Pups                Age          Weight.lbs     Fluff.factor  
     Length:2           Min.   : 7.00   Min.   :35.00   Min.   : 9.00  
     Class :character   1st Qu.: 7.75   1st Qu.:36.25   1st Qu.: 9.25  
     Mode  :character   Median : 8.50   Median :37.50   Median : 9.50  
                        Mean   : 8.50   Mean   :37.50   Mean   : 9.50  
                        3rd Qu.: 9.25   3rd Qu.:38.75   3rd Qu.: 9.75  
                        Max.   :10.00   Max.   :40.00   Max.   :10.00  
      Fetch.skills  
     Min.   : 5.00  
     1st Qu.: 6.25  
     Median : 7.50  
     Mean   : 7.50  
     3rd Qu.: 8.75  
     Max.   :10.00  

``` r
str(pups)
```

    'data.frame':   2 obs. of  5 variables:
     $ Pups        : chr  "Sage" "Blue"
     $ Age         : int  10 7
     $ Weight.lbs  : int  35 40
     $ Fluff.factor: int  10 9
     $ Fetch.skills: int  5 10

# Manipulating data frames

Create a new column of your data frame by performing some kind of
arithmetic operation on an existing column.

``` r
Fluff.percent <- pups$Fluff.factor *10

cbind(pups, Fluff.percent)
```

      Pups Age Weight.lbs Fluff.factor Fetch.skills Fluff.percent
    1 Sage  10         35           10            5           100
    2 Blue   7         40            9           10            90

# Working on columns

Calculate the mean of a numeric column in your data frame.

``` r
mean(pups$Fetch.skills)
```

    [1] 7.5

# Accessing elements of data frames

-   [Challenge 3 from SC Data Structures
    lesson](https://swcarpentry.github.io/r-novice-gapminder/04-data-structures-part1/index.html#challenge-3):
    Show what each of the following returns, and explain what each line
    of code is doing: \*\*Doing this instead for my pups data frame
    -   `pups[1] this will call the first column, and lay it out top to bottom`
    -   `pups[[1]] this will call the first column, but list the rows`
    -   `pups$Age this calls the data from the Age column`
    -   `pups[1, 1] this calls the data in the first row and column position`
    -   `pups[ , 1] this calls everything in the first column, but leaving a specific row blank`
    -   `pups[1, ] this calls the first row`

``` r
pups[1]
```

      Pups
    1 Sage
    2 Blue

``` r
pups[[1]]
```

    [1] "Sage" "Blue"

``` r
pups$Age
```

    [1] 10  7

``` r
pups[1, 1]
```

    [1] "Sage"

``` r
pups[ , 1]
```

    [1] "Sage" "Blue"

``` r
pups[1, ]
```

      Pups Age Weight.lbs Fluff.factor Fetch.skills
    1 Sage  10         35           10            5

# Optional challenge

A data frame is an example of a list. I haven’t discussed how to access
elements of lists, but it is covered
[here](https://swcarpentry.github.io/r-novice-gapminder/04-data-structures-part1/index.html#lists)).

Explain in what ways accessing elements of lists are like accessing
columns of data frames, and given that, how it shows that data frames
are a type of list.

# Subsetting our dataframe

https://swcarpentry.github.io/r-novice-gapminder/06-data-subsetting/index.html

We can subset using logical operations

``` r
pups[c(TRUE, FALSE, TRUE, TRUE) , ]
```

         Pups Age Weight.lbs Fluff.factor Fetch.skills
    1    Sage  10         35           10            5
    NA   <NA>  NA         NA           NA           NA
    NA.1 <NA>  NA         NA           NA           NA

We can subset using logical test of dogs that are ten years old

``` r
pups[pups$Age == 10, ]
```

      Pups Age Weight.lbs Fluff.factor Fetch.skills
    1 Sage  10         35           10            5

Select dogs that are seven years or older

``` r
pups[pups$Age >= 7, ]
```

      Pups Age Weight.lbs Fluff.factor Fetch.skills
    1 Sage  10         35           10            5
    2 Blue   7         40            9           10
