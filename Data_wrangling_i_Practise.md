Data_wrangling_i
================
09.16.2025

``` r
library(tidyverse)
```

    ## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ## ✔ dplyr     1.1.4     ✔ readr     2.1.5
    ## ✔ forcats   1.0.0     ✔ stringr   1.5.1
    ## ✔ ggplot2   4.0.0     ✔ tibble    3.3.0
    ## ✔ lubridate 1.9.4     ✔ tidyr     1.3.1
    ## ✔ purrr     1.1.0     
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()
    ## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

## Read some data, but first import it, and make variable names all lower case.

``` r
litters_df = read_csv(file = "./data_import_examples/FAS_litters.csv")
```

    ## Rows: 49 Columns: 8
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (4): Group, Litter Number, GD0 weight, GD18 weight
    ## dbl (4): GD of Birth, Pups born alive, Pups dead @ birth, Pups survive
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
names(litters_df)
```

    ## [1] "Group"             "Litter Number"     "GD0 weight"       
    ## [4] "GD18 weight"       "GD of Birth"       "Pups born alive"  
    ## [7] "Pups dead @ birth" "Pups survive"

``` r
## use the janitor :: clean_names() function to put the variable names into snake lower case

litters_df = janitor::clean_names(litters_df)
names(litters_df)
```

    ## [1] "group"           "litter_number"   "gd0_weight"      "gd18_weight"    
    ## [5] "gd_of_birth"     "pups_born_alive" "pups_dead_birth" "pups_survive"

## Importing the pups_df, and making all variables lower case.

``` r
pups_df = read_csv(file = "./data_import_examples/FAS_pups.csv")
```

    ## New names:
    ## Rows: 316 Columns: 6
    ## ── Column specification
    ## ──────────────────────────────────────────────────────── Delimiter: "," chr
    ## (6): ...1, 1 = male, 2 = female, ...3, ...4, ...5, ...6
    ## ℹ Use `spec()` to retrieve the full column specification for this data. ℹ
    ## Specify the column types or set `show_col_types = FALSE` to quiet this message.
    ## • `` -> `...1`
    ## • `` -> `...3`
    ## • `` -> `...4`
    ## • `` -> `...5`
    ## • `` -> `...6`

``` r
names(pups_df)
```

    ## [1] "...1"                 "1 = male, 2 = female" "...3"                
    ## [4] "...4"                 "...5"                 "...6"

``` r
## use the janitor :: clean_names() function to put the variable names into snake lower case

litters_df = janitor::clean_names(pups_df)
names(pups_df)
```

    ## [1] "...1"                 "1 = male, 2 = female" "...3"                
    ## [4] "...4"                 "...5"                 "...6"

### Looking at the data, and the head and tail.

``` r
litters_df
```

    ## # A tibble: 316 × 6
    ##    x1            x1_male_2_female x3      x4      x5       x6     
    ##    <chr>         <chr>            <chr>   <chr>   <chr>    <chr>  
    ##  1 <NA>          <NA>             <NA>    <NA>    <NA>     <NA>   
    ##  2 <NA>          <NA>             <NA>    <NA>    <NA>     <NA>   
    ##  3 Litter Number Sex              PD ears PD eyes PD pivot PD walk
    ##  4 #85           1                4       13      7        11     
    ##  5 #85           1                4       13      7        12     
    ##  6 #1/2/95/2     1                5       13      7        9      
    ##  7 #1/2/95/2     1                5       13      8        10     
    ##  8 #5/5/3/83/3-3 1                5       13      8        10     
    ##  9 #5/5/3/83/3-3 1                5       14      6        9      
    ## 10 #5/4/2/95/2   1                .       14      5        9      
    ## # ℹ 306 more rows

``` r
head(litters_df, 5)
```

    ## # A tibble: 5 × 6
    ##   x1            x1_male_2_female x3      x4      x5       x6     
    ##   <chr>         <chr>            <chr>   <chr>   <chr>    <chr>  
    ## 1 <NA>          <NA>             <NA>    <NA>    <NA>     <NA>   
    ## 2 <NA>          <NA>             <NA>    <NA>    <NA>     <NA>   
    ## 3 Litter Number Sex              PD ears PD eyes PD pivot PD walk
    ## 4 #85           1                4       13      7        11     
    ## 5 #85           1                4       13      7        12

``` r
tail(litters_df, 5)
```

    ## # A tibble: 5 × 6
    ##   x1      x1_male_2_female x3    x4    x5    x6   
    ##   <chr>   <chr>            <chr> <chr> <chr> <chr>
    ## 1 #2/95/2 2                3     13    6     8    
    ## 2 #2/95/2 2                3     13    7     9    
    ## 3 #82/4   2                4     13    7     9    
    ## 4 #82/4   2                3     13    7     9    
    ## 5 #82/4   2                3     13    7     9

### Using the skimr function to quickly look at data.

``` r
skimr::skim(litters_df)
```

|                                                  |            |
|:-------------------------------------------------|:-----------|
| Name                                             | litters_df |
| Number of rows                                   | 316        |
| Number of columns                                | 6          |
| \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_   |            |
| Column type frequency:                           |            |
| character                                        | 6          |
| \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ |            |
| Group variables                                  | None       |

Data summary

**Variable type: character**

| skim_variable    | n_missing | complete_rate | min | max | empty | n_unique | whitespace |
|:-----------------|----------:|--------------:|----:|----:|------:|---------:|-----------:|
| x1               |         2 |          0.99 |   3 |  15 |     0 |       50 |          0 |
| x1_male_2_female |         2 |          0.99 |   1 |   3 |     0 |        3 |          0 |
| x3               |         2 |          0.99 |   1 |   7 |     0 |        6 |          0 |
| x4               |        15 |          0.95 |   2 |   7 |     0 |        5 |          0 |
| x5               |        15 |          0.95 |   1 |   8 |     0 |       10 |          0 |
| x6               |         2 |          0.99 |   1 |   7 |     0 |        9 |          0 |

### Arguments to read

``` r
litters_df = 
    read_csv(file = "./data_import_examples/FAS_litters.csv",
    skip = 10, col_names = FALSE)
