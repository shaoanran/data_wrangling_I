Data Manupulation
================

## import datasets

``` r
litters_data =  read_csv("./data_import_examples/FAS_litters.csv")
```

    ## Parsed with column specification:
    ## cols(
    ##   Group = col_character(),
    ##   `Litter Number` = col_character(),
    ##   `GD0 weight` = col_double(),
    ##   `GD18 weight` = col_double(),
    ##   `GD of Birth` = col_double(),
    ##   `Pups born alive` = col_double(),
    ##   `Pups dead @ birth` = col_double(),
    ##   `Pups survive` = col_double()
    ## )

``` r
litters_data = janitor::clean_names(litters_data)

pups_data = read_csv("./data_import_examples/FAS_pups.csv")
```

    ## Parsed with column specification:
    ## cols(
    ##   `Litter Number` = col_character(),
    ##   Sex = col_double(),
    ##   `PD ears` = col_double(),
    ##   `PD eyes` = col_double(),
    ##   `PD pivot` = col_double(),
    ##   `PD walk` = col_double()
    ## )

``` r
pups_data = janitor::clean_names(pups_data)
```

## selecting \!\!\!

``` r
select(litters_data,group,litter_number)
```

    ## # A tibble: 49 x 2
    ##    group litter_number  
    ##    <chr> <chr>          
    ##  1 Con7  #85            
    ##  2 Con7  #1/2/95/2      
    ##  3 Con7  #5/5/3/83/3-3  
    ##  4 Con7  #5/4/2/95/2    
    ##  5 Con7  #4/2/95/3-3    
    ##  6 Con7  #2/2/95/3-2    
    ##  7 Con7  #1/5/3/83/3-3/2
    ##  8 Con8  #3/83/3-3      
    ##  9 Con8  #2/95/3        
    ## 10 Con8  #3/5/2/2/95    
    ## # … with 39 more rows

``` r
select(litters_data,group,litter_number,gd0_weight)
```

    ## # A tibble: 49 x 3
    ##    group litter_number   gd0_weight
    ##    <chr> <chr>                <dbl>
    ##  1 Con7  #85                   19.7
    ##  2 Con7  #1/2/95/2             27  
    ##  3 Con7  #5/5/3/83/3-3         26  
    ##  4 Con7  #5/4/2/95/2           28.5
    ##  5 Con7  #4/2/95/3-3           NA  
    ##  6 Con7  #2/2/95/3-2           NA  
    ##  7 Con7  #1/5/3/83/3-3/2       NA  
    ##  8 Con8  #3/83/3-3             NA  
    ##  9 Con8  #2/95/3               NA  
    ## 10 Con8  #3/5/2/2/95           28.5
    ## # … with 39 more rows

``` r
select(litters_data,group,gd0_weight, starts_with("pups"))
```

    ## # A tibble: 49 x 5
    ##    group gd0_weight pups_born_alive pups_dead_birth pups_survive
    ##    <chr>      <dbl>           <dbl>           <dbl>        <dbl>
    ##  1 Con7        19.7               3               4            3
    ##  2 Con7        27                 8               0            7
    ##  3 Con7        26                 6               0            5
    ##  4 Con7        28.5               5               1            4
    ##  5 Con7        NA                 6               0            6
    ##  6 Con7        NA                 6               0            4
    ##  7 Con7        NA                 9               0            9
    ##  8 Con8        NA                 9               1            8
    ##  9 Con8        NA                 8               0            8
    ## 10 Con8        28.5               8               0            8
    ## # … with 39 more rows

``` r
select(litters_data, litter_number,group,gd0_weight)
```

    ## # A tibble: 49 x 3
    ##    litter_number   group gd0_weight
    ##    <chr>           <chr>      <dbl>
    ##  1 #85             Con7        19.7
    ##  2 #1/2/95/2       Con7        27  
    ##  3 #5/5/3/83/3-3   Con7        26  
    ##  4 #5/4/2/95/2     Con7        28.5
    ##  5 #4/2/95/3-3     Con7        NA  
    ##  6 #2/2/95/3-2     Con7        NA  
    ##  7 #1/5/3/83/3-3/2 Con7        NA  
    ##  8 #3/83/3-3       Con8        NA  
    ##  9 #2/95/3         Con8        NA  
    ## 10 #3/5/2/2/95     Con8        28.5
    ## # … with 39 more rows

