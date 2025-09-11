Problem Set 1
================
Sam Zlot
Sys.Date(9/10/25)\`

### Introduction

This problem set is designed to test your understanding of data
wrangling concepts using the **`tidyverse`**, specifically **`dplyr`**
and **`tidyr`**, as well as foundational R concepts. You’ll primarily
work with the `mtcars`, a simulated sales dataset, and new simulated
student demographic/grade datasets, applying core verbs and functions to
prepare data for analysis. This activity should take approximately 60
minutes.

### Instructions

- Read each task carefully.
- Write your R code in the provided code chunks.
- Run the code to see your output and verify your results.
- `mtcars` is a built-in R dataset (or part of the `tidyverse`
  installation).

------------------------------------------------------------------------

## Part 0: R Fundamentals (10 minutes)

This section will test your understanding of basic R syntax, data types,
and vector operations.

### Task 0.1: Data Types and Logical Operations

1.  Create a variable `course_name` and assign it the string
    `"Introduction to Data Science"`.
2.  Create a variable `num_students` and assign it the integer value
    `45`.
3.  Check the data type (`class()`) of `course_name` and `num_students`.
4.  Create a numeric variable `pi_value` with the value $3.14159$.
5.  Create a logical variable `is_active` and set it to `TRUE`.
6.  Evaluate the following logical expressions and print their results:
    - Is `num_students` greater than or equal to `50`?
    - Is `course_name` exactly equal to `"introduction to data science"`
      (case-sensitive)?

``` r
course_name <- "Introduction to Data Science"
num_students <- 45
class(course_name)
```

    ## [1] "character"

``` r
class(num_students)
```

    ## [1] "numeric"

``` r
pi_value <- 3.14159
is_active = TRUE
num_students >= 50
```

    ## [1] FALSE

``` r
course_name == "introduction to data sciene"
```

    ## [1] FALSE

------------------------------------------------------------------------

### Task 0.2: Working with Vectors

1.  Create a numeric vector named `temperatures` with the values
    $22, 25, 19, 28, 23$.
2.  Calculate the `sum()` and `mean()` of the `temperatures` vector.
3.  Add a new temperature, $30$, to the `temperatures` vector (re-assign
    the variable).
4.  Create a new logical vector named `is_hot` that is `TRUE` for
    temperatures greater than $25$ and `FALSE` otherwise.

``` r
temperatures <- c(22, 25, 19, 28, 23)
sum(temperatures)
```

    ## [1] 117

``` r
mean(temperatures)
```

    ## [1] 23.4

``` r
temperatures <- c(22, 25, 19, 28, 30)
is_hot <- temperatures > 25
temperatures
```

    ## [1] 22 25 19 28 30

``` r
is_hot
```

    ## [1] FALSE FALSE FALSE  TRUE  TRUE

------------------------------------------------------------------------

## Part 1: `dplyr` Fundamentals with `mtcars` (25 minutes)

This section focuses on applying core `dplyr` verbs to the classic
`mtcars` dataset. The `mtcars` dataset contains information about
various car models from 1973-74.

### Task 1.1: Filtering and Arranging

1.  The `mtcars` dataset has been pre-processed for you to include
    `car_model` as a column.
2.  Filter the dataset to include only cars with `cyl` (number of
    cylinders) equal to `4` or `6` AND `mpg` (miles per gallon) greater
    than `20`.
3.  Arrange the results first by `mpg` in ascending order, and then by
    `cyl` in descending order.

``` r
mtcars_processed <- mtcars %>%
  rownames_to_column("car_model")