```

    ## Rows: 40 Columns: 8
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (4): X1, X2, X3, X4
    ## dbl (4): X5, X6, X7, X8
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
head(litters_df)
```

    ## # A tibble: 6 × 8
    ##   X1    X2              X3    X4       X5    X6    X7    X8
    ##   <chr> <chr>           <chr> <chr> <dbl> <dbl> <dbl> <dbl>
    ## 1 Con8  #3/5/2/2/95     28.5  <NA>     20     8     0     8
    ## 2 Con8  #5/4/3/83/3     28    <NA>     19     9     0     8
    ## 3 Con8  #1/6/2/2/95-2   <NA>  <NA>     20     7     0     6
    ## 4 Con8  #3/5/3/83/3-3-2 <NA>  <NA>     20     8     0     8
    ## 5 Con8  #2/2/95/2       <NA>  <NA>     19     5     0     4
    ## 6 Con8  #3/6/2/2/95-3   <NA>  <NA>     20     7     0     7

### Excluding the missing vaulues

``` r
litters_df = 
    read_csv(
        file = "./data_import_examples/FAS_litters.csv",
        na = c(".", "NA", ""))
```

    ## Rows: 49 Columns: 8
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (2): Group, Litter Number
    ## dbl (6): GD0 weight, GD18 weight, GD of Birth, Pups born alive, Pups dead @ ...
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
head(litters_df)
```

    ## # A tibble: 6 × 8
    ##   Group `Litter Number` `GD0 weight` `GD18 weight` `GD of Birth`
    ##   <chr> <chr>                  <dbl>         <dbl>         <dbl>
    ## 1 Con7  #85                     19.7          34.7            20
    ## 2 Con7  #1/2/95/2               27            42              19
    ## 3 Con7  #5/5/3/83/3-3           26            41.4            19
    ## 4 Con7  #5/4/2/95/2             28.5          44.1            19
    ## 5 Con7  #4/2/95/3-3             NA            NA              20
    ## 6 Con7  #2/2/95/3-2             NA            NA              20
    ## # ℹ 3 more variables: `Pups born alive` <dbl>, `Pups dead @ birth` <dbl>,
    ## #   `Pups survive` <dbl>

### Parsing columns

`In some cases, you’ll want to give explicit column specifications. This is done using the cols function, where you can give each column a type.`

``` r
litters_df = 
    read_csv(file = "./data_import_examples/FAS_litters.csv",
        na = c(".", "NA", ""),
    col_types = cols(
      Group = col_character(),
      `Litter Number` = col_character(),
      `GD0 weight` = col_double(),
      `GD18 weight` = col_double(),
      `GD of Birth` = col_integer(),
      `Pups born alive` = col_integer(),
      `Pups dead @ birth` = col_integer(),
      `Pups survive` = col_integer()
    )
  )