``` r
select(litters_data,gd0_weight,everything())
```

    ## # A tibble: 49 x 8
    ##    gd0_weight group litter_number gd18_weight gd_of_birth pups_born_alive
    ##         <dbl> <chr> <chr>               <dbl>       <dbl>           <dbl>
    ##  1       19.7 Con7  #85                  34.7          20               3
    ##  2       27   Con7  #1/2/95/2            42            19               8
    ##  3       26   Con7  #5/5/3/83/3-3        41.4          19               6
    ##  4       28.5 Con7  #5/4/2/95/2          44.1          19               5
    ##  5       NA   Con7  #4/2/95/3-3          NA            20               6
    ##  6       NA   Con7  #2/2/95/3-2          NA            20               6
    ##  7       NA   Con7  #1/5/3/83/3-…        NA            20               9
    ##  8       NA   Con8  #3/83/3-3            NA            20               9
    ##  9       NA   Con8  #2/95/3              NA            20               8
    ## 10       28.5 Con8  #3/5/2/2/95          NA            20               8
    ## # … with 39 more rows, and 2 more variables: pups_dead_birth <dbl>,
    ## #   pups_survive <dbl>

``` r
select(litters_data,-group)
```

    ## # A tibble: 49 x 7
    ##    litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr>              <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 #85                 19.7        34.7          20               3
    ##  2 #1/2/95/2           27          42            19               8
    ##  3 #5/5/3/83/3-3       26          41.4          19               6
    ##  4 #5/4/2/95/2         28.5        44.1          19               5
    ##  5 #4/2/95/3-3         NA          NA            20               6
    ##  6 #2/2/95/3-2         NA          NA            20               6
    ##  7 #1/5/3/83/3-…       NA          NA            20               9
    ##  8 #3/83/3-3           NA          NA            20               9
    ##  9 #2/95/3             NA          NA            20               8
    ## 10 #3/5/2/2/95         28.5        NA            20               8
    ## # … with 39 more rows, and 2 more variables: pups_dead_birth <dbl>,
    ## #   pups_survive <dbl>

``` r
select(litters_data,group,litter_number,gd0_weight:gd_of_birth)
```

    ## # A tibble: 49 x 5
    ##    group litter_number   gd0_weight gd18_weight gd_of_birth
    ##    <chr> <chr>                <dbl>       <dbl>       <dbl>
    ##  1 Con7  #85                   19.7        34.7          20
    ##  2 Con7  #1/2/95/2             27          42            19
    ##  3 Con7  #5/5/3/83/3-3         26          41.4          19
    ##  4 Con7  #5/4/2/95/2           28.5        44.1          19
    ##  5 Con7  #4/2/95/3-3           NA          NA            20
    ##  6 Con7  #2/2/95/3-2           NA          NA            20
    ##  7 Con7  #1/5/3/83/3-3/2       NA          NA            20
    ##  8 Con8  #3/83/3-3             NA          NA            20
    ##  9 Con8  #2/95/3               NA          NA            20
    ## 10 Con8  #3/5/2/2/95           28.5        NA            20
    ## # … with 39 more rows

``` r
select(litters_data,GROUP = group, litter_number)
```

    ## # A tibble: 49 x 2
    ##    GROUP litter_number  
    ##    <chr> <chr>          
    ##  1 Con7  #85            
    ##  2 Con7  #1/2/95/2      
    ##  3 Con7  #5/5/3/83/3-3  
    ##  4 Con7  #5/4/2/95/2    
    ##  5 Con7  #4/2/95/3-3    
    ##  6 Con7  #2/2/95/3-2    
    ##  7 Con7  #1/5/3/83/3-3/2
    ##  8 Con8  #3/83/3-3      
    ##  9 Con8  #2/95/3        
    ## 10 Con8  #3/5/2/2/95    
    ## # … with 39 more rows

