Hmk_05
================
Katelyn

Please read the entire [R for Data
Science](https://r4ds.had.co.nz/transform.html) before you do this
homework.

This homework relies on the `nycflights13` package, which contains
several data frames, including `airlines`, `airports`, `flights`,
`planes`, and `weather`. Loading `nycflights13` puts all of these data
frames on the search path, so that they are available automatically,
just like `mpg` or `mtcars`.

## Installing data packages

Remember that any package needs to be installed only once (per version
of R), but needs to be loaded every time we start a new R session.

To install `nyclflights13`, we use `install.packages("nycflights13")`
(with quotation marks). To load it, we use `library(nycflights13)`.

``` r
library(nycflights13)
library(tidyverse)
?flights
?nycflights13
```

# Question 1: filtering

Make a plot of air time (Y) as a function of distance (X) for all
flights that meet the following criteria:

-   originate from LaGuardia airport (“LGA”)
-   departed on the 16th of the month
-   have a flight distance of less than 2000

``` r
q1 <- filter(flights, origin == "LGA", day == 16, distance < 2000)

ggplot(q1, aes(x = distance, y = air_time)) +
  geom_point()
```

![](hmk_05_files/figure-gfm/unnamed-chunk-2-1.png)

# Question 2: dealing with NAs

Make a data frame of all of the rows of `flights` that have values for
*both* `arr_time` and `dep_time` - that is, neither of those values are
`NA`.

``` r
q2 <- filter(flights, arr_time > 0, dep_time > 0)
```

## filtering NAs

`ggplot()` will automatically remove NA values from the plot, as you may
have seen in question 1, but it emits a warning message about that. Of
course you could silence the warning message using [chunk
options](https://bookdown.org/yihui/rmarkdown-cookbook/chunk-options.html),
but how could you prevent them from appearing in the first place?

``` r
#There are two options I can think of here. First is to use the filter function for all the variables you want to graph, since it automatically will remove NAs. 

#Second you can create your new data frame and then use the function drop_na()

q1 %>% drop_na() #where q1 is the dataframe we want to clean up
```

    # A tibble: 3,291 × 19
        year month   day dep_time sched_de…¹ dep_d…² arr_t…³ sched…⁴ arr_d…⁵ carrier
       <int> <int> <int>    <int>      <int>   <dbl>   <int>   <int>   <dbl> <chr>  
     1  2013     1    16        2       2125     157     119    2250     149 MQ     
     2  2013     1    16      552        600      -8     920     904      16 B6     
     3  2013     1    16      555        600      -5     859     815      44 FL     
     4  2013     1    16      555        600      -5     917     825      52 MQ     
     5  2013     1    16      557        600      -3     720     659      21 US     
     6  2013     1    16      600        600       0     952     910      42 AA     
     7  2013     1    16      601        600       1     734     724      10 EV     
     8  2013     1    16      603        600       3     802     703      59 US     
     9  2013     1    16      605        610      -5    1002     915      47 AA     
    10  2013     1    16      612        600      12     818     759      19 DL     
    # … with 3,281 more rows, 9 more variables: flight <int>, tailnum <chr>,
    #   origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>, hour <dbl>,
    #   minute <dbl>, time_hour <dttm>, and abbreviated variable names
    #   ¹​sched_dep_time, ²​dep_delay, ³​arr_time, ⁴​sched_arr_time, ⁵​arr_delay

`q1 %>% drop_na() #where q1 is the dataframe we want to clean up`

# Question 3: adding columns

Create a data frame of average flight speeds, based on `air_time` and
`distance`. Make either a histogram or a density plot of the data. If
you like, you may break the data out (e.g. by airline, or some other
variable) in a way that you think makes sense.

``` r
q3 <- flights %>%
  mutate(avg_speed = 60*(distance / air_time))

q3alternate <- mutate(flights, avg_speed = 60*(distance / air_time))

ggplot(data = q3, aes(x = avg_speed)) +
  geom_histogram(color = "black", fill = "red")
```

![](hmk_05_files/figure-gfm/unnamed-chunk-5-1.png)