mtcars %>% filter(cyl == 4 & mpg > 20)
```

    ##                 mpg cyl  disp  hp drat    wt  qsec vs am gear carb
    ## Datsun 710     22.8   4 108.0  93 3.85 2.320 18.61  1  1    4    1
    ## Merc 240D      24.4   4 146.7  62 3.69 3.190 20.00  1  0    4    2
    ## Merc 230       22.8   4 140.8  95 3.92 3.150 22.90  1  0    4    2
    ## Fiat 128       32.4   4  78.7  66 4.08 2.200 19.47  1  1    4    1
    ## Honda Civic    30.4   4  75.7  52 4.93 1.615 18.52  1  1    4    2
    ## Toyota Corolla 33.9   4  71.1  65 4.22 1.835 19.90  1  1    4    1
    ## Toyota Corona  21.5   4 120.1  97 3.70 2.465 20.01  1  0    3    1
    ## Fiat X1-9      27.3   4  79.0  66 4.08 1.935 18.90  1  1    4    1
    ## Porsche 914-2  26.0   4 120.3  91 4.43 2.140 16.70  0  1    5    2
    ## Lotus Europa   30.4   4  95.1 113 3.77 1.513 16.90  1  1    5    2
    ## Volvo 142E     21.4   4 121.0 109 4.11 2.780 18.60  1  1    4    2

``` r
mtcars %>% arrange(mpg, desc(cyl))
```

    ##                      mpg cyl  disp  hp drat    wt  qsec vs am gear carb
    ## Cadillac Fleetwood  10.4   8 472.0 205 2.93 5.250 17.98  0  0    3    4
    ## Lincoln Continental 10.4   8 460.0 215 3.00 5.424 17.82  0  0    3    4
    ## Camaro Z28          13.3   8 350.0 245 3.73 3.840 15.41  0  0    3    4
    ## Duster 360          14.3   8 360.0 245 3.21 3.570 15.84  0  0    3    4
    ## Chrysler Imperial   14.7   8 440.0 230 3.23 5.345 17.42  0  0    3    4
    ## Maserati Bora       15.0   8 301.0 335 3.54 3.570 14.60  0  1    5    8
    ## Merc 450SLC         15.2   8 275.8 180 3.07 3.780 18.00  0  0    3    3
    ## AMC Javelin         15.2   8 304.0 150 3.15 3.435 17.30  0  0    3    2
    ## Dodge Challenger    15.5   8 318.0 150 2.76 3.520 16.87  0  0    3    2
    ## Ford Pantera L      15.8   8 351.0 264 4.22 3.170 14.50  0  1    5    4
    ## Merc 450SE          16.4   8 275.8 180 3.07 4.070 17.40  0  0    3    3
    ## Merc 450SL          17.3   8 275.8 180 3.07 3.730 17.60  0  0    3    3
    ## Merc 280C           17.8   6 167.6 123 3.92 3.440 18.90  1  0    4    4
    ## Valiant             18.1   6 225.0 105 2.76 3.460 20.22  1  0    3    1
    ## Hornet Sportabout   18.7   8 360.0 175 3.15 3.440 17.02  0  0    3    2
    ## Pontiac Firebird    19.2   8 400.0 175 3.08 3.845 17.05  0  0    3    2
    ## Merc 280            19.2   6 167.6 123 3.92 3.440 18.30  1  0    4    4
    ## Ferrari Dino        19.7   6 145.0 175 3.62 2.770 15.50  0  1    5    6
    ## Mazda RX4           21.0   6 160.0 110 3.90 2.620 16.46  0  1    4    4
    ## Mazda RX4 Wag       21.0   6 160.0 110 3.90 2.875 17.02  0  1    4    4
    ## Hornet 4 Drive      21.4   6 258.0 110 3.08 3.215 19.44  1  0    3    1
    ## Volvo 142E          21.4   4 121.0 109 4.11 2.780 18.60  1  1    4    2
    ## Toyota Corona       21.5   4 120.1  97 3.70 2.465 20.01  1  0    3    1
    ## Datsun 710          22.8   4 108.0  93 3.85 2.320 18.61  1  1    4    1
    ## Merc 230            22.8   4 140.8  95 3.92 3.150 22.90  1  0    4    2
    ## Merc 240D           24.4   4 146.7  62 3.69 3.190 20.00  1  0    4    2
    ## Porsche 914-2       26.0   4 120.3  91 4.43 2.140 16.70  0  1    5    2
    ## Fiat X1-9           27.3   4  79.0  66 4.08 1.935 18.90  1  1    4    1
    ## Honda Civic         30.4   4  75.7  52 4.93 1.615 18.52  1  1    4    2
    ## Lotus Europa        30.4   4  95.1 113 3.77 1.513 16.90  1  1    5    2
    ## Fiat 128            32.4   4  78.7  66 4.08 2.200 19.47  1  1    4    1
    ## Toyota Corolla      33.9   4  71.1  65 4.22 1.835 19.90  1  1    4    1

### Short Answer

Based on your filtered and arranged results, briefly describe the
characteristics of the cars that appear at the top of your output. What
does this tell you about the relationship between cylinders and miles
per gallon in this subset?

## Having only four cylinders results in a more fuel efficient car since engine is lighter and has less capabilities. Rather for the eight cylinder cars the fuel efficiency is much less due to the heavier and stronger engine.

### Task 1.2: Mutating and Selecting

Using the `mtcars_processed` dataset:

1.  Create a new column `hp_per_wt` by dividing `hp` (horsepower) by
    `wt` (weight in 1000 lbs).
2.  Create another new column `qsec_category` based on `qsec` (1/4 mile
    time):
    - `"Fast"` if `qsec < 17`
    - `"Medium"` if `qsec >= 17` and `qsec < 19`
    - `"Slow"` if `qsec >= 19`
3.  Select only the `car_model`, `mpg`, `hp`, `wt`, `hp_per_wt`, and
    `qsec_category` columns.

``` r
mtcars %>% 
  mutate(
    hp_per_wt = hp / wt,
    qsec_category = ifelse(qsec < 17, "Fast",
                     ifelse(qsec >= 17 & qsec < 19, "Medium",
                     ifelse(qsec >= 19, "Slow", NA)))
  ) %>%