tail(litters_df)
```

    ## # A tibble: 6 × 8
    ##   Group `Litter Number` `GD0 weight` `GD18 weight` `GD of Birth`
    ##   <chr> <chr>                  <dbl>         <dbl>         <int>
    ## 1 Low8  #79                     25.4          43.8            19
    ## 2 Low8  #100                    20            39.2            20
    ## 3 Low8  #4/84                   21.8          35.2            20
    ## 4 Low8  #108                    25.6          47.5            20
    ## 5 Low8  #99                     23.5          39              20
    ## 6 Low8  #110                    25.5          42.7            20
    ## # ℹ 3 more variables: `Pups born alive` <int>, `Pups dead @ birth` <int>,
    ## #   `Pups survive` <int>

`Note that you don’t have to specify the variable type for every column, and can only focus on ones that are difficult:`

``` r
litters_df = 
    read_csv(file = "./data_import_examples/FAS_litters.csv",
        na = c(".", "NA", ""),
    col_types = cols(
      Group = col_factor()
    )
)

head(litters_df)
```

    ## # A tibble: 6 × 8
    ##   Group `Litter Number` `GD0 weight` `GD18 weight` `GD of Birth`
    ##   <fct> <chr>                  <dbl>         <dbl>         <dbl>
    ## 1 Con7  #85                     19.7          34.7            20
    ## 2 Con7  #1/2/95/2               27            42              19
    ## 3 Con7  #5/5/3/83/3-3           26            41.4            19
    ## 4 Con7  #5/4/2/95/2             28.5          44.1            19
    ## 5 Con7  #4/2/95/3-3             NA            NA              20
    ## 6 Con7  #2/2/95/3-2             NA            NA              20
    ## # ℹ 3 more variables: `Pups born alive` <dbl>, `Pups dead @ birth` <dbl>,
    ## #   `Pups survive` <dbl>

#### Learning Assessment 1

``` r
pups_df = 
    read_csv(file = "./data_import_examples/FAS_pups.csv",
    skip = 3, col_names = FALSE)
```

    ## Rows: 314 Columns: 6
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (6): X1, X2, X3, X4, X5, X6
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
head(pups_df)
```

    ## # A tibble: 6 × 6
    ##   X1            X2    X3      X4      X5       X6     
    ##   <chr>         <chr> <chr>   <chr>   <chr>    <chr>  
    ## 1 Litter Number Sex   PD ears PD eyes PD pivot PD walk
    ## 2 #85           1     4       13      7        11     
    ## 3 #85           1     4       13      7        12     
    ## 4 #1/2/95/2     1     5       13      7        9      
    ## 5 #1/2/95/2     1     5       13      8        10     
    ## 6 #5/5/3/83/3-3 1     5       13      8        10

`excluding missing values.`

``` r
pups_df = 
    read_csv(
        file = "./data_import_examples/FAS_pups.csv",
        skip = 3,
        na = c(".", "NA", ""))
```

    ## Rows: 313 Columns: 6
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (1): Litter Number
    ## dbl (5): Sex, PD ears, PD eyes, PD pivot, PD walk
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
head(pups_df)
```

    ## # A tibble: 6 × 6
    ##   `Litter Number`   Sex `PD ears` `PD eyes` `PD pivot` `PD walk`
    ##   <chr>           <dbl>     <dbl>     <dbl>      <dbl>     <dbl>
    ## 1 #85                 1         4        13          7        11
    ## 2 #85                 1         4        13          7        12
    ## 3 #1/2/95/2           1         5        13          7         9
    ## 4 #1/2/95/2           1         5        13          8        10
    ## 5 #5/5/3/83/3-3       1         5        13          8        10
    ## 6 #5/5/3/83/3-3       1         5        14          6         9

`parsing columns`

``` r
pups_df = 
    read_csv(file = "./data_import_examples/FAS_pups.csv",
        skip = 3,
        na = c(".", "NA", ""),
    col_types = cols(
      `...1` = col_factor(),
      `1 = male, 2 = female` = col_double(),
      `...3` = col_double(),
      `...4` = col_double(),
      `...5` = col_double(),
      `...6` = col_double(),
      
    )
  )
