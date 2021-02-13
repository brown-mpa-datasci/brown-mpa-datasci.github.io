# Control Flow

In any software application or script it is often essential to be able to control the "flow of execution". For example, suppose that a portion of our code should only be execute if some condition is met. Or in a different example, suppose that we want a function in our code to excute repeatedly—perhaps even hundreds, thousands, or millions of times. These are examples of problems we can solve using control flow statements in R.



## The `if` Statement

One of the most commonly used mechanisms of controling flow of execution is with the use of `if` statements. The `if` statement, unsurprisingly, allows us to execute a piece of code _if_ some conditiion is met. Consider the example below.

```r
v <- 17

if (v > 8) {
    print("Hello!")
}
```

The code above prints `"Hello!"`; but of course, if we set `v` to be equal to `8` or less, then nothing will be printed. Note also that we can (and usually do) have more complicated operations in our `if` blocks.



## The `else` Statement

Much like the `if` statement, the `else` statement can be used to execute some piece of code based on conditions being met or not met. The example below extends our previous example. 

```r
u <- 27

if (u > 100000) {
    print("u is a large number!")
} else {
    print("u is not that large...")
}
```

As we see in the example above, the code in the `else` block is executed since `u` is set to be less than `100000`. Note that the `else` block must follow an `if` block. But note also that not every `if` block has an `else` block.



### Sequential `if`/`else` Statements

A common pattern, and one that you may use yourself is to have a sequence of `if` and `else` statements. Consider the example below. 
```r
today <- "Friday"

if (today == "Monday") {
    print("Boo...")
} else if (today %in% c("Tuesday", "Wednesday", "Thursday")) {
    print("...")
} else if (today %in% c("Friday", "Saturday", "Sunday")) {
    print("Yay!")
} else {
    print("Hmm... what day is this?")
}
```

The code above has a few different possible paths of execution; in particular, there are 4 possible  paths that the code might take based on the content of the variable `today`. Note that the possible branches here are mutually exclusive; that is, only one of those four branches will execute on any given run of this code. 

As an aside, the code block above also introduces the `%in%` operator, which checks for containment. Essentially, the expression `a %in% b` returns a boolean value when `a` is an element of `b`. For example `3 %in% 1:10` would return `TRUE` since `3` is in the range of `1` to `10`. 



## Looping
 
In addition to controling our code's flow of execution with conditional branching, it is also hugely useful to be able to repeatedly carry out operations. This kind of repeated execution can be accomplished using a few "looping" statements. In particular, we will explore the `for` loop and the `while` loop. We will also discuss their respective strengths.


## The `for` Loop
One of the most commonly used constructs in almost any programming language is the `for` loop. The `for` loop gives us a way to execute a give code block a specified number of times. For example, the code snippet below prints the integers from 1 to 5.

```r
for (i in 1:5) {
    print(i)
}
```

It is worth pointing out here that directly after the `for` statement, and in between the parentheses, is where we specify how many iterations the loop will execute. Specifically, when we say `(i in 1:5)`, what we are actually saying is that the code block will execute 5 times, with `i` taking a different value each time (i.e., `1` on the first iteration, `2` on the second, and so on).

Note that there is no requirement that we use the index variable (e.g., `i`) in the body of our loop. Also note that the index variable can be named arbitrarily, just like any other variable in R. Consider the example below.

```r
for (soup in 1:6) {
    print("Hello!")
}
```

In the above example, we call our index varaible `soup`; and note that we never actually use the variable in the loop's body. 



## The `while` Loop

The `while` loop is very similar to the `for` loop. The key difference is that the `while` loop can be used when we do not know ahead of time the number of iterations we want to use. A very common example is one in which we are doing some kind of approximation, and we want to keep going until some value in the computation surpasses some threshold. Consider the example below.

```r
a <- 100

while (a > 1) {
    print(a)
    a <- a/2
}
```

As we see in the above snippet, the `while` loop is similar to the `for` loop in the sense that there is an expression in parentheses after the `while` keyword. It is this expression that controls how many iterations our loop will execute. In the example above, the loop executes until the variable `a` has a value less than `1`. 



## Chosing Between `for` and `while` Loops

In general, we can accomplish almost every kind of looping task with either a `for` loop or a `while`. When choosing which one to use, the general rule-of-thumb is to use a `for` loop when we know in advance the number of iterations we want to execute, and to use a `while` loop when we do not.


## Early Exit and Skipping Iterations
The `for` loop and `while` loop give us a great deal of power and flexibility in terms of excuting repeated operations. Another very useful feature of both of these is the ability to exit the loop early and to skip iterations as needed. These two features are implemented using `break` and `next` constructs. Both of these statements allow us to control the loop's behavior from within the actual loop itself. 





### Using `break` to Exit Early
Often, we are in the position of generally knowing the nuber of iterations we want to execute, but also want to be able to exit our loop if something occurs. This is the usecase for the `break` statement. By using `break`, we are able to prematurely exit a loop prior to its natural stopping point. Consider the example below. 

```r
for (i in 1:100) {
    print(i)
    if (i > 5) {
        print("oh, no!!")
        break
    }
}
```

As we see above, the code is meant to execute 100 iterations, but we exit the loop after only 6 iterations. This is a somewhat contrived example, since we could have just as easily used a `while` loop to accomplish this, but the point is clear. Also note that this is the first time we have seen an `if` statement embeddeded in a loop. This is actually a very common practice. In fact, you will also frequently see loops embedded in other loops and various combinations of `if` and `else` statements in different combinations of `for` and `while` loops. 



### Using `next` to Skip an Iteration
Somewhat like `break`, we can use the `next` statement to control the behavior of a loop from within the loop. Consider the example below. 

```r
for (i in 1:10) {
    if (i %% 2 == 0) {
        next
    }
    print(i)
}
```

In the above example we use the `next` statement to skip all the iterations where `i` is an even number (recall that the modulo operator gives us the remainder of integer division).