``` r
rename(litters_data,GROUP = group)
```

    ## # A tibble: 49 x 8
    ##    GROUP litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>              <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 Con7  #85                 19.7        34.7          20               3
    ##  2 Con7  #1/2/95/2           27          42            19               8
    ##  3 Con7  #5/5/3/83/3-3       26          41.4          19               6
    ##  4 Con7  #5/4/2/95/2         28.5        44.1          19               5
    ##  5 Con7  #4/2/95/3-3         NA          NA            20               6
    ##  6 Con7  #2/2/95/3-2         NA          NA            20               6
    ##  7 Con7  #1/5/3/83/3-…       NA          NA            20               9
    ##  8 Con8  #3/83/3-3           NA          NA            20               9
    ##  9 Con8  #2/95/3             NA          NA            20               8
    ## 10 Con8  #3/5/2/2/95         28.5        NA            20               8
    ## # … with 39 more rows, and 2 more variables: pups_dead_birth <dbl>,
    ## #   pups_survive <dbl>

***sequencing; renaming the variable; detemrine the first and last
variable The difference between 35 and 33: 35 is only changing the
variable name and show all of variables. 35 not only changed the
variable name, but also choose the variables to be shown. ***

## filtering \!\!\!

``` r
filter(litters_data, group == "Mod8")
```

    ## # A tibble: 7 x 8
    ##   group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##   <chr> <chr>              <dbl>       <dbl>       <dbl>           <dbl>
    ## 1 Mod8  #97                 24.5        42.8          20               8
    ## 2 Mod8  #5/93               NA          41.1          20              11
    ## 3 Mod8  #5/93/2             NA          NA            19               8
    ## 4 Mod8  #7/82-3-2           26.9        43.2          20               7
    ## 5 Mod8  #7/110/3-2          27.5        46            19               8
    ## 6 Mod8  #2/95/2             28.5        44.5          20               9
    ## 7 Mod8  #82/4               33.4        52.7          20               8
    ## # … with 2 more variables: pups_dead_birth <dbl>, pups_survive <dbl>

``` r
filter(litters_data, gd_of_birth == 20)
```

    ## # A tibble: 32 x 8
    ##    group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>              <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 Con7  #85                 19.7        34.7          20               3
    ##  2 Con7  #4/2/95/3-3         NA          NA            20               6
    ##  3 Con7  #2/2/95/3-2         NA          NA            20               6
    ##  4 Con7  #1/5/3/83/3-…       NA          NA            20               9
    ##  5 Con8  #3/83/3-3           NA          NA            20               9
    ##  6 Con8  #2/95/3             NA          NA            20               8
    ##  7 Con8  #3/5/2/2/95         28.5        NA            20               8
    ##  8 Con8  #1/6/2/2/95-2       NA          NA            20               7
    ##  9 Con8  #3/5/3/83/3-…       NA          NA            20               8
    ## 10 Con8  #3/6/2/2/95-3       NA          NA            20               7
    ## # … with 22 more rows, and 2 more variables: pups_dead_birth <dbl>,
    ## #   pups_survive <dbl>

``` r
filter(litters_data, gd_of_birth < 20)
```

    ## # A tibble: 17 x 8
    ##    group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>              <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 Con7  #1/2/95/2           27          42            19               8
    ##  2 Con7  #5/5/3/83/3-3       26          41.4          19               6
    ##  3 Con7  #5/4/2/95/2         28.5        44.1          19               5
    ##  4 Con8  #5/4/3/83/3         28          NA            19               9
    ##  5 Con8  #2/2/95/2           NA          NA            19               5
    ##  6 Mod7  #59                 17          33.4          19               8
    ##  7 Mod7  #103                21.4        42.1          19               9
    ##  8 Mod7  #1/82/3-2           NA          NA            19               6
    ##  9 Mod7  #3/83/3-2           NA          NA            19               8
    ## 10 Mod7  #4/2/95/2           23.5        NA            19               9
    ## 11 Mod7  #5/3/83/5-2         22.6        37            19               5
    ## 12 Mod7  #94/2               24.4        42.9          19               7
    ## 13 Mod7  #62                 19.5        35.9          19               7
    ## 14 Low7  #112                23.9        40.5          19               6
    ## 15 Mod8  #5/93/2             NA          NA            19               8
    ## 16 Mod8  #7/110/3-2          27.5        46            19               8
    ## 17 Low8  #79                 25.4        43.8          19               8
    ## # … with 2 more variables: pups_dead_birth <dbl>, pups_survive <dbl>

