---
layout: post
title: Cross-validation using the function classify()
author: Maciej Eder
date:   2017-12-13
description: Cross-validation using the function `classify()`
---



This post assumes that the reader is familiar with supervised
machine-learning classification methods and their main advantage, namely
the ability to assess the quality of the trained model. This can be
accomplished via cross-validation, or a number of swaps between the
training and the testing sets. There are several great introductions
into the fascinating world of machine-learning (cross-validation being
covered in almost all of them), including tons of materials on the
internet. I personally love the book on statistics with R by James and
his colleagues (2013). The following sections will be focused on two
functions provided the R package `stylo`.

Performing cross-validation is relatively straightforward using the
function `classify()`, without any manual swaps between the two sets.
You define your `primary_set` and the `secondary_set`, and then you
invoke the function indicating the number of cross-validation folds:

``` r
classify(cv.folds = 10)
```

or, if you want to have an access to particular cv folds:

``` r
# perform the classification:
results = classify(cv.folds = 10)

# get the classification accuracy:
results$cross.validation.summary
```

This will give you the stratified cross-validation, or the variant that
reproduces the representation of classes from your `training_set` in *N*
random iterations.

Now, there is a function `crossv()` that is meant to replace some core
fragments of `classify()` in the future. I am not there yet, though. So
far, it is not fully functional. To perform leave-one-out
cross-validation, you prepare the `training_set` only, and put your
stuff there. Then you have to load the corpus, and prepare a
document-term matrix. Let’s assume you’ve already got it:

``` r
library(stylo)
data(galbraith)
```

Type `help(galbraith)` to see what the matrix contains. Then you
type:

``` r
crossv(training.set = galbraith, cv.mode = "leaveoneout", classification.method = "svm")
```

To build the document-term matrix, some more steps have to be undertaken
beforehand:

``` r
library(stylo)

# loading the corpus
texts = load.corpus.and.parse(files = "all", corpus.dir = "corpus")

# getting a genral frequency list
freq.list = make.frequency.list(texts, head = 1000)
# preparing the document-term matrix:
word.frequencies = make.table.of.frequencies(corpus = texts, features = freq.list)

# now the main procedure takes place:
crossv(training.set = word.frequencies, cv.mode = "leaveoneout", classification.method = "svm")
```

Needless to say, it is wise to store the results of your
cross-validation procedure in a variable rather than letting it fly
away, hence the above code should be slightly refined:

``` r
# the same as above but saved to a variable:
results = crossv(training.set = word.frequencies, cv.mode = "leaveoneout", classification.method = "svm")
```

By piping the results into a variable, you can further assess the
distribution of the accuracy scores acros the cross-validation folds,
which tells you quite a lot about your corpus. There is a study (Eder
and Rybicki, 2013) comparing different corpora and their distributions
of authorship attribution accuracy scores under intense cross-validation
scenarios.

## References

**Eder, M. and Rybicki, J.** (2013). [Do birds of a feather really flock together, or how to choose training samples for authorship attribution](http://llc.oxfordjournals.org/content/28/2/229). _Literary and Linguistic Computing_, **28**(2): 229-36, [[pre-print](https://github.com/computationalstylistics/preprints/blob/master/Eder-Rybicki_How_to_choose.pdf)].

**James, G., Witten, D., Hastie, T. and Tibshirani, R.** (2013). [_An
Introduction to Statistical Learning with Applications in R_](https://www-bcf.usc.edu/~gareth/ISL/). New York:
Springer.

