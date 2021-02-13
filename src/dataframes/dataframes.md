# The `data.frame` and Tidy Data 

In this lesson we will cover the basics of data in R and will do so from a somewhat opinionated viewpoint of "Tidy Data".  There are other paradigms and other ways to work with data in R, but focusing on Tidy Data concepts and tools (a.k.a., The Tidyverse) gets people to a productive place the quickest.  For more on data analysis using the Tidyverse, the best resource I know of is [R for Data Science](http://r4ds.had.co.nz).  The approaches we will cover are very much inspired by this book.


## The `data.frame`

Simply put, a data structure is a way for programming languages to handle storing information.  Like most languages, R has several structures (vectors, matrix, lists, etc.).  But R was originally built for data analysis, so the `data.frame`, a spreadsheet like structure with rows and columns, is the most widely used.  In addition, the `data.frame` is the basis for many modern R pacakges (e.g. the tidyverse) and getting used to it will allow you to quickly build your R skills.

Best way to learn what a data frame is is to look at one.  Let's now build a simple data frame from scratch with the `data.frame()` function.  This is mostly a teaching excercise as we will use the function very little in the excercises to come.  


```r
# Our first data frame

my_df <- data.frame(names = c("jones","lee","smith","yang"), 
                    age = c(45, 27, 38,51), 
                    knows_r = c(FALSE, TRUE, TRUE,FALSE), 
                    stringsAsFactors = FALSE)
my_df
```

That created a data frame with 3 columns (names, age, knows_r) and four rows.  For each row we have some information on the name of an individual (stored as a character/string), their age (stored as a numeric value), and a column indicating if they know R or not (stored as a boolean/logical).

If you have worked with data before in a spreadsheet or from a table in a database, this rectangular structure should look somewhat familiar.   One way (there are many!) we can access the different parts of the data frame is like:


```r
# Use the dollar sign to get a column
my_df$age
```


```r
# Grab a row with indexing
my_df[2,]
```

At this point, we have:

- built a data frame from scratch
- seen rows and columns
- heard about "rectangular" structure
- seen how to get a row and a column

The purpose of all this was to introduce the concept of the data frame.  Moving forward we will use other tools to read in data, but the end result will be the same: a data frame with rows (i.e. observations) and columns (i.e. variables).

## Reading in data

Completely creating a data frame from scratch is useful (especially when you start writing your own functions), but more often than not data is stored in an external file that you need to read into R.  These may be delimited text files, spreadsheets, relational databases, SAS files ...  You get the idea.  Instead of treating this subject exhaustively, we will focus just on a single file type, the `.csv` file, that is very commonly encountered and (usually) easy to create from other file types.  For this, we will use the Tidyverse way to do this and use  `read_csv()` from the `readr` pacakge.

The `read_csv()` function is a re-imagined version of the base R fucntion, `read.csv()`.  This command assumes a header row with column names and that the delimiter is a comma. The expected no data value is NA and by default, strings are NOT converted to factors.  This is a big benefit to using `read_csv()` as opposed to `read.csv()`.  Additionally, `read_csv()` has some performance enhancements that make it preferrable when working with larger data sets.  In my limited experience it is about 45% faster than the base R options.  



