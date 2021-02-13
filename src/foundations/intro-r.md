# The R Programming Language

The R programming language has a rather interesting history. The language itself was developed in the mid 90s by two statisiticians—Ross Ihaka and Robert Gentlemen. But interestingly, the language that Ihaka and Gentlemen developed is actually an implementation of the S programming language, which was developed at Bell Labs primarily by John Chambers in the mid 70s. It is important to note that there was a commercial version of the S language sold under the name _S Plus_ in the 80s. However, R, the language that Ihaka and Gentlemen developed was free and open-source.

## Why R?
The original S language was developed specifically for its application to statistical problems. At the time, a great deal of statisitical problems were being solved using the "lower-level"[^1] language called _Fortran_. While the Fortran programming language was (and still is) known of it's speed of execution, the syntax and semantics of the language make it not-so-friendly for reading, writing, and debugging.

Both the S programming language—and later R—were designed to give the user access to a "high-level" language that could be used for quickly developing code to solve problems and answer statistical questions. In sum, R is a language that is meant to make it easy to work with data.



---
[^1] The term "lower-level" when referring to a programming language is not in any way derogatory. Instead, it referrs to languages which provide a high degree of access and control over the machine's resources (e.g., processor, memory, storage, networking). Low-level languages are said to be "close to the metal".