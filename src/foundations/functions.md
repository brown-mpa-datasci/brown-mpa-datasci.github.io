# Functions

One of the most fundemental methods of organizing code—in any language—is with the use of functions. A function is basically a stand-alone block of code that we can use to carry out operations. In many cases, functions in programming languages work like functions in math; that is, they take some inputs, perform some operations, and then produce some output.

There are a number of reasons for defining functions; one of the more obvious reasons for defining a function is that it allows us to compartmentalize our code in a rational way. For example if we have some lengthy set of operations we want to perform on some given input, we might want to write a function that carries out that set of operations. This way, instead of repeatedly carrying out the operations in an explicit manner, we simply call the function repeatedly.

## Defining a Simple Function

Functions in R are simply another kind of object. And as such, we create functions using the assignment operator (i.e., `<-`) that we have already encountered. For example, the code snippet below creates a function cleverly called `add_one()` that adds `1` to whatever we pass it.

```r
add_one <- function(x) {
    x_plus1 <- x + 1          # add 1 to x 
    return(x_plus1)           # return result of x + 1
}

```

The code snippet above defines a function that has a parameter, `x`, and then returns a new variable that is the result of adding `x` and `1` together. 

Another noteworthy point from the above snippet is our use of indentation. When defining functions, or using other constructs in R that contain a "code block", it is considered best practice to use indentation to denote the code block. The convention in R is to use 4 spaces, or a tab that indents the equivalent of 4 spaces. Note that this is only a stylistics convention.[^5] 

### Using a Function

The above snippet has defined this function. Now when we actually want to use the function, we do so as we would any other function (e.g., the `print()` function, which we have used widely already).

```r
add_one(42)
```

As expected, our function takes single argument, `42`, and then returns the result of `42` plus `1`. Note that, like other functions, if we wanted to store the result of our function, we would simply assign that to a new variable. 

```r
a <- add_one(137)

print(a)
```

The snippet above illustrates how we would use our function assign its results to a new variable, `a`. And again, this is the same behavior as we would see with any of the built-in R functions.

It is worth noting that our function can also take other variables as arguments. That is, we need not pass it an integer literal. Consider the example below. 

```r
z <- 13 
y <- add_one(z) 

print(y)
```

## Functions with Multiple Arguments

We can also define functions that accept multiple arguments. The code snippet below illustrates how this is done.


```r
adding_something <- function(a, b) {
    res <- a + b 
    return(res)
}
```

We can then use the `adding_something()` function much like we did with `add_one()`. And as we did before, if we wanted to use the output of the function, we can simply assign it to a new variable. 

```r
u <- adding_something(21, 29)

print(u)
```




### Default Function Arguments

Often we want functions to perform a given operation with some default arguments. Suppose, for example that we have a function that strips the last characters from a string. And further suppose that when we strip characters, we usually want to strip only the last character in the string. We can do this using a function like the one below. 

```r
strip_ending <- function(s, m = 1) {
    n <- nchar(s)                 # get number of characters 
    new_s <- substr(s, 1, n - m)  # cut `m` characters
    
    return(new_s)
}
```

Now, we can call this function to remove the last characters of a string. By default, it will remove the last 1 character, but we can changes this to be any number we want. This is illustrated below. 

```r
my_name <- "jones."

a <- strip_ending(my_name)

b <- strip_ending(my_name, m = 3)

print(a)
print(b)
```

Running the above code, we see that the first function call creates an object `a` that holds the string `"jones"`, and the string `b` that holds the string `"jon"`. And of course, we note that the two function calls are taking the same input string as their first argument (i.e., `my_name`); the only difference is that in the first case, we let the default argument determine the number of characters to strip off the end—in the second case, we specify it explicitly.







[^5]: Note that in R (unlike in Python), indentation is not actually required for defining code blocks. The use of curly braces (i.e., `{` and `}`) is what R uses to denote code blocks. Nonetheless, indentation makes our code _vastly_ more readable, and we will always use indentation in practice.