select( mpg, hp, wt, hp_per_wt, qsec_category)
```

    ##                      mpg  hp    wt hp_per_wt qsec_category
    ## Mazda RX4           21.0 110 2.620  41.98473          Fast
    ## Mazda RX4 Wag       21.0 110 2.875  38.26087        Medium
    ## Datsun 710          22.8  93 2.320  40.08621        Medium
    ## Hornet 4 Drive      21.4 110 3.215  34.21462          Slow
    ## Hornet Sportabout   18.7 175 3.440  50.87209        Medium
    ## Valiant             18.1 105 3.460  30.34682          Slow
    ## Duster 360          14.3 245 3.570  68.62745          Fast
    ## Merc 240D           24.4  62 3.190  19.43574          Slow
    ## Merc 230            22.8  95 3.150  30.15873          Slow
    ## Merc 280            19.2 123 3.440  35.75581        Medium
    ## Merc 280C           17.8 123 3.440  35.75581        Medium
    ## Merc 450SE          16.4 180 4.070  44.22604        Medium
    ## Merc 450SL          17.3 180 3.730  48.25737        Medium
    ## Merc 450SLC         15.2 180 3.780  47.61905        Medium
    ## Cadillac Fleetwood  10.4 205 5.250  39.04762        Medium
    ## Lincoln Continental 10.4 215 5.424  39.63864        Medium
    ## Chrysler Imperial   14.7 230 5.345  43.03087        Medium
    ## Fiat 128            32.4  66 2.200  30.00000          Slow
    ## Honda Civic         30.4  52 1.615  32.19814        Medium
    ## Toyota Corolla      33.9  65 1.835  35.42234          Slow
    ## Toyota Corona       21.5  97 2.465  39.35091          Slow
    ## Dodge Challenger    15.5 150 3.520  42.61364          Fast
    ## AMC Javelin         15.2 150 3.435  43.66812        Medium
    ## Camaro Z28          13.3 245 3.840  63.80208          Fast
    ## Pontiac Firebird    19.2 175 3.845  45.51365        Medium
    ## Fiat X1-9           27.3  66 1.935  34.10853        Medium
    ## Porsche 914-2       26.0  91 2.140  42.52336          Fast
    ## Lotus Europa        30.4 113 1.513  74.68605          Fast
    ## Ford Pantera L      15.8 264 3.170  83.28076          Fast
    ## Ferrari Dino        19.7 175 2.770  63.17690          Fast
    ## Maserati Bora       15.0 335 3.570  93.83754          Fast
    ## Volvo 142E          21.4 109 2.780  39.20863        Medium

### Short Answer

Why might creating `hp_per_wt` and `qsec_category` be useful metrics
when analyzing car performance, beyond just raw horsepower and weight?

## Horse power divided by weight is helpful since usually a bigger engine that provides more horse power weighs more so can see pound for pound the most powerful car. The qsec for category just makes it easier to comprehend how fast the car is for someone not knowledgeable of how fast cars are for a quarter mile time.

### Task 1.3: Grouped Summaries

Using the `mtcars_processed` dataset:

1.  Group the data by `cyl` (number of cylinders) and `am` (transmission
    type: 0 for automatic, 1 for manual).
2.  For each group, calculate the **average `mpg`**, the **median
    `hp`**, and the **number of cars** (`n()`).
3.  Arrange the final result first by `cyl` (ascending) and then by
    `average_mpg` (descending).

``` r
mtcars %>%
  group_by(cyl, am)%>% 
  summarise(
    average_mpg = mean(mpg, na.rm = TRUE),
    median_hp = median(hp, na.rm = TRUE),
    number_cars = n()
  ) %>%
