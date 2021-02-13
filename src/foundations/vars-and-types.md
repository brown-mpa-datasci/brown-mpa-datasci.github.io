# Variables and Types

## Basic Math with R

We can begin our exploration of R by using it in the most straightforward manner; that is, we will use R as a "fancy calculator". We will quickly see that R is capable of vastly more than a calculator, but this is a good place for us to begin our journey.


```r
13 + 7
```

We see from above that R can nicely perform simple addition. And the example below also demonstates slightly more interesting arithmetic.

```r
13 + 7 * 100
```

As we can see above, R will respect the rules that govern order of operation in arithemetic. If we wanted to be more explicit, we could also add parantheses to the above expression. 

```r
13 + (7 * 100)
```


And of course, we can also use the parantheses to control the order of operations and change the above result.

```r
(13 + 7) * 100
```


## Variable Assignment 

In a more realistic scenario, we would perform some computation and also want to preserve the result in some way such that it is accessible for subsequent computations. Essentially, we want to tell the machine "_Do this math, and store the result_". This is something we can acheive using the assignment operator in R. The assignment operator in R is the arrow `<-`, which we construct using the less-than symbol combined with the dash symbol.[^1]

```r
a <- 13 + 7
```




Programming is essentially just about giving a computer instructions. The above code is us telling the computer to take `13` and `7`, add them together, and then put the result in `a`. Here `a` is just a completely arbitrary label for the result of `13 + 7`.[^2] 



Note that the above code snippet does not immediately generate output. However, this is the default behavior when performing assignment. But now if we wanted to print the result of the computation, we can simply use the `print()` function in R.

```r
print(a)         # show us the value of `a`
```

Two things are worth noting from the code snippet above. First, we have seen our first example of the `print()` function. This is a function in R that is used to display the contents of objects. Here, we pass `a` to the print function, and we then observe the value of `a`, which is `20` as expected. 

The second thing to note is that we have now seen our first comment. Using the `#` character is how we tell R that we are just leaving a note for our future selves or others who end up reading our code. Everything on the line that is to the right of `#` will not be evaluated by R.

## Basic Types

There are a few things that contribute to how a programming languages "feels". Without question, one of the key elements is the language's type system. A language's type system essentially refers to the kinds of values the langauge can represent (e.g., integers, boolean values, strings of characters, _etc_.).


### Numeric Types

We have already seen examples of a numeric type. In the examples above, computing the sum of `13` and `7` gives us an integer value. We can inspect the type of an element with the `typeof()` function. 

```r
b <- 17 + 13         

typeof(b)   
```

We see the above result is `"double"`, which stands for "_double precision floating point number_". This is how R stores the result of many numeric operations. Consider the example below.

```r
d <- 1.3 + 7.1

typeof(d)
```



### Boolean Types

Like most other languages, R is also capable of representing Boolean values (i.e., `logical` values `TRUE`, and `FALSE`). As we will see later, these kinds of values end up being very useful when working with conditional expressions.

```r
bool_val <- FALSE

typeof(bool_val)
```

Like many other langauges, R also lets us do arithmetic with boolean values. Consider the example below. 

```r
num_trues <- TRUE + FALSE + TRUE 

print(num_trues)
```

This is something that we will see later has the ability to help us count occurences.


### Character Strings

Another hugely important type of variable is the character string. These are simply the type `character` in R. The character string is simply a sequence of letters. Consider the example below.

```r
dog_name <- "willie"

typeof(dog_name)
```

Here, we have created a character string called `dog_name`, and we assign it the value of `"willie"`. And upon checking, we also see that this variable has the type `character`. 

We can perform many intesting operations on character strings. Suppose we wanted to paste together two character strings; we can do so using the `paste()` function in R. 

```r
pets <- paste("willie", "and leo")   # paste together

print(pets)
```

We can also take variables saved as strings and paste them together. 

```r
my_opinion <- paste(pets, "are great!")

print(my_opinion)
```

Here we see that we can take the saved string variable `pets` and paste it together with `"are great!"`.

We can also change between upper and lowercase characters by using the `toupper()` and the `tolower()` functions, respectively. Consider the example below.

```r
my_loud_opinion <- toupper(my_opinion)

print(my_loud_opinion)
```


Much as we use the `paste()` function to combine character strings, we can use the `substr()` function to take subsets of a given string. For example the snippet below returns the first 3 elements of the string `my_opinion` and stores them in a new variable called `name_fragment`, which we then print.

