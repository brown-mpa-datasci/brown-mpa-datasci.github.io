
# Other Interesting Types
R has a number of other interesting types in the base language. The types discussed below are interesting in a number of ways. Of particular interest is the manner in which they hint at the early use cases and motivations for developing the R langauge; that is, working with tabular data, that is continuous or categorical, and which sometimes contain missing values. 

# The `NA` Type

One exceedingly common feature of working with real data sets is that they contain missing values. That is, for whatever reason, some entry was omitted for a given record. As an example, suppose a patient did not enter their age on the patient intake form. This would be a missing value that we then have to handle. 

Missing data is so ubiquitous in real data sets that R has a built-in type for representing missing values. This is the `NA` type. The `NA` type is special in the sense that it "propogates" over computations. Note the example below, where we try to take the summation of the elements in the `vals` vector. 

```r
vals <- c(4, 23, NA)

sum(vals)
```