arrange(cyl, desc(average_mpg))
```

    ## # A tibble: 6 × 5
    ## # Groups:   cyl [3]
    ##     cyl    am average_mpg median_hp number_cars
    ##   <dbl> <dbl>       <dbl>     <dbl>       <int>
    ## 1     4     1        28.1      78.5           8
    ## 2     4     0        22.9      95             3
    ## 3     6     1        20.6     110             3
    ## 4     6     0        19.1     116.            4
    ## 5     8     1        15.4     300.            2
    ## 6     8     0        15.0     180            12

### Short Answer

Based on your grouped summary, what general trends do you observe
regarding average `mpg` and median `hp` across different combinations of
`cylinders` and `transmission` types? How do these summaries help
differentiate car characteristics?

## What I noticed is that the less cylinders leads to higher mpg but also less horse power. I noticed too for each type manual car for the same cylinders has more fuel efficiency.

## Part 2: Reshaping and Joining Data (25 minutes)

For this part, we’ll explore reshaping and joining using a simulated
sales dataset and new simulated student enrollment data.

**Run this code chunk first to set up the data:**

``` r
# Part 2 Data Setup
product_sales_wide <- tibble(
  product = c("Laptop", "Monitor", "Keyboard"),
  `2020` = c(1000, 500, 800),
  `2021` = c(1100, 550, 850),
  `2022` = c(1250, 600, 900)
) %>%
  rename(Year_2020 = `2020`, Year_2021 = `2021`, Year_2022 = `2022`) # Rename to avoid issues with non-syntactic names

# Simulated Student and Grade Data
students_demographics <- tibble(
  student_id = c("S001", "S002", "S003", "S004", "S005", "S007"), # S007 is a new student, no grades yet
  student_name = c("Alice", "Bob", "Charlie", "David", "Eve", "Frank"),
  major = c("CS", "Math", "Physics", "CS", "Biology", "History"),
  enrollment_year = c(2020, 2021, 2020, 2022, 2021, 2023)
)

student_grades <- tibble(
  student_id = c("S001", "S002", "S003", "S001", "S006", "S004"), # S006 has grades but no demographic info
  course_id = c("CS101", "MA201", "PH301", "CS102", "BI101", "CS205"),
  semester = c("Fall 2020", "Spring 2022", "Fall 2021", "Spring 2021", "Fall 2021", "Spring 2023"),
  grade_score = c(92, 85, 88, 78, 75, 90) # Assuming numeric scores for easier calculation
)

# Display the dataframes
print(product_sales_wide)
```

    ## # A tibble: 3 × 4
    ##   product  Year_2020 Year_2021 Year_2022
    ##   <chr>        <dbl>     <dbl>     <dbl>
    ## 1 Laptop        1000      1100      1250
    ## 2 Monitor        500       550       600
    ## 3 Keyboard       800       850       900

``` r
print(students_demographics)
```

    ## # A tibble: 6 × 4
    ##   student_id student_name major   enrollment_year
    ##   <chr>      <chr>        <chr>             <dbl>
    ## 1 S001       Alice        CS                 2020
    ## 2 S002       Bob          Math               2021
    ## 3 S003       Charlie      Physics            2020
    ## 4 S004       David        CS                 2022
    ## 5 S005       Eve          Biology            2021
    ## 6 S007       Frank        History            2023

``` r
print(student_grades)
```

    ## # A tibble: 6 × 4
    ##   student_id course_id semester    grade_score
    ##   <chr>      <chr>     <chr>             <dbl>
    ## 1 S001       CS101     Fall 2020            92
    ## 2 S002       MA201     Spring 2022          85
    ## 3 S003       PH301     Fall 2021            88
    ## 4 S001       CS102     Spring 2021          78
    ## 5 S006       BI101     Fall 2021            75
    ## 6 S004       CS205     Spring 2023          90

------------------------------------------------------------------------

### Task 2.1: New Variable Creation: Wide vs. Long (`product_sales` dataset)

This task demonstrates how creating new variables that depend on
previous time periods is much easier in a long (tidy) format.

1.  **Analysis in Wide Format:** Using the `product_sales_wide` dataset,
    create new columns for the **year-over-year growth rate** for 2021
    and 2022.
    - `Growth_2021`: `(Year_2021 - Year_2020) / Year_2020 * 100`
    - `Growth_2022`: `(Year_2022 - Year_2021) / Year_2021 * 100`

``` r
product_sales_wide %>%
  mutate(
    Growth_2021 = (Year_2021 - Year_2020) / Year_2020 * 100,
    Growth_2022 = (Year_2022 - Year_2021) / Year_2021 * 100
  )