``` r
filter(litters_data, gd_of_birth >= 20)
```

    ## # A tibble: 32 x 8
    ##    group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>              <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 Con7  #85                 19.7        34.7          20               3
    ##  2 Con7  #4/2/95/3-3         NA          NA            20               6
    ##  3 Con7  #2/2/95/3-2         NA          NA            20               6
    ##  4 Con7  #1/5/3/83/3-…       NA          NA            20               9
    ##  5 Con8  #3/83/3-3           NA          NA            20               9
    ##  6 Con8  #2/95/3             NA          NA            20               8
    ##  7 Con8  #3/5/2/2/95         28.5        NA            20               8
    ##  8 Con8  #1/6/2/2/95-2       NA          NA            20               7
    ##  9 Con8  #3/5/3/83/3-…       NA          NA            20               8
    ## 10 Con8  #3/6/2/2/95-3       NA          NA            20               7
    ## # … with 22 more rows, and 2 more variables: pups_dead_birth <dbl>,
    ## #   pups_survive <dbl>

``` r
filter(litters_data,gd_of_birth < 6, group == "Con7")
```

    ## # A tibble: 0 x 8
    ## # … with 8 variables: group <chr>, litter_number <chr>, gd0_weight <dbl>,
    ## #   gd18_weight <dbl>, gd_of_birth <dbl>, pups_born_alive <dbl>,
    ## #   pups_dead_birth <dbl>, pups_survive <dbl>

``` r
# following two lines produce same results##
filter(litters_data,group == "Con7" | group == "Mod8")
```

    ## # A tibble: 14 x 8
    ##    group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>              <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 Con7  #85                 19.7        34.7          20               3
    ##  2 Con7  #1/2/95/2           27          42            19               8
    ##  3 Con7  #5/5/3/83/3-3       26          41.4          19               6
    ##  4 Con7  #5/4/2/95/2         28.5        44.1          19               5
    ##  5 Con7  #4/2/95/3-3         NA          NA            20               6
    ##  6 Con7  #2/2/95/3-2         NA          NA            20               6
    ##  7 Con7  #1/5/3/83/3-…       NA          NA            20               9
    ##  8 Mod8  #97                 24.5        42.8          20               8
    ##  9 Mod8  #5/93               NA          41.1          20              11
    ## 10 Mod8  #5/93/2             NA          NA            19               8
    ## 11 Mod8  #7/82-3-2           26.9        43.2          20               7
    ## 12 Mod8  #7/110/3-2          27.5        46            19               8
    ## 13 Mod8  #2/95/2             28.5        44.5          20               9
    ## 14 Mod8  #82/4               33.4        52.7          20               8
    ## # … with 2 more variables: pups_dead_birth <dbl>, pups_survive <dbl>

``` r
filter(litters_data,group %in% c("Con7","Mod8"))
```

    ## # A tibble: 14 x 8
    ##    group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>              <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 Con7  #85                 19.7        34.7          20               3
    ##  2 Con7  #1/2/95/2           27          42            19               8
    ##  3 Con7  #5/5/3/83/3-3       26          41.4          19               6
    ##  4 Con7  #5/4/2/95/2         28.5        44.1          19               5
    ##  5 Con7  #4/2/95/3-3         NA          NA            20               6
    ##  6 Con7  #2/2/95/3-2         NA          NA            20               6
    ##  7 Con7  #1/5/3/83/3-…       NA          NA            20               9
    ##  8 Mod8  #97                 24.5        42.8          20               8
    ##  9 Mod8  #5/93               NA          41.1          20              11
    ## 10 Mod8  #5/93/2             NA          NA            19               8
    ## 11 Mod8  #7/82-3-2           26.9        43.2          20               7
    ## 12 Mod8  #7/110/3-2          27.5        46            19               8
    ## 13 Mod8  #2/95/2             28.5        44.5          20               9
    ## 14 Mod8  #82/4               33.4        52.7          20               8
    ## # … with 2 more variables: pups_dead_birth <dbl>, pups_survive <dbl>

