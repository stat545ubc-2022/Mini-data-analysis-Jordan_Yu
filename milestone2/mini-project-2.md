Mini Data Analysis Milestone 2
================

*To complete this milestone, you can edit [this `.rmd`
file](https://raw.githubusercontent.com/UBC-STAT/stat545.stat.ubc.ca/master/content/mini-project/mini-project-2.Rmd)
directly. Fill in the sections that are commented out with
`<!--- start your work here--->`. When you are done, make sure to knit
to an `.md` file by changing the output in the YAML header to
`github_document`, before submitting a tagged release on canvas.*

# Welcome to your second (and last) milestone in your mini data analysis project!

In Milestone 1, you explored your data, came up with research questions,
and obtained some results by making summary tables and graphs. This
time, we will first explore more in depth the concept of *tidy data.*
Then, you’ll be sharpening some of the results you obtained from your
previous milestone by:

-   Manipulating special data types in R: factors and/or dates and
    times.
-   Fitting a model object to your data, and extract a result.
-   Reading and writing data as separate files.

**NOTE**: The main purpose of the mini data analysis is to integrate
what you learn in class in an analysis. Although each milestone provides
a framework for you to conduct your analysis, it’s possible that you
might find the instructions too rigid for your data set. If this is the
case, you may deviate from the instructions – just make sure you’re
demonstrating a wide range of tools and techniques taught in this class.

# Instructions

**To complete this milestone**, edit [this very `.Rmd`
file](https://raw.githubusercontent.com/UBC-STAT/stat545.stat.ubc.ca/master/content/mini-project/mini-project-2.Rmd)
directly. Fill in the sections that are tagged with
`<!--- start your work here--->`.

**To submit this milestone**, make sure to knit this `.Rmd` file to an
`.md` file by changing the YAML output settings from
`output: html_document` to `output: github_document`. Commit and push
all of your work to your mini-analysis GitHub repository, and tag a
release on GitHub. Then, submit a link to your tagged release on canvas.

**Points**: This milestone is worth 55 points (compared to the 45 points
of the Milestone 1): 45 for your analysis, and 10 for your entire
mini-analysis GitHub repository. Details follow.

**Research Questions**: In Milestone 1, you chose two research questions
to focus on. Wherever realistic, your work in this milestone should
relate to these research questions whenever we ask for justification
behind your work. In the case that some tasks in this milestone don’t
align well with one of your research questions, feel free to discuss
your results in the context of a different research question.

# Learning Objectives

By the end of this milestone, you should:

-   Understand what *tidy* data is, and how to create it using `tidyr`.
-   Generate a reproducible and clear report using R Markdown.
-   Manipulating special data types in R: factors and/or dates and
    times.
-   Fitting a model object to your data, and extract a result.
-   Reading and writing data as separate files.

# Setup

Begin by loading your data and the tidyverse package below:

``` r
library(datateachr) # <- might contain the data you picked!
library(tidyverse)
```

# Task 1: Tidy your data (15 points)

In this task, we will do several exercises to reshape our data. The goal
here is to understand how to do this reshaping with the `tidyr` package.

A reminder of the definition of *tidy* data:

-   Each row is an **observation**
-   Each column is a **variable**
-   Each cell is a **value**

*Tidy’ing* data is sometimes necessary because it can simplify
computation. Other times it can be nice to organize data so that it can
be easier to understand when read manually.

### 2.1 (2.5 points)

Based on the definition above, can you identify if your data is tidy or
untidy? Go through all your columns, or if you have \>8 variables, just
pick 8, and explain whether the data is untidy or tidy.

<!--------------------------- Start your work below --------------------------->

``` r
cancer_sample
```

    ## # A tibble: 569 × 32
    ##          ID diagnosis radius_m…¹ textu…² perim…³ area_…⁴ smoot…⁵ compa…⁶ conca…⁷
    ##       <dbl> <chr>          <dbl>   <dbl>   <dbl>   <dbl>   <dbl>   <dbl>   <dbl>
    ##  1   842302 M               18.0    10.4   123.    1001   0.118   0.278   0.300 
    ##  2   842517 M               20.6    17.8   133.    1326   0.0847  0.0786  0.0869
    ##  3 84300903 M               19.7    21.2   130     1203   0.110   0.160   0.197 
    ##  4 84348301 M               11.4    20.4    77.6    386.  0.142   0.284   0.241 
    ##  5 84358402 M               20.3    14.3   135.    1297   0.100   0.133   0.198 
    ##  6   843786 M               12.4    15.7    82.6    477.  0.128   0.17    0.158 
    ##  7   844359 M               18.2    20.0   120.    1040   0.0946  0.109   0.113 
    ##  8 84458202 M               13.7    20.8    90.2    578.  0.119   0.164   0.0937
    ##  9   844981 M               13      21.8    87.5    520.  0.127   0.193   0.186 
    ## 10 84501001 M               12.5    24.0    84.0    476.  0.119   0.240   0.227 
    ## # … with 559 more rows, 23 more variables: concave_points_mean <dbl>,
    ## #   symmetry_mean <dbl>, fractal_dimension_mean <dbl>, radius_se <dbl>,
    ## #   texture_se <dbl>, perimeter_se <dbl>, area_se <dbl>, smoothness_se <dbl>,
    ## #   compactness_se <dbl>, concavity_se <dbl>, concave_points_se <dbl>,
    ## #   symmetry_se <dbl>, fractal_dimension_se <dbl>, radius_worst <dbl>,
    ## #   texture_worst <dbl>, perimeter_worst <dbl>, area_worst <dbl>,
    ## #   smoothness_worst <dbl>, compactness_worst <dbl>, concavity_worst <dbl>, …

The dataset “cancer_sample” is tidy since each column is a variable,
each cell is a value, and each row is an observation (patient). So we do
not need to tidy it, and here we will select 8 variables: *ID,
diagnosis, radius_mean, texture_mean, perimeter_mean, area_mean,
smoothness_mean, compactness_mean.* The selected columns will be stored
into a new dataframe called “new_cancer_sample”.

``` r
new_cancer_sample = cancer_sample%>%
  select(ID, 
         diagnosis, 
         radius_mean, 
         texture_mean, 
         perimeter_mean, 
         area_mean, 
         smoothness_mean, 
         compactness_mean)
new_cancer_sample
```

    ## # A tibble: 569 × 8
    ##          ID diagnosis radius_mean texture_mean perimet…¹ area_…² smoot…³ compa…⁴
    ##       <dbl> <chr>           <dbl>        <dbl>     <dbl>   <dbl>   <dbl>   <dbl>
    ##  1   842302 M                18.0         10.4     123.    1001   0.118   0.278 
    ##  2   842517 M                20.6         17.8     133.    1326   0.0847  0.0786
    ##  3 84300903 M                19.7         21.2     130     1203   0.110   0.160 
    ##  4 84348301 M                11.4         20.4      77.6    386.  0.142   0.284 
    ##  5 84358402 M                20.3         14.3     135.    1297   0.100   0.133 
    ##  6   843786 M                12.4         15.7      82.6    477.  0.128   0.17  
    ##  7   844359 M                18.2         20.0     120.    1040   0.0946  0.109 
    ##  8 84458202 M                13.7         20.8      90.2    578.  0.119   0.164 
    ##  9   844981 M                13           21.8      87.5    520.  0.127   0.193 
    ## 10 84501001 M                12.5         24.0      84.0    476.  0.119   0.240 
    ## # … with 559 more rows, and abbreviated variable names ¹​perimeter_mean,
    ## #   ²​area_mean, ³​smoothness_mean, ⁴​compactness_mean

<!----------------------------------------------------------------------------->

### 2.2 (5 points)

Now, if your data is tidy, untidy it! Then, tidy it back to it’s
original state.

If your data is untidy, then tidy it! Then, untidy it back to it’s
original state.

Be sure to explain your reasoning for this task. Show us the “before”
and “after”.

<!--------------------------- Start your work below --------------------------->

Since the data is tidy, we are going to untidy it now:

``` r
new_cancer_sample$ID = paste(new_cancer_sample$ID, 
                             new_cancer_sample$diagnosis, 
                             new_cancer_sample$radius_mean,
                             new_cancer_sample$texture_mean,
                             new_cancer_sample$perimeter_mean,
                             new_cancer_sample$area_mean,
                             new_cancer_sample$smoothness_mean,
                             new_cancer_sample$compactness_mean)
new_cancer_sample
```

    ## # A tibble: 569 × 8
    ##    ID                    diagn…¹ radiu…² textu…³ perim…⁴ area_…⁵ smoot…⁶ compa…⁷
    ##    <chr>                 <chr>     <dbl>   <dbl>   <dbl>   <dbl>   <dbl>   <dbl>
    ##  1 842302 M 17.99 10.38… M          18.0    10.4   123.    1001   0.118   0.278 
    ##  2 842517 M 20.57 17.77… M          20.6    17.8   133.    1326   0.0847  0.0786
    ##  3 84300903 M 19.69 21.… M          19.7    21.2   130     1203   0.110   0.160 
    ##  4 84348301 M 11.42 20.… M          11.4    20.4    77.6    386.  0.142   0.284 
    ##  5 84358402 M 20.29 14.… M          20.3    14.3   135.    1297   0.100   0.133 
    ##  6 843786 M 12.45 15.7 … M          12.4    15.7    82.6    477.  0.128   0.17  
    ##  7 844359 M 18.25 19.98… M          18.2    20.0   120.    1040   0.0946  0.109 
    ##  8 84458202 M 13.71 20.… M          13.7    20.8    90.2    578.  0.119   0.164 
    ##  9 844981 M 13 21.82 87… M          13      21.8    87.5    520.  0.127   0.193 
    ## 10 84501001 M 12.46 24.… M          12.5    24.0    84.0    476.  0.119   0.240 
    ## # … with 559 more rows, and abbreviated variable names ¹​diagnosis,
    ## #   ²​radius_mean, ³​texture_mean, ⁴​perimeter_mean, ⁵​area_mean, ⁶​smoothness_mean,
    ## #   ⁷​compactness_mean

Now we see that *ID* column contains the value of all other variables
and seperated by whitespace.

Next, we need to tidy it again:

``` r
new_cancer_sample = separate(new_cancer_sample, ID, c('ID', 
                                                      'diagnosis', 
                                                      'radius_mean', 
                                                      'texture_mean', 
                                                      'perimeter_mean', 
                                                      'area_mean', 
                                                      'smoothness_mean', 
                                                      'compactness_mean'), sep = " ")
new_cancer_sample
```

    ## # A tibble: 569 × 8
    ##    ID       diagnosis radius_mean texture_mean perimet…¹ area_…² smoot…³ compa…⁴
    ##    <chr>    <chr>     <chr>       <chr>        <chr>     <chr>   <chr>   <chr>  
    ##  1 842302   M         17.99       10.38        122.8     1001    0.1184  0.2776 
    ##  2 842517   M         20.57       17.77        132.9     1326    0.08474 0.07864
    ##  3 84300903 M         19.69       21.25        130       1203    0.1096  0.1599 
    ##  4 84348301 M         11.42       20.38        77.58     386.1   0.1425  0.2839 
    ##  5 84358402 M         20.29       14.34        135.1     1297    0.1003  0.1328 
    ##  6 843786   M         12.45       15.7         82.57     477.1   0.1278  0.17   
    ##  7 844359   M         18.25       19.98        119.6     1040    0.09463 0.109  
    ##  8 84458202 M         13.71       20.83        90.2      577.9   0.1189  0.1645 
    ##  9 844981   M         13          21.82        87.5      519.8   0.1273  0.1932 
    ## 10 84501001 M         12.46       24.04        83.97     475.9   0.1186  0.2396 
    ## # … with 559 more rows, and abbreviated variable names ¹​perimeter_mean,
    ## #   ²​area_mean, ³​smoothness_mean, ⁴​compactness_mean

Now we see that new_cancer_sample is back to the original form.

<!----------------------------------------------------------------------------->

### 2.3 (7.5 points)

Now, you should be more familiar with your data, and also have made
progress in answering your research questions. Based on your interest,
and your analyses, pick 2 of the 4 research questions to continue your
analysis in the next four tasks:

<!-------------------------- Start your work below ---------------------------->

Based on the feedback of mini-data-analysis 1, I rephrased my research
questions to the following:

1.  what is the relationship between mean texture and diagnosis
2.  what is the relationship between mean area and diagnosis

<!----------------------------------------------------------------------------->

Explain your decision for choosing the above two research questions.

<!--------------------------- Start your work below --------------------------->

From the plots generated in the last assignment, we can see that there’s
some relationship between these biomarkers and diagnosis, so it is
worthwhile to dig more into it.

<!----------------------------------------------------------------------------->

Now, try to choose a version of your data that you think will be
appropriate to answer these 2 questions. Use between 4 and 8 functions
that we’ve covered so far (i.e. by filtering, cleaning, tidy’ing,
dropping irrelevant columns, etc.).

<!--------------------------- Start your work below --------------------------->

Since we will only study *texture_mean* and *area_mean*, we will drop
all other irrelevant columns and only select what we need:

``` r
new_cancer_sample = new_cancer_sample%>%
  select(ID, diagnosis, texture_mean, area_mean)
new_cancer_sample
```

    ## # A tibble: 569 × 4
    ##    ID       diagnosis texture_mean area_mean
    ##    <chr>    <chr>     <chr>        <chr>    
    ##  1 842302   M         10.38        1001     
    ##  2 842517   M         17.77        1326     
    ##  3 84300903 M         21.25        1203     
    ##  4 84348301 M         20.38        386.1    
    ##  5 84358402 M         14.34        1297     
    ##  6 843786   M         15.7         477.1    
    ##  7 844359   M         19.98        1040     
    ##  8 84458202 M         20.83        577.9    
    ##  9 844981   M         21.82        519.8    
    ## 10 84501001 M         24.04        475.9    
    ## # … with 559 more rows

From the output above, we notice that the data type of column
*texture_mean* and *area_mean* is character. In order to make the
further computation easier, we here convert their data type to numeric.

``` r
new_cancer_sample$texture_mean = as.numeric(new_cancer_sample$texture_mean)
new_cancer_sample$area_mean = as.numeric(new_cancer_sample$area_mean)
new_cancer_sample
```

    ## # A tibble: 569 × 4
    ##    ID       diagnosis texture_mean area_mean
    ##    <chr>    <chr>            <dbl>     <dbl>
    ##  1 842302   M                 10.4     1001 
    ##  2 842517   M                 17.8     1326 
    ##  3 84300903 M                 21.2     1203 
    ##  4 84348301 M                 20.4      386.
    ##  5 84358402 M                 14.3     1297 
    ##  6 843786   M                 15.7      477.
    ##  7 844359   M                 20.0     1040 
    ##  8 84458202 M                 20.8      578.
    ##  9 844981   M                 21.8      520.
    ## 10 84501001 M                 24.0      476.
    ## # … with 559 more rows

Next, we will remove the outliers for texture_mean and area_mean:

``` r
new_cancer_sample = new_cancer_sample %>%
  filter( abs(texture_mean - median(texture_mean)) < 3*sd(texture_mean)) %>%
  filter( abs(area_mean - median(area_mean)) < 3*sd(area_mean))
new_cancer_sample
```

    ## # A tibble: 553 × 4
    ##    ID       diagnosis texture_mean area_mean
    ##    <chr>    <chr>            <dbl>     <dbl>
    ##  1 842302   M                 10.4     1001 
    ##  2 842517   M                 17.8     1326 
    ##  3 84300903 M                 21.2     1203 
    ##  4 84348301 M                 20.4      386.
    ##  5 84358402 M                 14.3     1297 
    ##  6 843786   M                 15.7      477.
    ##  7 844359   M                 20.0     1040 
    ##  8 84458202 M                 20.8      578.
    ##  9 844981   M                 21.8      520.
    ## 10 84501001 M                 24.0      476.
    ## # … with 543 more rows

Add new columns showing the classifying group for texture_mean and
area_mean to the dataframe:

``` r
new_cancer_sample = new_cancer_sample %>% 
  mutate(
     texture_mean_group = case_when(
        texture_mean - mean(texture_mean) < 0 ~ 'below avg',
        texture_mean - mean(texture_mean) == 0 ~ 'equal avg',
        texture_mean - mean(texture_mean) > 0 ~ 'above avg',
     )
)
```

``` r
new_cancer_sample = new_cancer_sample %>% 
  mutate(
     area_mean_group = case_when(
        area_mean - mean(area_mean) < 0 ~ 'below avg',
        area_mean - mean(area_mean) == 0 ~ 'equal avg',
        area_mean - mean(area_mean) > 0 ~ 'above avg',
     )
)
new_cancer_sample
```

    ## # A tibble: 553 × 6
    ##    ID       diagnosis texture_mean area_mean texture_mean_group area_mean_group
    ##    <chr>    <chr>            <dbl>     <dbl> <chr>              <chr>          
    ##  1 842302   M                 10.4     1001  below avg          above avg      
    ##  2 842517   M                 17.8     1326  below avg          above avg      
    ##  3 84300903 M                 21.2     1203  above avg          above avg      
    ##  4 84348301 M                 20.4      386. above avg          below avg      
    ##  5 84358402 M                 14.3     1297  below avg          above avg      
    ##  6 843786   M                 15.7      477. below avg          below avg      
    ##  7 844359   M                 20.0     1040  above avg          above avg      
    ##  8 84458202 M                 20.8      578. above avg          below avg      
    ##  9 844981   M                 21.8      520. above avg          below avg      
    ## 10 84501001 M                 24.0      476. above avg          below avg      
    ## # … with 543 more rows

We also create a new column to show the location of area_mean on centile
basis

``` r
new_cancer_sample = new_cancer_sample %>% 
  mutate(
     area_loc = case_when(
        abs(area_mean - mean(area_mean)) < sd(area_mean) ~ 'one-sd',
        abs(area_mean - mean(area_mean)) < 2*sd(area_mean) ~ 'two-sd',
        abs(area_mean - mean(area_mean)) < 3*sd(area_mean) ~ 'three-sd',
        abs(area_mean - mean(area_mean)) > 3*sd(area_mean) ~ 'other-sd',
     )
)
new_cancer_sample
```

    ## # A tibble: 553 × 7
    ##    ID       diagnosis texture_mean area_mean texture_mean_group area_m…¹ area_…²
    ##    <chr>    <chr>            <dbl>     <dbl> <chr>              <chr>    <chr>  
    ##  1 842302   M                 10.4     1001  below avg          above a… two-sd 
    ##  2 842517   M                 17.8     1326  below avg          above a… three-…
    ##  3 84300903 M                 21.2     1203  above avg          above a… two-sd 
    ##  4 84348301 M                 20.4      386. above avg          below a… one-sd 
    ##  5 84358402 M                 14.3     1297  below avg          above a… three-…
    ##  6 843786   M                 15.7      477. below avg          below a… one-sd 
    ##  7 844359   M                 20.0     1040  above avg          above a… two-sd 
    ##  8 84458202 M                 20.8      578. above avg          below a… one-sd 
    ##  9 844981   M                 21.8      520. above avg          below a… one-sd 
    ## 10 84501001 M                 24.0      476. above avg          below a… one-sd 
    ## # … with 543 more rows, and abbreviated variable names ¹​area_mean_group,
    ## #   ²​area_loc

<!----------------------------------------------------------------------------->

# Task 2: Special Data Types (10)

For this exercise, you’ll be choosing two of the three tasks below –
both tasks that you choose are worth 5 points each.

But first, tasks 1 and 2 below ask you to modify a plot you made in a
previous milestone. The plot you choose should involve plotting across
at least three groups (whether by facetting, or using an aesthetic like
colour). Place this plot below (you’re allowed to modify the plot if
you’d like). If you don’t have such a plot, you’ll need to make one.
Place the code for your plot below.

<!-------------------------- Start your work below ---------------------------->

Since we do not have such plot from the last milestone, here we make a
plot for different group of patients based on their texture_mean_group:

``` r
# we first change the type of texture_mean_group 
new_cancer_sample$area_loc = as.factor(new_cancer_sample$area_loc)
new_cancer_sample
```

    ## # A tibble: 553 × 7
    ##    ID       diagnosis texture_mean area_mean texture_mean_group area_m…¹ area_…²
    ##    <chr>    <chr>            <dbl>     <dbl> <chr>              <chr>    <fct>  
    ##  1 842302   M                 10.4     1001  below avg          above a… two-sd 
    ##  2 842517   M                 17.8     1326  below avg          above a… three-…
    ##  3 84300903 M                 21.2     1203  above avg          above a… two-sd 
    ##  4 84348301 M                 20.4      386. above avg          below a… one-sd 
    ##  5 84358402 M                 14.3     1297  below avg          above a… three-…
    ##  6 843786   M                 15.7      477. below avg          below a… one-sd 
    ##  7 844359   M                 20.0     1040  above avg          above a… two-sd 
    ##  8 84458202 M                 20.8      578. above avg          below a… one-sd 
    ##  9 844981   M                 21.8      520. above avg          below a… one-sd 
    ## 10 84501001 M                 24.0      476. above avg          below a… one-sd 
    ## # … with 543 more rows, and abbreviated variable names ¹​area_mean_group,
    ## #   ²​area_loc

``` r
ggplot(new_cancer_sample, aes(x=area_loc, ..count..)) + 
   geom_bar(aes(fill=diagnosis)) + labs(x = "area_loc")
```

![](mini-project-2_files/figure-gfm/unnamed-chunk-13-1.png)<!-- -->

<!----------------------------------------------------------------------------->

Now, choose two of the following tasks.

1.  Produce a new plot that reorders a factor in your original plot,
    using the `forcats` package (3 points). Then, in a sentence or two,
    briefly explain why you chose this ordering (1 point here for
    demonstrating understanding of the reordering, and 1 point for
    demonstrating some justification for the reordering, which could be
    subtle or speculative.)

2.  Produce a new plot that groups some factor levels together into an
    “other” category (or something similar), using the `forcats` package
    (3 points). Then, in a sentence or two, briefly explain why you
    chose this grouping (1 point here for demonstrating understanding of
    the grouping, and 1 point for demonstrating some justification for
    the grouping, which could be subtle or speculative.)

3.  If your data has some sort of time-based column like a date (but
    something more granular than just a year):

    1.  Make a new column that uses a function from the `lubridate` or
        `tsibble` package to modify your original time-based column. (3
        points)

        -   Note that you might first have to *make* a time-based column
            using a function like `ymd()`, but this doesn’t count.
        -   Examples of something you might do here: extract the day of
            the year from a date, or extract the weekday, or let 24
            hours elapse on your dates.

    2.  Then, in a sentence or two, explain how your new column might be
        useful in exploring a research question. (1 point for
        demonstrating understanding of the function you used, and 1
        point for your justification, which could be subtle or
        speculative).

        -   For example, you could say something like “Investigating the
            day of the week might be insightful because penguins don’t
            work on weekends, and so may respond differently”.

<!-------------------------- Start your work below ---------------------------->

**Task Number**: 1

Produce a new plot that reorders a factor in your original plot, using
the `forcats` package (3 points). Then, in a sentence or two, briefly
explain why you chose this ordering (1 point here for demonstrating
understanding of the reordering, and 1 point for demonstrating some
justification for the reordering, which could be subtle or speculative.)

``` r
ggplot(new_cancer_sample, aes(x=fct_reorder(area_loc, area_mean), ..count..)) +
    geom_bar(aes(fill=diagnosis)) + labs(x = "area_loc") 
```

![](mini-project-2_files/figure-gfm/unnamed-chunk-14-1.png)<!-- -->

Here, the reordering is based on ‘area_mean’ by using fct_reorder in
descending order instead of alphabetical order, which makes the plot
much clearer.

<!----------------------------------------------------------------------------->
<!-------------------------- Start your work below ---------------------------->

**Task Number**: 2

``` r
ggplot(new_cancer_sample, aes(x=fct_collapse(area_loc, other_sd = c("three-sd", "other-sd")), ..count..)) +
    geom_bar(aes(fill=diagnosis)) + labs(x = "area_loc")
```

![](mini-project-2_files/figure-gfm/unnamed-chunk-15-1.png)<!-- -->

Since the count of three-sd and other-sd are much less than the others,
we can merge them together to get the new “other_sd” group.

<!----------------------------------------------------------------------------->

# Task 3: Modelling

## 2.0 (no points)

Pick a research question, and pick a variable of interest (we’ll call it
“Y”) that’s relevant to the research question. Indicate these.

<!-------------------------- Start your work below ---------------------------->

**Research Question**: What is the relationship between area_mean and
texture_mean? Can we fit a model for them?

**Variable of interest**: area_mean, texture_mean

<!----------------------------------------------------------------------------->

## 2.1 (5 points)

Fit a model or run a hypothesis test that provides insight on this
variable with respect to the research question. Store the model object
as a variable, and print its output to screen. We’ll omit having to
justify your choice, because we don’t expect you to know about model
specifics in STAT 545.

-   **Note**: It’s OK if you don’t know how these models/tests work.
    Here are some examples of things you can do here, but the sky’s the
    limit.

    -   You could fit a model that makes predictions on Y using another
        variable, by using the `lm()` function.
    -   You could test whether the mean of Y equals 0 using `t.test()`,
        or maybe the mean across two groups are different using
        `t.test()`, or maybe the mean across multiple groups are
        different using `anova()` (you may have to pivot your data for
        the latter two).
    -   You could use `lm()` to test for significance of regression.

<!-------------------------- Start your work below ---------------------------->

``` r
model = lm(texture_mean ~ area_mean, data = new_cancer_sample)
model
```

    ## 
    ## Call:
    ## lm(formula = texture_mean ~ area_mean, data = new_cancer_sample)
    ## 
    ## Coefficients:
    ## (Intercept)    area_mean  
    ##   16.341997     0.004417

<!----------------------------------------------------------------------------->

## 2.2 (5 points)

Produce something relevant from your fitted model: either predictions on
Y, or a single value like a regression coefficient or a p-value.

-   Be sure to indicate in writing what you chose to produce.
-   Your code should either output a tibble (in which case you should
    indicate the column that contains the thing you’re looking for), or
    the thing you’re looking for itself.
-   Obtain your results using the `broom` package if possible. If your
    model is not compatible with the broom function you’re needing, then
    you can obtain your results by some other means, but first indicate
    which broom function is not compatible.

<!-------------------------- Start your work below ---------------------------->

``` r
library(broom)
model_summary = tidy(model)
model_summary
```

    ## # A tibble: 2 × 5
    ##   term        estimate std.error statistic   p.value
    ##   <chr>          <dbl>     <dbl>     <dbl>     <dbl>
    ## 1 (Intercept) 16.3      0.385        42.4  1.38e-175
    ## 2 area_mean    0.00442  0.000556      7.94 1.16e- 14

What is the standard error of the intercept for this model?

``` r
intercept_sd = model_summary%>%
  filter(term == '(Intercept)')%>%
  select(std.error)
intercept_sd
```

    ## # A tibble: 1 × 1
    ##   std.error
    ##       <dbl>
    ## 1     0.385

The standard error of intercept in this model is shown above.

<!----------------------------------------------------------------------------->

# Task 4: Reading and writing data

Get set up for this exercise by making a folder called `output` in the
top level of your project folder / repository. You’ll be saving things
there.

## 3.1 (5 points)

Take a summary table that you made from Milestone 1 (Task 4.2), and
write it as a csv file in your `output` folder. Use the `here::here()`
function.

-   **Robustness criteria**: You should be able to move your Mini
    Project repository / project folder to some other location on your
    computer, or move this very Rmd file to another location within your
    project repository / folder, and your code should still work.
-   **Reproducibility criteria**: You should be able to delete the csv
    file, and remake it simply by knitting this Rmd file.

<!-------------------------- Start your work below ---------------------------->

``` r
library(here)
```

    ## here() starts at /Users/jordan/Desktop/2022W1/STAT545/Mini-data-analysis-Jordan_Yu

``` r
here()
```

    ## [1] "/Users/jordan/Desktop/2022W1/STAT545/Mini-data-analysis-Jordan_Yu"

``` r
write_csv(model_summary, here::here("output", "mini_project_result.csv"))
```

<!----------------------------------------------------------------------------->

## 3.2 (5 points)

Write your model object from Task 3 to an R binary file (an RDS), and
load it again. Be sure to save the binary file in your `output` folder.
Use the functions `saveRDS()` and `readRDS()`.

-   The same robustness and reproducibility criteria as in 3.1 apply
    here.

<!-------------------------- Start your work below ---------------------------->

``` r
saveRDS(model_summary, here::here("output", "mini_project_model.rds"))
read_model = readRDS(here::here("output", "mini_project_model.rds"))
read_model
```

    ## # A tibble: 2 × 5
    ##   term        estimate std.error statistic   p.value
    ##   <chr>          <dbl>     <dbl>     <dbl>     <dbl>
    ## 1 (Intercept) 16.3      0.385        42.4  1.38e-175
    ## 2 area_mean    0.00442  0.000556      7.94 1.16e- 14

<!----------------------------------------------------------------------------->

# Tidy Repository

Now that this is your last milestone, your entire project repository
should be organized. Here are the criteria we’re looking for.

## Main README (3 points)

There should be a file named `README.md` at the top level of your
repository. Its contents should automatically appear when you visit the
repository on GitHub.

Minimum contents of the README file:

-   In a sentence or two, explains what this repository is, so that
    future-you or someone else stumbling on your repository can be
    oriented to the repository.
-   In a sentence or two (or more??), briefly explains how to engage
    with the repository. You can assume the person reading knows the
    material from STAT 545A. Basically, if a visitor to your repository
    wants to explore your project, what should they know?

Once you get in the habit of making README files, and seeing more README
files in other projects, you’ll wonder how you ever got by without them!
They are tremendously helpful.

## File and Folder structure (3 points)

You should have at least three folders in the top level of your
repository: one for each milestone, and one output folder. If there are
any other folders, these are explained in the main README.

Each milestone document is contained in its respective folder, and
nowhere else.

Every level-1 folder (that is, the ones stored in the top level, like
“Milestone1” and “output”) has a `README` file, explaining in a sentence
or two what is in the folder, in plain language (it’s enough to say
something like “This folder contains the source for Milestone 1”).

## Output (2 points)

All output is recent and relevant:

-   All Rmd files have been `knit`ted to their output, and all data
    files saved from Task 4 above appear in the `output` folder.
-   All of these output files are up-to-date – that is, they haven’t
    fallen behind after the source (Rmd) files have been updated.
-   There should be no relic output files. For example, if you were
    knitting an Rmd to html, but then changed the output to be only a
    markdown file, then the html file is a relic and should be deleted.

Our recommendation: delete all output files, and re-knit each
milestone’s Rmd file, so that everything is up to date and relevant.

PS: there’s a way where you can run all project code using a single
command, instead of clicking “knit” three times. More on this in STAT
545B!

## Error-free code (1 point)

This Milestone 1 document knits error-free, and the Milestone 2 document
knits error-free.

Plots failing to show up on Github in the .md counts as an error here.
So does the entire .md failing to show up on Github in the .md (“Sorry
about that, but we can’t show files that are this big right now”).

## Tagged release (1 point)

You’ve tagged a release for Milestone 1, and you’ve tagged a release for
Milestone 2.

### Attribution

Thanks to Victor Yuan for mostly putting this together.