```

    ## # A tibble: 3 × 6
    ##   product  Year_2020 Year_2021 Year_2022 Growth_2021 Growth_2022
    ##   <chr>        <dbl>     <dbl>     <dbl>       <dbl>       <dbl>
    ## 1 Laptop        1000      1100      1250       10          13.6 
    ## 2 Monitor        500       550       600       10           9.09
    ## 3 Keyboard       800       850       900        6.25        5.88

2.  **Reshape to Long Format:** Reshape `product_sales_wide` into a long
    format called `product_sales_long`. Pivot the year columns
    (`Year_2020`, `Year_2021`, `Year_2022`) into two new columns: `Year`
    and `Sales`. Make sure `Year` is numeric.

``` r
product_sales_long <- product_sales_wide %>%
  pivot_longer(
    cols = starts_with("Year_"),
    names_to = "Year",
    values_to = "Sales"
  ) %>%
mutate(Year = as.numeric(str_remove(Year, "Year_")))
product_sales_long
```

    ## # A tibble: 9 × 3
    ##   product   Year Sales
    ##   <chr>    <dbl> <dbl>
    ## 1 Laptop    2020  1000
    ## 2 Laptop    2021  1100
    ## 3 Laptop    2022  1250
    ## 4 Monitor   2020   500
    ## 5 Monitor   2021   550
    ## 6 Monitor   2022   600
    ## 7 Keyboard  2020   800
    ## 8 Keyboard  2021   850
    ## 9 Keyboard  2022   900

3.  **Analysis in Long Format:** Using the `product_sales_long` dataset,
    calculate a single `Growth_Rate` column that represents the
    year-over-year growth for each product. You should use `group_by()`
    and `lag()`. The formula for growth rate is
    `(current_year_sales - previous_year_sales) / previous_year_sales * 100`.

``` r
product_sales_long_growth <- product_sales_long %>% 
  group_by(product) %>%
  arrange(Year, .by_group = TRUE) %>%
  mutate(
    Growth_Rate = ((Sales - lag(Sales)) / lag(Sales)) * 100
  ) 
product_sales_long_growth
```

    ## # A tibble: 9 × 4
    ## # Groups:   product [3]
    ##   product   Year Sales Growth_Rate
    ##   <chr>    <dbl> <dbl>       <dbl>
    ## 1 Keyboard  2020   800       NA   
    ## 2 Keyboard  2021   850        6.25
    ## 3 Keyboard  2022   900        5.88
    ## 4 Laptop    2020  1000       NA   
    ## 5 Laptop    2021  1100       10   
    ## 6 Laptop    2022  1250       13.6 
    ## 7 Monitor   2020   500       NA   
    ## 8 Monitor   2021   550       10   
    ## 9 Monitor   2022   600        9.09

### Short Answer

Compare the code required to calculate the year-over-year growth rate in
the wide format versus the long format. Which approach is more concise
and scalable if you had many more years of data? Why is the long format
generally preferred for this type of time-series calculation?

## The wide format might be more concise and scale able since it’s more has the product only listed once and shows only year 2021 and 2022 growth since 2020 is the base year. The long format is generally preferred since will automatically any years added on rather need to manually code each year for wide format.

### Task 2.2: Mutating Joins: Student Demographics and Grades

This task explores combining student demographic information with their
academic performance. Pay close attention to how different join types
handle students who may or may not have corresponding grade records.

1.  **Inner Join:** Perform an `inner_join()` to combine
    `students_demographics` with `student_grades` based on `student_id`.
    This will show students who have **both** demographic information
    and at least one grade record.
2.  **Left Join:** Perform a `left_join()` to combine
    `students_demographics` (left table) with `student_grades` based on
    `student_id`. This will keep **all students** from the demographic
    data and add their grade records where available.
3.  **Advanced Mutate (after Left Join):** After performing the left
    join, calculate the **average `grade_score` for each student**. This
    will require grouping by `student_id` and `student_name`.

``` r
students_demographics %>%
  inner_join(student_grades, by = "student_id")  
