# The _dplry_ Package

Like the vast majority of programming languages—particularly those that are open-source—the R language relies on a huge number of "add-on" modules that can be loaded to supplement the base language. These add-on modules are frequently called "packages" or "libraries"[^1].

The _dplyr_ package was developed by Hadley Wickham, who also continues to be the primary maintainer, as well as the most prolific contributor to the package. The package was a successor to the _plyr_ package, which was also authored by Wickham.[^2] 

# Why _dplyr_?

The name _dplyr_ is short for "data plier". This reflects the author's intent for the package. In particular, it is meant to be a package for working with, cleaning, aggregating, and summarizing our data. If you are a person who uses tabular-type data (i.e., data in the form of rows and columns), it is very likely that you will find _dplyr_ massively useful. Part of the utility of the package comes from the easy of use, as well as its many built-in functions. But another huge part of its utility comes from the philosophical motivation. 

The _dplyr_ package (and much of Wickham's work) centers on the notion of "[tidy data](https://cran.r-project.org/web/packages/tidyr/vignettes/tidy-data.html)". The key features of tidy data arae the following.

    1. Each variable forms a column.
    
    2. Each observation forms a row.
    
    3. Each type of observational unit forms a table.



---
[^1] The term "library" is often used to mean something a bit more specific in many programming circles, so we will tend to use the word "package" in R. To add to the confusion a bit, the mechanism of loading packages in R is to use the `library()` function... `¯\_(ツ)_/¯`

[^2] It is worth noting here that Hadley Wickham is of the most influential developers in the R community. He is responsible for staggering amount of the modern tools used every day by R programmers, and he has simplified the lives of researchers and data scientists across the world.

