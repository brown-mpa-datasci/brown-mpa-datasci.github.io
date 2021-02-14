# The _dplry_ Package

Like the vast majority of programming languages—particularly those that are open-source—the R language relies on a huge number of "add-on" modules that can be loaded to supplement the base language. These add-on modules are frequently called "packages" or "libraries"[^1].

The _dplyr_ package was developed by Hadley Wickham, who also continues to be the primary maintainer, as well as the most prolific contributor to the package. The package was a successor to the _plyr_ package, which was also authored by Wickham.[^2] 

# Why _dplyr_?

The name _dplyr_ is short for "data plier". This reflects the author's intent for the package. In particular, it is meant to be a package for working with, cleaning, aggregating, and summarizing our data. If you are a person who uses tabular-type data (i.e., data in the form of rows and columns), it is very likely that you will find _dplyr_ massively useful. Part of the utility of the package comes from the easy of use, as well as its many built-in functions. But another huge part of its utility comes from the philosophical motivation. 

The _dplyr_ package (and much of Wickham's work) centers on the notion of "[tidy data](https://cran.r-project.org/web/packages/tidyr/vignettes/tidy-data.html)". The key features of tidy data arae the following.

1. Each variable forms a column.

2. Each observation forms a row.

3. Each type of observational unit forms a table.


# The _dplyr_ Grammar
The _dplyr_ package is designed to solve several of the most common operations related to working with tabular data (i.e., data in a `data.frame` or similar object). These operations include: selecting, summarizing, arranging, mutating, and filtering. And as such, the operations are encapsulated by the following function in _dplyr_: 

1. `select()`

2. `summarise()`

3. `arrange()`

4. `mutate()`

5. `filter()`


## The `select()` Function
We can use the `select()` function to "select" some desired columns from a `data.frame` (or similar object).[^3] In the example below we load the _dplyr_ package and then use the `select()` function to obtain the `name`, `species`, and `height` columns from the `starwars` dataframe. 

```r
library(dplyr)

starwars %>%
    select(name, species, height)
```

Also note in the code snippet above the use of the "piping" operator `%>%` that we use to "pipe" the `starwars` dataframe in to the `filter()` function. This piping operator passes the object on the left and then places it as the first argument to the function on the right. The piping operator—though not originally from the _dplyr_ package—is exceedingly popular in examples of _dplyr_ code. Part of the reason for its popularity, is likely the capability to "chain" results of the piping operator together. We will see this in a future example.

## The `arrange()` Function
As the name implies, we can use the `arrange()` function to sort the rows of a dataframe. In the example below, we take the `starwars` dataframe and sort it according to the `height` column.

```r
starwars %>%
    arrange(height)
```
### Chaining the `arrange()` Function
As mentioned above, we will very often see _dplyr_ function calls "chained" in sequence using the `%>%` operator. In the case below, we are combining our two previous examples aand thus selecting only the `name`, `species` and `height` columns, and then finally sorting the result according to the `height` column.

```r
starwars %>%
    select(name, species, height) %>%
    arrange(height)
```

At this point, we should point out an important feature of the _dplyr_ (and many other) functions in R. Specifically, the three examples above have not altered the original `starwars` dataframe. In fact, the examples above have only demonstrated how we would use the `select()` and `arrange()` function on the dataframe. For us to obtain any usable object from the `select()` and `arrange()` functions, we would need to assign the result of the function calls to a new object using `<-` assignment operator. The example below illustrates this, as well as the use of the `desc()` function, which when used with the `arrange()` function allows us to sort in descending order.

```r
dat <- starwars %>%
           select(name, species, height) %>%
           arrange(desc(height))
```






---
[^1] The term "library" is often used to mean something a bit more specific in many programming circles, so we will tend to use the word "package" in R. To add to the confusion a bit, the mechanism of loading packages in R is to use the `library()` function... `¯\_(ツ)_/¯`

[^2] It is worth noting here that Hadley Wickham is of the most influential developers in the R community. He is responsible for staggering amount of the modern tools used every day by R programmers, and he has simplified the lives of researchers and data scientists across the world.

[^3] Rather than continuing to say "`data.frame` (or similar object)" we will now simply refer to `data.frame` objects. It should be noted, however, that this also includes objects such at the `tibble` from the _tibble_ package (and also exposed in the _dplyr_ package).