```

    ## # A tibble: 5 × 7
    ##   student_id student_name major   enrollment_year course_id semester grade_score
    ##   <chr>      <chr>        <chr>             <dbl> <chr>     <chr>          <dbl>
    ## 1 S001       Alice        CS                 2020 CS101     Fall 20…          92
    ## 2 S001       Alice        CS                 2020 CS102     Spring …          78
    ## 3 S002       Bob          Math               2021 MA201     Spring …          85
    ## 4 S003       Charlie      Physics            2020 PH301     Fall 20…          88
    ## 5 S004       David        CS                 2022 CS205     Spring …          90

``` r
students_demographics %>% 
  left_join(student_grades, by = "student_id") %>% 
  group_by(student_id, student_name) %>%
  mutate(avg_grade = mean(grade_score, na.rm = TRUE))
```

    ## # A tibble: 7 × 8
    ## # Groups:   student_id, student_name [6]
    ##   student_id student_name major   enrollment_year course_id semester grade_score
    ##   <chr>      <chr>        <chr>             <dbl> <chr>     <chr>          <dbl>
    ## 1 S001       Alice        CS                 2020 CS101     Fall 20…          92
    ## 2 S001       Alice        CS                 2020 CS102     Spring …          78
    ## 3 S002       Bob          Math               2021 MA201     Spring …          85
    ## 4 S003       Charlie      Physics            2020 PH301     Fall 20…          88
    ## 5 S004       David        CS                 2022 CS205     Spring …          90
    ## 6 S005       Eve          Biology            2021 <NA>      <NA>              NA
    ## 7 S007       Frank        History            2023 <NA>      <NA>              NA
    ## # ℹ 1 more variable: avg_grade <dbl>

### Short Answer

Compare the number of rows and the content of the `inner_join()` and
`left_join()` results. Specifically, identify which student(s) are
present in one join but not the other, and explain why. What does the
average grade calculation reveal about students with multiple grades or
no grades?

## Eve and Frank are not in inner join. It seems that they are not enrolled right now so they are not showing up with a course ID. With no grades means they are not enrolled. For more than one grade I think it shows they are taking more than one class.

### Task 2.3: Filtering Joins: Identifying Student Enrollment Status

This task focuses on using filtering joins to identify different
categories of students based on their enrollment and grade records.

1.  **Enrolled Students:** Use a `semi_join()` to identify which
    students from `students_demographics` are actually enrolled in and
    have a grade record in `student_grades`. This should return only
    columns from `students_demographics`.
2.  **Students Without Grades:** Use an `anti_join()` to identify which
    students from `students_demographics` are in the system but
    currently do *not* have any grade records in `student_grades` (e.g.,
    new students, or those who haven’t completed courses yet). This
    should return only columns from `students_demographics`.
3.  **Grades Without Students:** Use an `anti_join()` to identify any
    grade records in `student_grades` that do *not* correspond to an
    existing student in `students_demographics` (e.g., a data entry
    error or a record for a past student no longer in the demographic
    system). This should return only columns from `student_grades`.

``` r
enrolled_students <- students_demographics %>%
  inner_join(student_grades, by = "student_id")
enrolled_students
```

    ## # A tibble: 5 × 7
    ##   student_id student_name major   enrollment_year course_id semester grade_score
    ##   <chr>      <chr>        <chr>             <dbl> <chr>     <chr>          <dbl>
    ## 1 S001       Alice        CS                 2020 CS101     Fall 20…          92
    ## 2 S001       Alice        CS                 2020 CS102     Spring …          78
    ## 3 S002       Bob          Math               2021 MA201     Spring …          85
    ## 4 S003       Charlie      Physics            2020 PH301     Fall 20…          88
    ## 5 S004       David        CS                 2022 CS205     Spring …          90

``` r
notenrolled_students <- students_demographics %>%
  anti_join(student_grades, by = "student_id")
notenrolled_students
```

    ## # A tibble: 2 × 4
    ##   student_id student_name major   enrollment_year
    ##   <chr>      <chr>        <chr>             <dbl>
    ## 1 S005       Eve          Biology            2021
    ## 2 S007       Frank        History            2023

``` r
grades_withno_students <- student_grades %>%
  anti_join(students_demographics, by = "student_id")
grades_withno_students
```

    ## # A tibble: 1 × 4
    ##   student_id course_id semester  grade_score
    ##   <chr>      <chr>     <chr>           <dbl>
    ## 1 S006       BI101     Fall 2021          75

### Short Answer

Describe the distinct insights gained from each of the three filtering
joins in this task. How do these joins help in data validation and
understanding the completeness of your student records?

The first one shows which students are actually enrolled. The second
shows students without grades so waiting on grade. The last one shows a
grade but has no student attached to it.