```r
name_fragment <- substr(my_opinion, 1, 3)

print(name_fragment)
```


There are a host of other functions for working with strings in R. And we will later explore many that live in the `stringr` add-on package in R.




## Container Types

As the name implies, container types in R tend to be types that "hold things". There are many different container types in R, and we will explore the most common and useful here. 

### The `vector` Type
One hugely usefull example of a container type is the `vector` type. This is effectively just an ordered sequence of entries. We can construct `vector` types in a number of ways, but the most basic is using the `c()` funciton. The `c()` function basically concatenates the elements that we pass it in to a single container. 

```r
my_vect <- c(55, 32, 123)

print(my_vect)
```

The `vector` type turns out to be one of the most fundamental in the R language. We will see vectors appear very often. Vectors can contain any type of objects, but a given vector in R will only contain a single type.

Accessing elements of a vector can be done using the square bracket notation seen below. 

```r
foo <- c(11, 22, 33)

foo[1]                # get first element
```

Like the Julia programming language, R uses 1-based indexing, which means that a vector's first element is accessed using a `1` combined with the square bracket notation. We can also obtain "slices" of a vector by using the `:` operator.

```r
bar <- c("cat", "dog", "shoe")

animals <- bar[1:2]   # get first two elements
```

The code snippet above uses the square-bracket notation for indexing combined with the `:` operator for defining a range of the vector we want to obtain.

We can also index a vector using _another vector_. That is we can index the contents of the vector `bar` by using the square-bracket notation and a second vector of indices. This is illustrated below. 

```r
people <- c("ned", "jon", "robb", "arya")

is_stark <- c(TRUE, FALSE, TRUE, TRUE)

starks <- people[is_stark]
```


### The `matrix` Type
Much the the `vector` data type, the `matrix` type is designed for holding elements that are themselves all of the same type (e.g., all numeric, or all strings, etc.).

```r
dat <- seq(1, 12)          

m <- matrix(dat, nrow = 3)

print(m)
```

Slicing and indexing an array works in much the same way as with vectors; that is, we used the familiar square-bracket notation. In the example below, we access the element in the second row, third column.

```r
m[2, 3]
```

Note that in the above example the `2` inside the square bracket corresponds to the row, and the `3` corresponds to the column. 

The matrix objects also lets us access entire rows or columns by leaving one of the indexes blank. For example, in the code snippet below, we are accessing the entire third column.

```r
m[, 3]
```

Here, we have left a blank space where the row index would typically be placed. This is the equivalent of saying "_All of these!_". We can also do the same for columns; in the example below, we are essentially saying, "_Give me the entire second row._".

```r
m[2, ]
```


## The `array` Type
Both the `vector` type and the `matrix` type can actually be thought of as simply a special case of the `array` type. An `array` is the R type for reprsenting _N_-dimensional arrays; these are containers that have elements that are all of the same type. The number of dimensions defines how we do indexing. If we have a one-dimensional `array`, we simply have a vector, so we could access the third element (for example) by using `v[3]`. If we have a two-dimensional array, this is essentially a matrix, and we can access the second row, third column (for exmample) by using `m[2, 3]`. Now suppose we want to work with a three-dimensional array. The example below creates a three-dimensional array and then illustrates how we index in to it.

```r
dat <- seq(1, 24)

arr <- array(dat, c(4, 2, 3))

print(arr)

arr[2, 1, 3]     # second row, first column, third layer
```

In the example above, we create a three-dimensional array called `arr`, and then we use the familiar bracket notation to get the element in the second row and first column of the third "layer". 

When taking slices of `array` objects, we can also leave indices blank to indicate "_All of these!_" as we did with the `matrix` object. For example, in the snippet below we get the entire third layer of the `arr` array. 

```r
arr[, , 3]
```





---

[^1]: Strictly speaking, there are a few assignment operators in R, including the equal sign, which is much more common in other programming languages. However, when learning a programming language, it is generally preferred to adopt the conventions of the language. And the convention in R has always been to use `<-` for assignments.

[^2]: It is worth noting that variable names are almost completely arbitrary; we could just as easily have said `potato <- 13 + 7`, and the only difference is that when we want to retrieve the value, we would now use `potato` to refer to it rather than `a`. The only restriction on variable names in R is that they must begin with an upper or lowercase letter.