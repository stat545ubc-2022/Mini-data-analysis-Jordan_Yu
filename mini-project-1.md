---
title: "Mini Data-Analysis Deliverable 1"
output: github_document
---

# Welcome to your (maybe) first-ever data analysis project!

And hopefully the first of many. Let's get started:

1.  Install the [`datateachr`](https://github.com/UBC-MDS/datateachr) package by typing the following into your **R terminal**:

<!-- -->

    install.packages("devtools")
    devtools::install_github("UBC-MDS/datateachr")

1.  Load the packages below.

```{r}
library(datateachr)
library(tidyverse)
```

1.  Make a repository in the <https://github.com/stat545ubc-2022> Organization. You will be working with this repository for the entire data analysis project. You can either make it public, or make it private and add the TA's and Lucy as collaborators. A link to help you create a private repository is available on the #collaborative-project Slack channel.

# Instructions

## For Both Milestones

-   Each milestone is worth 45 points. The number of points allocated to each task will be annotated within each deliverable. Tasks that are more challenging will often be allocated more points.

-   10 points will be allocated to the reproducibility, cleanliness, and coherence of the overall analysis. While the two milestones will be submitted as independent deliverables, the analysis itself is a continuum - think of it as two chapters to a story. Each chapter, or in this case, portion of your analysis, should be easily followed through by someone unfamiliar with the content. [Here](https://swcarpentry.github.io/r-novice-inflammation/06-best-practices-R/) is a good resource for what constitutes "good code". Learning good coding practices early in your career will save you hassle later on!

## For Milestone 1

**To complete this milestone**, edit [this very `.Rmd` file](https://raw.githubusercontent.com/UBC-STAT/stat545.stat.ubc.ca/master/content/mini-project/mini-project-1.Rmd) directly. Fill in the sections that are tagged with `<!--- start your work below --->`.

**To submit this milestone**, make sure to knit this `.Rmd` file to an `.md` file by changing the YAML output settings from `output: html_document` to `output: github_document`. Commit and push all of your work to the mini-analysis GitHub repository you made earlier, and tag a release on GitHub. Then, submit a link to your tagged release on canvas.

**Points**: This milestone is worth 45 points: 43 for your analysis, 1 point for having your Milestone 1 document knit error-free, and 1 point for tagging your release on Github.

# Learning Objectives

By the end of this milestone, you should:

-   Become familiar with your dataset of choosing
-   Select 4 questions that you would like to answer with your data
-   Generate a reproducible and clear report using R Markdown
-   Become familiar with manipulating and summarizing your data in tibbles using `dplyr`, with a research question in mind.

# Task 1: Choose your favorite dataset (10 points)

The `datateachr` package by Hayley Boyce and Jordan Bourak currently composed of 7 semi-tidy datasets for educational purposes. Here is a brief description of each dataset:

-   *apt_buildings*: Acquired courtesy of The City of Toronto's Open Data Portal. It currently has 3455 rows and 37 columns.

-   *building_permits*: Acquired courtesy of The City of Vancouver's Open Data Portal. It currently has 20680 rows and 14 columns.

-   *cancer_sample*: Acquired courtesy of UCI Machine Learning Repository. It currently has 569 rows and 32 columns.

-   *flow_sample*: Acquired courtesy of The Government of Canada's Historical Hydrometric Database. It currently has 218 rows and 7 columns.

-   *parking_meters*: Acquired courtesy of The City of Vancouver's Open Data Portal. It currently has 10032 rows and 22 columns.

-   *steam_games*: Acquired courtesy of Kaggle. It currently has 40833 rows and 21 columns.

-   *vancouver_trees*: Acquired courtesy of The City of Vancouver's Open Data Portal. It currently has 146611 rows and 20 columns.

**Things to keep in mind**

-   We hope that this project will serve as practice for carrying our your own *independent* data analysis. Remember to comment your code, be explicit about what you are doing, and write notes in this markdown document when you feel that context is required. As you advance in the project, prompts and hints to do this will be diminished - it'll be up to you!

-   Before choosing a dataset, you should always keep in mind **your goal**, or in other ways, *what you wish to achieve with this data*. This mini data-analysis project focuses on *data wrangling*, *tidying*, and *visualization*. In short, it's a way for you to get your feet wet with exploring data on your own.

And that is exactly the first thing that you will do!

1.1 Out of the 7 datasets available in the `datateachr` package, choose **4** that appeal to you based on their description. Write your choices below:

**Note**: We encourage you to use the ones in the `datateachr` package, but if you have a dataset that you'd really like to use, you can include it here. But, please check with a member of the teaching team to see whether the dataset is of appropriate complexity. Also, include a **brief** description of the dataset here to help the teaching team understand your data.

<!-------------------------- Start your work below ---------------------------->

1: *apt_buildings*
2: *cancer_sample*
3: *flow_sample*
4: *parking_meters*

<!----------------------------------------------------------------------------->

1.2 One way to narrowing down your selection is to *explore* the datasets. Use your knowledge of dplyr to find out at least *3* attributes about each of these datasets (an attribute is something such as number of rows, variables, class type...). The goal here is to have an idea of *what the data looks like*.

*Hint:* This is one of those times when you should think about the cleanliness of your analysis. I added a single code chunk for you below, but do you want to use more than one? Would you like to write more comments outside of the code chunk?

<!-------------------------- Start your work below ---------------------------->

```{r}
### EXPLORE HERE ###
# check the number of rows and columns for each dataset
dim(apt_buildings)
dim(cancer_sample)
dim(flow_sample)
dim(parking_meters)
```

```{r}
### EXPLORE HERE ###
# check the class for each dataset
class(apt_buildings)
class(cancer_sample)
class(flow_sample)
class(parking_meters)
```

```{r}
### EXPLORE HERE ###
# check the overview for each dataset

glimpse(apt_buildings)
#----------------------------------------------------------------------------------------------

glimpse(cancer_sample)
#----------------------------------------------------------------------------------------------

glimpse(flow_sample)
#----------------------------------------------------------------------------------------------

glimpse(parking_meters)
```

<!----------------------------------------------------------------------------->

1.3 Now that you've explored the 4 datasets that you were initially most interested in, let's narrow it down to 2. What lead you to choose these 2? Briefly explain your choices below, and feel free to include any code in your explanation.

<!-------------------------- Start your work below ---------------------------->

I would like to choose "cancer_sample" and "apt_buildings" for the following reason:

-   The dataset of "cancer_sample" is closely related to my research (bioinformatics);

-   The dataset of "apt_buildings" could provide me with a number of information, and I personally think it would be very helpful for me in the future when buying my first house.

<!----------------------------------------------------------------------------->

1.4 Time for the final decision! Going back to the beginning, it's important to have an *end goal* in mind. For example, if I had chosen the `titanic` dataset for my project, I might've wanted to explore the relationship between survival and other variables. Try to think of 1 research question that you would want to answer with each dataset. Note them down below, and make your final choice based on what seems more interesting to you!

<!-------------------------- Start your work below ---------------------------->

-   *cancer_sample*:explore the relationship between different diagnosis and biomarkers

-   *apt_buildings*: explore the relationship between and their number of units

```{r}
View(cancer_sample)
View(apt_buildings)
```

Due to complicated types of data in *apt_buildings*, I would like to choose *cancer_sample* as my final choice.

<!----------------------------------------------------------------------------->

# Important note

Read Tasks 2 and 3 *fully* before starting to complete either of them. Probably also a good point to grab a coffee to get ready for the fun part!

This project is semi-guided, but meant to be *independent*. For this reason, you will complete tasks 2 and 3 below (under the **START HERE** mark) as if you were writing your own exploratory data analysis report, and this guidance never existed! Feel free to add a brief introduction section to your project, format the document with markdown syntax as you deem appropriate, and structure the analysis as you deem appropriate. Remember, marks will be awarded for completion of the 4 tasks, but 10 points of the whole project are allocated to a reproducible and clean analysis. If you feel lost, you can find a sample data analysis [here](https://www.kaggle.com/headsortails/tidy-titarnic) to have a better idea. However, bear in mind that it is **just an example** and you will not be required to have that level of complexity in your project.

# Task 2: Exploring your dataset (15 points)

If we rewind and go back to the learning objectives, you'll see that by the end of this deliverable, you should have formulated *4* research questions about your data that you may want to answer during your project. However, it may be handy to do some more exploration on your dataset of choice before creating these questions - by looking at the data, you may get more ideas. **Before you start this task, read all instructions carefully until you reach START HERE under Task 3**.

2.1 Complete *4 out of the following 8 exercises* to dive deeper into your data. All datasets are different and therefore, not all of these tasks may make sense for your data - which is why you should only answer *4*. Use *dplyr* and *ggplot*.

1.  [**Plot the distribution of a numeric variable.**]{.underline}
2.  [**Create a new variable based on other variables in your data (only if it makes sense)**]{.underline}
3.  Investigate how many missing values there are per variable. Can you find a way to plot this?
4.  [**Explore the relationship between 2 variables in a plot.**]{.underline}
5.  Filter observations in your data according to your own criteria. Think of what you'd like to explore - again, if this was the `titanic` dataset, I may want to narrow my search down to passengers born in a particular year...
6.  Use a boxplot to look at the frequency of different observations within a single variable. You can do this for more than one variable if you wish!
7.  [**Make a new tibble with a subset of your data, with variables and observations that you are interested in exploring.**]{.underline}
8.  Use a density plot to explore any of your variables (that are suitable for this type of plot).

2.2 For each of the 4 exercises that you complete, provide a *brief explanation* of why you chose that exercise in relation to your data (in other words, why does it make sense to do that?), and sufficient comments for a reader to understand your reasoning and code.

<!-------------------------- Start your work below ---------------------------->

[**2.2.1**]{.underline}[**Plot the distribution of a numeric variable**]{.underline}

We plot the radius_mean of *cancer_sample*:

```{r}
library(ggplot2)
cancer_sample %>%
  ggplot(aes(x = radius_mean)) +
  geom_histogram(colour = "red")
```

**2.2.2 Create a new variable based on other variables in your data (only if it makes sense)**

We would like to compute the normalized value for radius_mean, so we create a new variable called "norm_radius_mean" which is equal to *radius_mean - mean(radius_mean)*.

```{r}
cancer_sample <- mutate(cancer_sample, norm_radius_mean = radius_mean - mean(radius_mean))
```

**2.2.4 Explore the relationship between 2 variables in a plot.**

We would like to see the relationship between diagnosis and norm_radius_mean for each subject, so we create a plot as following:

```{r}
cancer_sample %>%
  ggplot(aes(x=diagnosis, y=norm_radius_mean)) +
  geom_jitter(alpha = 0.3, size = 0.6, width = 0.1, color = "navy")+
  xlab("diagnosis")+
  ylab("norm_radius_mean")
```

From the plot above we can see that for subjects with diagnosis "B", they usually have lower norm_radius_mean, and most of them are under 0. While for subjects with diagnosis "M", they usually have higher norm_radius_mean and most of them are greater than 0.

**2.2.7 Make a new tibble with a subset of your data, with variables and observations that you are interested in exploring.**

We would like to create a new tibble with all mean-variables and their ID and diagnosis in *cancer_sample* (column 1 to 12)

```{r}
cancer_sample_mean_vars = cancer_sample %>%
  select(ID, diagnosis, radius_mean, texture_mean, perimeter_mean, area_mean, smoothness_mean, compactness_mean, compactness_mean, concavity_mean, concave_points_mean, symmetry_mean, fractal_dimension_mean)
# check the type 
is_tibble(cancer_sample_mean_vars)
```

<!----------------------------------------------------------------------------->

# Task 3: Write your research questions (5 points)

So far, you have chosen a dataset and gotten familiar with it through exploring the data. Now it's time to figure out 4 research questions that you would like to answer with your data! Write the 4 questions and any additional comments at the end of this deliverable. These questions are not necessarily set in stone - TAs will review them and give you feedback; therefore, you may choose to pursue them as they are for the rest of the project, or make modifications!

<!--- *****START HERE***** --->

1.  **classify *texture_mean* and create a new variable for it, then explore the relationship between *texture_mean* and *diagnosis***

2.  **classify *area_mean* and create a new variable for it, then explore the relationship between *area_mean* and *diagnosis***

3.  **classify *smoothness_mean* and create a new variable for it, then explore the relationship between *smoothness_mean* and *diagnosis***

4.  **classify *concave_points_mean* and create a new variable for it, then explore the relationship between *concave_points_mean* and *diagnosis***

# Task 4: Process and summarize your data (13 points)

From Task 2, you should have an idea of the basic structure of your dataset (e.g. number of rows and columns, class types, etc.). Here, we will start investigating your data more in-depth using various data manipulation functions.

### 1.1 (10 points)

Now, for each of your four research questions, choose one task from options 1-4 (summarizing), and one other task from 4-8 (graphing). You should have 2 tasks done for each research question (8 total). Make sure it makes sense to do them! (e.g. don't use a numerical variables for a task that needs a categorical variable.). Comment on why each task helps (or doesn't!) answer the corresponding research question.

Ensure that the output of each operation is printed!

**Summarizing:**

1.  Compute the *range*, *mean*, and *two other summary statistics* of **one numerical variable** across the groups of **one categorical variable** from your data.
2.  Compute the number of observations for at least one of your categorical variables. Do not use the function `table()`!
3.  Create a categorical variable with 3 or more groups from an existing numerical variable. You can use this new variable in the other tasks! *An example: age in years into "child, teen, adult, senior".*
4.  Based on two categorical variables, calculate two summary statistics of your choosing.

**Graphing:**

1.  Create a graph out of summarized variables that has at least two geom layers.
2.  Create a graph of your choosing, make one of the axes logarithmic, and format the axes labels so that they are "pretty" or easier to read.
3.  Make a graph where it makes sense to customize the alpha transparency.
4.  Create 3 histograms out of summarized variables, with each histogram having different sized bins. Pick the "best" one and explain why it is the best.

Make sure it's clear what research question you are doing each operation for!

<!------------------------- Start your work below ----------------------------->

1.  **classify *texture_mean* and create a new variable for it, then explore the relationship between *texture_mean* and *diagnosis***

-   Create a categorical variable with 3 or more groups from an existing numerical variable. You can use this new variable in the other tasks! *An example: age in years into "child, teen, adult, senior".*

```{r}
cancer_sample_mean_vars = cancer_sample_mean_vars %>% 
  mutate(
     texture_mean_group = case_when(
        texture_mean - mean(texture_mean) < 0 ~ 'below avg',
        texture_mean - mean(texture_mean) == 0 ~ 'equal avg',
        texture_mean - mean(texture_mean) > 0 ~ 'above avg',
     )
)
# norm_radius_mean = texture_mean - mean(texture_mean)
```

Here we create a new variable "texture_mean_group" with 3 different groups - 'below avg', 'equal avg' and 'above avg'.

-   Create a graph out of summarized variables that has at least two geom layers.

    ```{r}
    cancer_sample_mean_vars %>%
      ggplot(aes(x = diagnosis, y = texture_mean_group))+
      geom_jitter(alpha = 0.3, size = 0.6, width = 0.1, color = "navy")
    ```

From the plot above, we cannot see obvious relationship between ***diagnosis*** and ***texture_mean_groups***. So, ***texture_mean_groups*** may not be a proper variable for classifying subjects.

1.  **classify *area_mean* and create a new variable for it, then explore the relationship between *area_mean* and *diagnosis***

-   Create a categorical variable with 3 or more groups from an existing numerical variable. You can use this new variable in the other tasks! *An example: age in years into "child, teen, adult, senior".*

```{r}
cancer_sample_mean_vars = cancer_sample_mean_vars %>% 
  mutate(
     area_mean_group = case_when(
        area_mean - mean(area_mean) < 0 ~ 'below avg',
        area_mean - mean(area_mean) == 0 ~ 'equal avg',
        area_mean - mean(area_mean) > 0 ~ 'above avg',
     )
)
# norm_radius_mean = texture_mean - mean(texture_mean)
```

Here we create a new variable "area_mean_group" with 3 different groups - 'below avg', 'equal avg' and 'above avg'.

-   Create a graph out of summarized variables that has at least two geom layers.

    ```{r}
    cancer_sample_mean_vars %>%
      ggplot(aes(x = diagnosis, y = area_mean_group))+
      geom_jitter(alpha = 0.3, size = 0.6, width = 0.1, color = "navy")
    ```

From the plot above, we can see that for subjects with diagnosis "B", most of them have 'below avg' area_mean_group, while for subjects with diagnosis "M", most of them have 'above avg' area_mean_group. So, area_mean_group could potentially be a variable for classifying subjects.

1.  **classify *smoothness_mean* and create a new variable for it, then explore the relationship between *smoothness_mean* and *diagnosis***

-   Create a categorical variable with 3 or more groups from an existing numerical variable. You can use this new variable in the other tasks! *An example: age in years into "child, teen, adult, senior".*

```{r}
cancer_sample_mean_vars = cancer_sample_mean_vars %>% 
  mutate(
     smoothness_mean_group = case_when(
        smoothness_mean - mean(smoothness_mean) < 0 ~ 'below avg',
        smoothness_mean - mean(smoothness_mean) == 0 ~ 'equal avg',
        smoothness_mean - mean(smoothness_mean) > 0 ~ 'above avg',
     )
)
# norm_radius_mean = texture_mean - mean(texture_mean)
```

Here we create a new variable "smoothness_mean_group" with 3 different groups - 'below avg', 'equal avg' and 'above avg'.

-   Create a graph out of summarized variables that has at least two geom layers.

    ```{r}
    cancer_sample_mean_vars %>%
      ggplot(aes(x = diagnosis, y = smoothness_mean_group))+
      geom_jitter(alpha = 0.3, size = 0.6, width = 0.1, color = "navy")
    ```

From the plot above, we cannot see an obvious relationship between ***diagnosis*** and ***smoothness_mean.*** So, ***smoothness_mean*** may not be a proper variable for classifying subjects.

1.  **classify *concave_points_mean* and create a new variable for it, then explore the relationship between *concave_points_mean* and *diagnosis***

-   Create a categorical variable with 3 or more groups from an existing numerical variable. You can use this new variable in the other tasks! *An example: age in years into "child, teen, adult, senior".*

```{r}
cancer_sample_mean_vars = cancer_sample_mean_vars %>% 
  mutate(
     concave_points_mean_group = case_when(
        concave_points_mean - mean(concave_points_mean) < 0 ~ 'below avg',
        concave_points_mean - mean(concave_points_mean) == 0 ~ 'equal avg',
        concave_points_mean - mean(concave_points_mean) > 0 ~ 'above avg',
     )
)
# norm_radius_mean = texture_mean - mean(texture_mean)
```

Here we create a new variable "***concave_points_mean***" with 3 different groups - 'below avg', 'equal avg' and 'above avg'.

-   Create a graph out of summarized variables that has at least two geom layers.

    ```{r}
    cancer_sample_mean_vars %>%
      ggplot(aes(x = diagnosis, y = concave_points_mean_group))+
      geom_jitter(alpha = 0.3, size = 0.6, width = 0.1, color = "navy")
    ```

From the plot above, we can see that for subjects with diagnosis "B", most of them have 'below avg' ***concave_points_mean_group***, while for subjects with diagnosis "M", most of them have 'above avg' ***concave_points_mean_group***. So, ***concave_points_mean_group*** could potentially be a variable for classifying subjects.

<!----------------------------------------------------------------------------->

### 1.2 (3 points)

Based on the operations that you've completed, how much closer are you to answering your research questions? Think about what aspects of your research questions remain unclear. Can your research questions be refined, now that you've investigated your data a bit more? Which research questions are yielding interesting results?

<!-------------------------- Start your work below ---------------------------->

-   Now we have found that some biomarkers (variables) could be used for classifying subjects, while others may not. However, we only selected 4 biomarkers out of interest, and we need to finish exploring the rest biomarkers to see whether any of them would also be good choices for classifying subjects.

<!----------------------------------------------------------------------------->

### Attribution

Thanks to Icíar Fernández Boyano for mostly putting this together, and Vincenzo Coia for launching.
