---
title: "Team Troubleshooting Deliverable 2"
output: github_document
---



There are **11 code chunks with errors** in this Rmd. Your objective is to fix all of the errors in this worksheet. For the purpose of grading, each erroneous code chunk is equally weighted.

Note that errors are not all syntactic (i.e., broken code)! Some are logical errors as well (i.e. code that does not do what it was intended to do).

## Exercise 1: Exploring with `select()` and `filter()`

[MovieLens](https://dl.acm.org/doi/10.1145/2827872) are a series of datasets widely used in education, that describe movie ratings from the MovieLens [website](https://movielens.org/). There are several MovieLens datasets, collected by the [GroupLens Research Project](https://grouplens.org/datasets/movielens/) at the University of Minnesota. Here, we load the MovieLens 100K dataset from Rafael Irizarry and Amy Gill's R package, [dslabs](https://cran.r-project.org/web/packages/dslabs/dslabs.pdf), which contains datasets useful for data analysis practice, homework, and projects in data science courses and workshops. We'll also load other required packages.


``` r
### ERROR HERE ###
# Assuming dslabs, tidyverse, stringr and gapminder have been installed previously
library(dslabs) # Corrected function to load package
```

```
## Error in library(dslabs): there is no package called 'dslabs'
```

``` r
library(tidyverse) # Corrected function to load package
```

```
## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
## ✔ dplyr     1.1.4     ✔ readr     2.1.5
## ✔ forcats   1.0.0     ✔ stringr   1.5.1
## ✔ ggplot2   3.5.1     ✔ tibble    3.2.1
## ✔ lubridate 1.9.4     ✔ tidyr     1.3.1
## ✔ purrr     1.0.4     
## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
## ✖ dplyr::filter() masks stats::filter()
## ✖ dplyr::lag()    masks stats::lag()
## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors
```

``` r
library(stringr)  # Corrected function to load package
# install.packages("devtools") # Do not run this if you already have this package installed! 
devtools::install_github("JoeyBernhardt/singer")
```

```
## Using GitHub PAT from the git credential store.
## Downloading GitHub repo JoeyBernhardt/singer@HEAD
```

```
## rlang        (1.1.5   -> 1.1.6 ) [CRAN]
## cli          (3.6.4   -> 3.6.5 ) [CRAN]
## utf8         (1.2.4   -> 1.2.6 ) [CRAN]
## stringi      (1.8.4   -> 1.8.7 ) [CRAN]
## pillar       (1.10.1  -> 1.11.1) [CRAN]
## generics     (0.1.3   -> 0.1.4 ) [CRAN]
## tibble       (3.2.1   -> 3.3.0 ) [CRAN]
## stringr      (1.5.1   -> 1.5.2 ) [CRAN]
## purrr        (1.0.4   -> 1.1.0 ) [CRAN]
## magrittr     (2.0.3   -> 2.0.4 ) [CRAN]
## openssl      (2.3.2   -> 2.3.3 ) [CRAN]
## mime         (0.12    -> 0.13  ) [CRAN]
## jsonlite     (1.9.0   -> 2.0.0 ) [CRAN]
## curl         (6.2.1   -> 7.0.0 ) [CRAN]
## xml2         (1.3.6   -> 1.4.0 ) [CRAN]
## ps           (1.9.0   -> 1.9.1 ) [CRAN]
## sass         (0.4.9   -> 0.4.10) [CRAN]
## tinytex      (0.55    -> 0.57  ) [CRAN]
## xfun         (0.51    -> 0.53  ) [CRAN]
## evaluate     (1.0.3   -> 1.0.5 ) [CRAN]
## knitr        (1.49    -> 1.50  ) [CRAN]
## fs           (1.6.5   -> 1.6.6 ) [CRAN]
## bit          (4.5.0.1 -> 4.6.0 ) [CRAN]
## vroom        (1.6.5   -> 1.6.6 ) [CRAN]
## textshaping  (1.0.0   -> 1.0.3 ) [CRAN]
## systemfonts  (1.1.0   -> 1.2.3 ) [CRAN]
## broom        (1.0.7   -> 1.0.10) [CRAN]
## forcats      (1.0.0   -> 1.0.1 ) [CRAN]
## googledrive  (2.1.1   -> 2.1.2 ) [CRAN]
## gargle       (1.5.2   -> 1.6.0 ) [CRAN]
## scales       (1.3.0   -> 1.4.0 ) [CRAN]
## S7           (NA      -> 0.2.0 ) [CRAN]
## data.table   (1.17.0  -> 1.17.8) [CRAN]
## rvest        (1.0.4   -> 1.0.5 ) [CRAN]
## readxl       (1.4.3   -> 1.4.5 ) [CRAN]
## ragg         (1.3.3   -> 1.5.0 ) [CRAN]
## haven        (2.5.4   -> 2.5.5 ) [CRAN]
## googleshe... (1.1.1   -> 1.1.2 ) [CRAN]
## ggplot2      (3.5.1   -> 4.0.0 ) [CRAN]
## dtplyr       (1.3.1   -> 1.3.2 ) [CRAN]
## dbplyr       (2.5.0   -> 2.5.1 ) [CRAN]
```

```
## Installing 41 packages: rlang, cli, utf8, stringi, pillar, generics, tibble, stringr, purrr, magrittr, openssl, mime, jsonlite, curl, xml2, ps, sass, tinytex, xfun, evaluate, knitr, fs, bit, vroom, textshaping, systemfonts, broom, forcats, googledrive, gargle, scales, S7, data.table, rvest, readxl, ragg, haven, googlesheets4, ggplot2, dtplyr, dbplyr
```

```
## 
## The downloaded binary packages are in
## 	/var/folders/16/wmm7yfzx6mj9vq37t6ptmzhm0000gn/T//Rtmp1VDI8h/downloaded_packages
## ── R CMD build ─────────────────────────────────────────────────────────────────
## * checking for file ‘/private/var/folders/16/wmm7yfzx6mj9vq37t6ptmzhm0000gn/T/Rtmp1VDI8h/remotes15c884ad3cca2/JoeyBernhardt-singer-2b4fe9c/DESCRIPTION’ ... OK
## * preparing ‘singer’:
## * checking DESCRIPTION meta-information ... OK
## * checking for LF line-endings in source and make files and shell scripts
## * checking for empty or unneeded directories
## * building ‘singer_0.0.0.9000.tar.gz’
```

``` r
library(gapminder) # Corrected function to load package
```

Let's have a look at the dataset! My goal is to:

-   Find out the "class" of the dataset.
-   If it isn't a tibble already, coerce it into a tibble and store it in the variable "movieLens".
-   Have a quick look at the tibble, using a *dplyr function*.


``` r
### ERROR HERE ###
class(dslabs::movielens)
```

```
## Error in loadNamespace(x): there is no package called 'dslabs'
```

``` r
if (is_tibble(dslabs::movielens) == FALSE) { # Conditional coerce if movielens is not a tibble
  movieLens <- as_tibble(dslabs::movielens)
}
```

```
## Error in loadNamespace(x): there is no package called 'dslabs'
```

``` r
dim(movieLens)
```

```
## Error: object 'movieLens' not found
```

``` r
class(movieLens)
```

```
## Error: object 'movieLens' not found
```

``` r
glimpse(movieLens) # Get a quick look at the tibble
```

```
## Error: object 'movieLens' not found
```

Now that we've had a quick look at the dataset, it would be interesting to explore the rows (observations) in some more detail. I'd like to consider the movie entries that...

-   belong *exclusively* to the genre *"Drama"*;
-   don't belong *exclusively* to the genre *"Drama"*;
-   were filmed *after* the year 2000;
-   were filmed in 1999 *or* 2000;
-   have *more than* 4.5 stars, and were filmed *before* 1995.


``` r
### ERROR HERE ###
filter(movieLens, genres == "Drama")
```

```
## Error: object 'movieLens' not found
```

``` r
filter(movieLens, grepl("Drama",genres) & genres != "Drama") # grepl function for filtering movies that do not exclusively belong to "Drama"
```

```
## Error: object 'movieLens' not found
```

``` r
filter(movieLens, year > 2000) # Change >= to >
```

```
## Error: object 'movieLens' not found
```

``` r
filter(movieLens, year == 1999 | year == 2000) # Change month to year
```

```
## Error: object 'movieLens' not found
```

``` r
filter(movieLens, rating > 4.5, year < 1995)
```

```
## Error: object 'movieLens' not found
```

While filtering for *all movies that do not belong to the genre drama* above, I noticed something interesting. I want to filter for the same thing again, this time selecting variables **title and genres first,** and then *everything else*. But I want to do this in a robust way, so that (for example) if I end up changing `movieLens` to contain more or less columns some time in the future, the code will still work. Hint: there is a function to select "everything else"...


``` r
### ERROR HERE ###
movieLens %>%
  filter(genres != "Drama") %>% # Filter out movies belonging to drama
  select(title, genres, everything()) # Move all other columns to the right of title and genres
```

```
## Error: object 'movieLens' not found
```

## Exercise 2: Calculating with `mutate()`-like functions

Some of the variables in the `movieLens` dataset are in *camelCase* (in fact, *movieLens* is in camelCase). Let's clean these two variables to use *snake_case* instead, and assign our post-rename object back to "movieLens".


``` r
### ERROR HERE ###
movieLens <- movieLens %>%
  rename(user_id = userId, # Corrected function for renaming
         movie_id = movieId) # Corrected function for renaming
```

```
## Error: object 'movieLens' not found
```

As you already know, `mutate()` defines and inserts new variables into a tibble. There is *another mystery function similar to `mutate()`* that adds the new variable, but also drops existing ones. I wanted to create an `average_rating` column that takes the `mean(rating)` across all entries, and I only want to see that variable (i.e drop all others!) but I forgot what that mystery function is. Can you remember?


``` r
### ERROR HERE ### 
transmute(movieLens,
       average_rating = mean(rating))
```

```
## Error: object 'movieLens' not found
```

## Exercise 3: Calculating with `summarise()`-like functions

Alone, `tally()` is a short form of `summarise()`. `count()` is short-hand for `group_by()` and `tally()`.

Each entry of the movieLens table corresponds to a movie rating by a user. Therefore, if more than one user rated the same movie, there will be several entries for the same movie. I want to find out how many times each movie has been reviewed, or in other words, how many times each movie title appears in the dataset.


``` r
movieLens %>%
  group_by(title) %>%
  tally()
```

```
## Error: object 'movieLens' not found
```

Without using `group_by()`, I want to find out how many movie reviews there have been for each year.


``` r
### ERROR HERE ###
movieLens %>%
  count(year) # Corrected tally to count
```

```
## Error: object 'movieLens' not found
```

Both `count()` and `tally()` can be grouped by multiple columns. Below, I want to count the number of movie reviews by title and rating, and sort the results.


``` r
### ERROR HERE ###
movieLens %>%
  count(title, rating, sort = TRUE) # Corrected function for count
```

```
## Error: object 'movieLens' not found
```

Not only do `count()` and `tally()` quickly allow you to count items within your dataset, `add_tally()` and `add_count()` are handy shortcuts that add an additional columns to your tibble, rather than collapsing each group.

## Exercise 4: Calculating with `group_by()`

We can calculate the mean rating by year, and store it in a new column called `avg_rating`:


``` r
movieLens %>%
  group_by(year) %>%
  summarize(avg_rating = mean(rating))
```

```
## Error: object 'movieLens' not found
```

Using `summarize()`, we can find the minimum and the maximum rating by title, stored under columns named `min_rating`, and `max_rating`, respectively.


``` r
### ERROR HERE ###
movieLens %>%
  group_by(title) %>% # Group by title
  summarize(min_rating = min(rating), # Corrected mutate to summarize
         max_rating = max(rating))
```

```
## Error: object 'movieLens' not found
```

## Exercise 5: Scoped variants with `across()`

`across()` is a newer dplyr function (`dplyr` 1.0.0) that allows you to apply a transformation to multiple variables selected with the `select()` and `rename()` syntax. For this section, we will use the `starwars` dataset, which is built into R. First, let's transform it into a tibble and store it under the variable `starWars`.


``` r
starWars <- as_tibble(starwars)
```

We can find the mean for all columns that are numeric, ignoring the missing values:


``` r
starWars %>%
  summarise(across(where(is.numeric), function(x) mean(x, na.rm=TRUE)))
```

```
## # A tibble: 1 × 3
##   height  mass birth_year
##    <dbl> <dbl>      <dbl>
## 1   175.  97.3       87.6
```

We can find the minimum height and mass within each species, ignoring the missing values: 


``` r
### ERROR HERE ###
starWars %>%
  group_by(species) %>%
  summarise(across(c(height, mass), ~min(.x, na.rm=TRUE), .names = "min_{.col}")) # Corrected function for finding minimum
```

```
## Warning: There were 6 warnings in `summarise()`.
## The first warning was:
## ℹ In argument: `across(c(height, mass), ~min(.x, na.rm = TRUE), .names =
##   "min_{.col}")`.
## ℹ In group 4: `species = "Chagrian"`.
## Caused by warning in `min()`:
## ! no non-missing arguments to min; returning Inf
## ℹ Run `dplyr::last_dplyr_warnings()` to see the 5 remaining warnings.
```

```
## # A tibble: 38 × 3
##    species   min_height min_mass
##    <chr>          <int>    <dbl>
##  1 Aleena            79       15
##  2 Besalisk         198      102
##  3 Cerean           198       82
##  4 Chagrian         196      Inf
##  5 Clawdite         168       55
##  6 Droid             96       32
##  7 Dug              112       40
##  8 Ewok              88       20
##  9 Geonosian        183       80
## 10 Gungan           196       66
## # ℹ 28 more rows
```

Note that here R has taken the convention that the minimum value of a set of `NA`s is `Inf`.

## Exercise 6: Making tibbles

Manually create a tibble with 4 columns:

-   `birth_year` should contain years 1998 to 2005 (inclusive);
-   `birth_weight` should take the `birth_year` column, subtract 1995, and multiply by 0.45;
-   `birth_location` should contain three locations (Liverpool, Seattle, and New York).


``` r
### ERROR HERE ###
fakeStarWars <- tribble(
  ~name,            ~birth_weight,  ~birth_year, ~birth_location, # Added missing comma
  "Luke Skywalker",  1.35      ,   1998        ,  "Liverpool, England", # Added quotation marks for all strings
  "C-3PO"         ,  1.80      ,   1999        ,  "Liverpool, England",
  "R2-D2"         ,  2.25      ,   2000        ,  "Seattle, WA",
  "Darth Vader"   ,  2.70      ,   2001        ,  "Liverpool, England",
  "Leia Organa"   ,  3.15      ,   2002        ,  "New York, NY",
  "Owen Lars"     ,  3.60      ,   2003        ,  "Seattle, WA",
  "Beru Whitesun Iars", 4.05   ,   2004        ,  "Liverpool, England",
  "R5-D4"         ,  4.50      ,   2005        ,  "New York, NY",
)
```

## Attributions

Thanks to Icíar Fernández-Boyano for writing most of this document, and Albina Gibadullina, Diana Lin, Yulia Egorova, and Vincenzo Coia for their edits.
