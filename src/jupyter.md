# Jupyter Notebooks

In the last decade or so the Jupyter notebook has become a ubiquitous tool in data science and many fields that rely on technical computing languages. As the name implies, a Jupyter notebooks is a document that can be used to store notes; but more than that, Jupyter notebooks are in fact a kind of "executable document". You can write notes (using Markdown, if you'd like), write your code, plot your output, see the results of your code, etc. This can all be done in an interactive environment.

## History
Jupyter notebooks were originally called IPython Notebooks, which reflects the fact that at one point only Python was a supported programming language.[^1] Since then, Jupyter notebooks have been expand to support a huge variety of programming languages. The name "Jupyter" itself is the concatenation of the names Julia, Python, and R, which are the big three technical computing languages for data science. But beyond that, Jupyter notebooks now support many dozens of programming languages including Rust, C++, Haskell, JavaScript, Ruby, and many, _many_ others. 

## Notebook Elements
Jupyter notebooks are made of "cells". Each cell is either (a.) text, (b.) code, or (c.) output. In text cells, we can simply write notes for ourselves and future users. In code cells we can write code to be executed using `shift` + `enter` when selecting a given cell. Output cells can either be text output printed from your code, or plot and visualizations that your code geneates. 



---
[^1] "Kernel" is the term of art for the language that is the behind any given notebook. A Jupyter notebook of Python code is said to being using "a Python kernel". 