```

    ## Warning: The following named parsers don't match the column names: ...1, 1 =
    ## male, 2 = female, ...3, ...4, ...5, ...6

``` r
skimr::skim(pups_df)
```

|                                                  |         |
|:-------------------------------------------------|:--------|
| Name                                             | pups_df |
| Number of rows                                   | 313     |
| Number of columns                                | 6       |
| \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_   |         |
| Column type frequency:                           |         |
| character                                        | 1       |
| numeric                                          | 5       |
| \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ |         |
| Group variables                                  | None    |

Data summary

**Variable type: character**

| skim_variable | n_missing | complete_rate | min | max | empty | n_unique | whitespace |
|:--------------|----------:|--------------:|----:|----:|------:|---------:|-----------:|
| Litter Number |         0 |             1 |   3 |  15 |     0 |       49 |          0 |

**Variable type: numeric**

| skim_variable | n_missing | complete_rate |  mean |   sd |  p0 | p25 | p50 | p75 | p100 | hist  |
|:--------------|----------:|--------------:|------:|-----:|----:|----:|----:|----:|-----:|:------|
| Sex           |         0 |          1.00 |  1.50 | 0.50 |   1 |   1 |   2 |   2 |    2 | ▇▁▁▁▇ |
| PD ears       |        18 |          0.94 |  3.68 | 0.59 |   2 |   3 |   4 |   4 |    5 | ▁▅▁▇▁ |
| PD eyes       |        13 |          0.96 | 12.99 | 0.62 |  12 |  13 |  13 |  13 |   15 | ▂▇▁▂▁ |
| PD pivot      |        13 |          0.96 |  7.09 | 1.51 |   4 |   6 |   7 |   8 |   12 | ▂▇▂▂▁ |
| PD walk       |         0 |          1.00 |  9.50 | 1.34 |   7 |   9 |   9 |  10 |   14 | ▆▇▇▂▁ |

`This works as well`

``` r
pups_df = 
    read_csv("./data_import_examples/FAS_pups.csv",
        na = c(".", "NA"), col_types = "fddddd")
```

    ## New names:
    ## • `` -> `...1`
    ## • `` -> `...3`
    ## • `` -> `...4`
    ## • `` -> `...5`
    ## • `` -> `...6`

    ## Warning: One or more parsing issues, call `problems()` on your data frame for details,
    ## e.g.:
    ##   dat <- vroom(...)
    ##   problems(dat)

``` r
skimr::skim(pups_df)
```

    ## Warning: There was 1 warning in `dplyr::summarize()`.
    ## ℹ In argument: `dplyr::across(tidyselect::any_of(variable_names),
    ##   mangled_skimmers$funs)`.
    ## ℹ In group 0: .
    ## Caused by warning:
    ## ! There was 1 warning in `dplyr::summarize()`.
    ## ℹ In argument: `dplyr::across(tidyselect::any_of(variable_names),
    ##   mangled_skimmers$funs)`.
    ## Caused by warning in `sorted_count()`:
    ## ! Variable contains value(s) of "" that have been converted to "empty".

|                                                  |         |
|:-------------------------------------------------|:--------|
| Name                                             | pups_df |
| Number of rows                                   | 316     |
| Number of columns                                | 6       |
| \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_   |         |
| Column type frequency:                           |         |
| factor                                           | 1       |
| numeric                                          | 5       |
| \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ |         |
| Group variables                                  | None    |

Data summary

**Variable type: factor**

| skim_variable | n_missing | complete_rate | ordered | n_unique | top_counts |
|:---|---:|---:|:---|---:|:---|
| …1 | 0 | 1 | FALSE | 51 | \#1/: 9, \#98: 9, \#10: 9, \#10: 9 |

**Variable type: numeric**

| skim_variable        | n_missing | complete_rate |  mean |   sd |  p0 | p25 | p50 | p75 | p100 | hist  |
|:---------------------|----------:|--------------:|------:|-----:|----:|----:|----:|----:|-----:|:------|
| 1 = male, 2 = female |         3 |          0.99 |  1.50 | 0.50 |   1 |   1 |   2 |   2 |    2 | ▇▁▁▁▇ |
| …3                   |        21 |          0.93 |  3.68 | 0.59 |   2 |   3 |   4 |   4 |    5 | ▁▅▁▇▁ |
| …4                   |        16 |          0.95 | 12.99 | 0.62 |  12 |  13 |  13 |  13 |   15 | ▂▇▁▂▁ |
| …5                   |        16 |          0.95 |  7.09 | 1.51 |   4 |   6 |   7 |   8 |   12 | ▂▇▂▂▁ |
| …6                   |         3 |          0.99 |  9.50 | 1.34 |   7 |   9 |   9 |  10 |   14 | ▆▇▇▂▁ |

### Other file formats