``` r
filter(litters_data,gd0_weight + gd18_weight < 70)
```

    ## # A tibble: 23 x 8
    ##    group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>              <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 Con7  #85                 19.7        34.7          20               3
    ##  2 Con7  #1/2/95/2           27          42            19               8
    ##  3 Con7  #5/5/3/83/3-3       26          41.4          19               6
    ##  4 Mod7  #59                 17          33.4          19               8
    ##  5 Mod7  #103                21.4        42.1          19               9
    ##  6 Mod7  #5/3/83/5-2         22.6        37            19               5
    ##  7 Mod7  #106                21.7        37.8          20               5
    ##  8 Mod7  #94/2               24.4        42.9          19               7
    ##  9 Mod7  #62                 19.5        35.9          19               7
    ## 10 Low7  #84/2               24.3        40.8          20               8
    ## # … with 13 more rows, and 2 more variables: pups_dead_birth <dbl>,
    ## #   pups_survive <dbl>

``` r
#getting the missing value, but don't do this please when we return the dataset, they only have missing values.#
filter(litters_data, is.na(gd0_weight))
```

    ## # A tibble: 15 x 8
    ##    group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>              <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 Con7  #4/2/95/3-3           NA        NA            20               6
    ##  2 Con7  #2/2/95/3-2           NA        NA            20               6
    ##  3 Con7  #1/5/3/83/3-…         NA        NA            20               9
    ##  4 Con8  #3/83/3-3             NA        NA            20               9
    ##  5 Con8  #2/95/3               NA        NA            20               8
    ##  6 Con8  #1/6/2/2/95-2         NA        NA            20               7
    ##  7 Con8  #3/5/3/83/3-…         NA        NA            20               8
    ##  8 Con8  #2/2/95/2             NA        NA            19               5
    ##  9 Con8  #3/6/2/2/95-3         NA        NA            20               7
    ## 10 Mod7  #1/82/3-2             NA        NA            19               6
    ## 11 Mod7  #3/83/3-2             NA        NA            19               8
    ## 12 Mod7  #2/95/2-2             NA        NA            20               7
    ## 13 Mod7  #8/110/3-2            NA        NA            20               9
    ## 14 Mod8  #5/93                 NA        41.1          20              11
    ## 15 Mod8  #5/93/2               NA        NA            19               8
    ## # … with 2 more variables: pups_dead_birth <dbl>, pups_survive <dbl>

``` r
# what we did instead: dropping the missing values under gd0_weight"# 
drop_na(litters_data,gd0_weight)
```

    ## # A tibble: 34 x 8
    ##    group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>              <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 Con7  #85                 19.7        34.7          20               3
    ##  2 Con7  #1/2/95/2           27          42            19               8
    ##  3 Con7  #5/5/3/83/3-3       26          41.4          19               6
    ##  4 Con7  #5/4/2/95/2         28.5        44.1          19               5
    ##  5 Con8  #3/5/2/2/95         28.5        NA            20               8
    ##  6 Con8  #5/4/3/83/3         28          NA            19               9
    ##  7 Mod7  #59                 17          33.4          19               8
    ##  8 Mod7  #103                21.4        42.1          19               9
    ##  9 Mod7  #3/82/3-2           28          45.9          20               5
    ## 10 Mod7  #4/2/95/2           23.5        NA            19               9
    ## # … with 24 more rows, and 2 more variables: pups_dead_birth <dbl>,
    ## #   pups_survive <dbl>

\*\*\* “==” is to asking question, whether the value is the specific
thing in the dataset. “=” is assigning a value to variable. we can put
multiple conditions together. \! –\> not, can be put outside of logical
condition. %in% –\> check more than one groups
