Homework 10: Decisions and loops
================
Katelyn Houghton

# Decisions

Write a function that accepts the current time as a parameter and prints
“Good morning”, “Good afternoon”, or “Good evening” depending on the
time. It is fine for the time to be in numeric format (e.g., `2317` for
11:17 pm). Bonus points if the function accepts time objects (see the
`lubridate` package).

``` r
library(lubridate)
library(tidyverse)

greet <- function(time = lubridate::now()) {
  if(is.numeric(time)){
    hr <- time
  } else {
    hr <- lubridate::hour(time) 
  }
  if (hr < 12) {
    print("good morning")
  } else if (hr < 17) {
    print("good afternoon")
  } else if (hr < 25) {
    print("good evening")
  } else {
    print("give me something from 0 to 24")
  }
  
}

greet()
```

    [1] "good morning"

``` r
greet(8)
```

    [1] "good morning"

``` r
greet(13)
```

    [1] "good afternoon"

``` r
greet(24)
```

    [1] "good evening"

``` r
greet(25)
```

    [1] "give me something from 0 to 24"

A few questions to consider:

-   What is a logical name for this function? What is a logical name for
    the parameter it accepts?

    **Answer**: Greet or Greeting. Hr (but not h)

-   The purpose of this function is to print a message to the console,
    so its primary purpose is a **side effect**. However, all functions
    must return something. What would be a logical value for this
    function to return?

    **Answer**: a object

-   Should the function have default behavior in case the user does not
    pass an argument?

    **Answer**: yes, just passes the current time the argument is
    supplied via lubridate::now

-   What would you like to happen if this function is passed the wrong
    data type (e.g., a negative number)?

    **Answer**: will give NA

# Loops

-   Write a `for` loops that calculates the mean of each column of
    mtcars

``` r
mtcars.mean <- vector("double", ncol(mtcars))
names(mtcars.mean) <- names(mtcars)
for (i in names(mtcars)) {
  mtcars.mean[i] <- mean(mtcars[[i]])
}
mtcars.mean
```

           mpg        cyl       disp         hp       drat         wt       qsec 
     20.090625   6.187500 230.721875 146.687500   3.596563   3.217250  17.848750 
            vs         am       gear       carb 
      0.437500   0.406250   3.687500   2.812500 

-   Write a function (using a for loop) that calculates the mean of all
    numeric columns of *any* data frame. This function should be able to
    accept data frames with non-numeric columns.

``` r
# using the diamonds dataset to test
# first i am just creating a new df with only 
# numeric and then just passing that into the
# function :)

df.is.numeric <- select_if(diamonds, is.numeric)
column.mean <- vector("double", ncol(df.is.numeric))  
for (i in seq_along(df.is.numeric)) {            
  column.mean[[i]] <- mean(df.is.numeric[[i]])      
}

column.mean
```

    [1]    0.7979397   61.7494049   57.4571839 3932.7997219    5.7311572
    [6]    5.7345260    3.5387338

## Why not loops

In R, we generally encourage people to use vectorized functions instead
of `for` loops. According to [your
textbook](https://r4ds.had.co.nz/iteration.html), what is better about
vectorized functions?

**Answer**: Vectorizing functions will element wise calculations, so
less prone to error. Loops you must pass the elements to it each time,
increasing your chances of error.
