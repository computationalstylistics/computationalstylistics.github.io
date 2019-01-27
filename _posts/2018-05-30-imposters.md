---
layout: post
title:  Authorship verification with the package ‘stylo’
author: Maciej Eder
date:   2018-05-30 16:40:16
description: Authorship verification with the package ‘stylo’
---



## Introduction

This post introduces to a new feature of the package `stylo` (ver.
0.6.7), namely the General Imposters (GI) method, also referred to as
the second verification system (o2), introduced by Koppel and Winter
(2014) and applied to the study of Julius Caesar’s disputed writings
(Kestemont et al., 2016a). To quote the authors, “\[t\]he general
intuition behind the GI, is not to assess whether two documents are
simply similar in writing style, given a static feature vocabulary, but
rather, it aims to assess whether two documents are significantly more
similar to one another than other documents, across a variety of
stochastically impaired feature spaces (Eder, 2012; Stamatatos, 2006),
and compared to random selections of so-called distractor authors
(Juola, 2015), also called ‘imposters’.” (Kestemont et al., 2016a: 88).

The implementation provided by the package `stylo` is a rather faithful
interpretation of two algorithms described in a study on authorship
verification (Kestemont et al., 2016b). A tiny function for computing
the score `c@1` used to evaluate the system is directly transplanted
from the original implementation
(<https://github.com/mikekestemont/ruzicka>).

The main procedure is available via the function `imposters()`. It
assumes that all the texts to be analyzed are already pre-processed and
represented in a form of a matrix with frequencies of features (usually
words). The function contrasts, in several iterations, a text in
question against (1) some texts written by possible candidates to
authorship, or the authors that are suspected of being the actual
author, and (2) a selection of “imposters”, or the authors that could
not have written the text to be assessed. Consequently, a given
candidate’s class is assigned a score between 0 and 1.

On theoretical grounds, any score above 0.5 would suggest that the
authorship verification for a given candidate was successful. However,
the scores such as 0.39 or 0.63 should be considered suspicious: they
seem to suggest that the classifier had problems in making clear-cut
decisions. Another function, namely `imposters.optimize()`, is meant to
assess – via a grid search – optimal parameters defining the
above-mentioned grey area where the classifier should keep shut. It is a
procedure of testing iteratively each text from a training corpus (one
at a time) against all the possible candidates. Being computationally
intense, this is a rather time-consuming task: be prepared to leave you
machine running for a few hours.

## Installation

The latest (and stable) version of the package `stylo` is usually
available on CRAN a few days after such a new version is released. In
this case, the installation is trivial:

``` r
install.packages("stylo")
```

Maybe a better way to install brand-new and/or experimental versions of
the package is to grab it directly from the GitHub repository – please
make sure, however, that you have the package `devtools` installed in
your system. The next step is straightforward:

``` r
library(devtools)
install_github("computationalstylistics/stylo")
```

If no errors occurred during the installation, we’re all set\!

## A tl;dr working example

To test at a glance what the `imposters()` function can offer, type the
following code. Notice that you don’t even need to prepare any corpus
beforehand:

``` r
# activating the package 'stylo':
library(stylo)

# activating one of the datasets provided by the package 'stylo';
# this is a table of frequences of a few novels, including "The Cuckoo's Calling"
# by Robert Galbraith, aka JK Rowling:
data(galbraith)

# to learn more about the dataset, type:
help(galbraith)

# to see the table itself, type:
galbraith

# now, time for launching the imposters method:
imposters(galbraith)
```

After a few seconds, the final results will be shown on the
    screen:

    ## 

    ## No candidate set specified; testing the following classes (one at a time):

    ##   coben   lewis   rowling   tolkien

    ## 

    ## Testing a given candidate against imposters...

    ## coben     0.34

    ## lewis     0

    ## rowling   1

    ## tolkien   0

    ##   coben   lewis rowling tolkien 
    ##    0.34    0.00    1.00    0.00

The interpretation of the results is rather straightforward: “The
Cuckoo’s Calling” was not written by CS Lewis, nor was it penned by
JRR Tolkien. Similarly, the score for JK Rowling turned out to be very
high (could not be higher), which clearly suggests the author of the
analyzed novel. The only class that is difficult to interpret is Harlan
Coben, since he was assigned 0.34. (When you run the same test again,
the final score will probably slightly differ, due to the stochastic
nature of the test). The score obviously falls into the \<0.5 category,
but still: can we reliably say that this candidate should be rulled out?
Or, rather, should we abstain from any conclusions here? The problem of
defining the “I don’t know” area around the score 0.5 will be discussed
below.

## Details

As you might have noticed, the dataset `galbraith` contains frequencies
for different texts by a few authors, the class *GALBRAITH*, however, is
represented by a single text (specifically, “The Cuckoo’s Calling”).
Whenever the function has no additional parameters passed by the user,
it tries to identify such a single text and then assumes that this is
the anonymous sample to be assessed.

Despite simplicity, however, this solution is far from being flexible.
In a vast majority of cases, one would like to have some control on
choosing the text to be contrasted against the corpus. The function
provides a dedicated parameter `test` to do the trick. Note the
following
code:

``` r
# getting the 8th row from the dataset (it contains frequencies for Galbraith):
my_text_to_be_tested = galbraith[8,]

# building the reference set so that it does not contain the 8th row
my_frequency_table = galbraith[-c(8),]

# launching the imposters method:
imposters(reference.set = my_frequency_table, test = my_text_to_be_tested)
```

Consequently, if you want to test who wrote “The Lord of the Rings”
(part 1), you first indicate the 24th row from the table, and exclude
this row from your reference corpus.

``` r
my_text_to_be_tested = galbraith[24,]
my_frequency_table = galbraith[-c(24),]
imposters(reference.set = my_frequency_table, test = my_text_to_be_tested)
```

By the way, it might be non trivial to know in advance which row of the
input table contains your disputed text. The simplest way to get the
content of the table is to request its row names via `rownames()`. One
can also use `grep()` to identify a given string of characters e.g.:

``` r
# getting the names of the texts
rownames(galbraith)

# getting the row number of a particular text (known by name):
grep("lewis_lion", rownames(galbraith)) 

# one can also combine the above-introduced snippets into one piece:
text_name = grep("lewis_lion", rownames(galbraith))
my_text_to_be_tested = galbraith[text_name,]
my_frequency_table = galbraith[-c(text_name),]
imposters(reference.set = my_frequency_table, test = my_text_to_be_tested)
```

So far, I’ve been neglecting one important feature of the imposters
method. As Kestemont et al. (2016b) show in their “Algorithm 1”, the
method tries to compare an anonymous text against (1) a candidate set,
containing the works of a probable candidate author, and (2) the
imposters set, containing lots of text by people who could not have
written the text in question. In the previous examples, where no
canditate set was explicitly indicated, the method repeatedly tested all
the available authors as potential candidates (one at a time). It is a
time consuming task. If you plan to focus on just one *actual*
candidate, e.g. if you want to test if “The cuckoo’s Calling” was
written by JK Rowling, you should define the parameters as follows:

``` r
# indicating the text to be tested (here, "The cuckoo's Calling"):
my_text_to_be_tested = galbraith[8,]

# defining the texts by the candidate author (here, the texts by JK Rowling):
my_candidate = galbraith[16:23,]

# building the reference set by excluding the already-selected rows
my_imposters = galbraith[-c(8, 16:23),]

# launching the imposters method:
imposters(reference.set = my_imposters, test = my_text_to_be_tested, candidate.set = my_candidate)
```

The above code shows a standard application of the General Imposters
method. In practice, however, I’d rather test *all* the authors
iteratively, even if this requires quite a lot of time to complete the
task. The reason is, this will serve as an additional cross-validation
step. To put it simply, one is able to check if all the *remaining*
authors – tested as if they were candidates – are indeed getting 0s
(which is expected). In an authorship verification setup, I’d rather
compare the behavior of JK Rowling in comparison to all possible
candidate authors, even if Rowling is the only class I believe would get
a reasonable score.

## Loading a corpus from text files

I am fully aware that the function `imposters()` in its current form
requires some advanced knowledge of R, since it does not provide any
corpus pre-processing (as the main functions of the package `stylo` do).
Specifically, one needs to know in advance how to produce the table of
frequencies. This step has been already described elsewhere (Eder et
al., 2016: 109–11), therefore I will not go into nuanced details here. A
straightforward way from raw text files to the final results of the
`imposters()` function might look as follows:

``` r
# activating the package
library(stylo)

# setting a working directory that contains the corpus, e.g.
setwd("/Users/m/Desktop/A_Small_Collection_of_British_Fiction/corpus")

# loading the files from a specified directory:
tokenized.texts = load.corpus.and.parse(files = "all")

# computing a list of most frequent words (trimmed to top 2000 items):
features = make.frequency.list(tokenized.texts, head = 2000)

# producing a table of relative frequencies:
data = make.table.of.frequencies(tokenized.texts, features, relative = TRUE)

# who wrote "Pride and Prejudice"? (in my case, this is the 4th row in the table):
imposters(reference.set = data[-c(4),], test = data[4,])
```

One important remark to be made, is that the frequency table is analyzed
in its entirety. In the above example, the input vector of features
(most frequent words) has 2000 elements. If you want to run the
`imposters()` function on a shorter vector of words, you should select
them in advance, e.g. to get 100 most frequent words, type:

``` r
imposters(reference.set = data[-c(4), 1:100], test = data[4, 1:100])
```

## Optimizing the decision scores

So far so good. One issue has not been resolved, though. In the example
discussed above, the novel entitled “The Cuckoo’s Calling” was assigned
the score 0.34 when tested against Harlan Coben. Is it much? Well, it
depends. Some authors might exhibit stronger signal, some other might be
stylometrically blurry. It depends on many factors which cannot be
simply accounted for once and forever. Instead, however, one might
thoroughly examine a given corpus, in order to estimate an average
proximity between any two texts written by the same author, and an
average proximity between a text by a given author and any text written
by someone else. Having done that, one can define a margin where a
classifier is (on average) wrong. This is a grey area where we should
abstain from making any “yes” or “no” conclusions.

The prodedure proposed for the General Imposters method involves a score
shifting algorithm (Kestemont et al., 2016b), which is based on the
`c@1` measure of classifier’s performance (Peñas and Rodrigo, 2011). In
the recent implementation, a dedicated function `imposters.optimize()`
takes care of finding optimal parameters. The only dataset it needs is a
table with frequencies: please make sure that the authorial classes are
represented by \>1 texts (single texts are automatically excluded from
the analysis). Type the following code:

``` r
# activating another dataset, which contains Southern American novels:
data(lee)

# getting some more information about the dataset
help(lee)

# running the computationally-intense optimalization
imposters.optimize(lee)
```

Be prepared to wait… Since the above dataset is quite small, the results
should be ready in less than 10 minutes. In some other setups, however,
it might take many hours. You’ll probably find it a bit disappointing to
see just two numbers (the parameters *p1* and *p2*) as the final
results:

    ## [1] 0.43 0.55

These two single scores (note that your scores might differ a bit) give
us some knowledge of how to interpret the results obtained by the
`imposters()` function. Any values smaller than 0.43 and greater than
0.55 can be, with a high degree of confidence, translated into binary
answers of “no” and “yes”, respectively.

And what about the aforementioned Coben, with the value 0.34? Is it high
enough to claim that he penned “The Cuckoo’s Calling”? To answer this
question, you have to compute the *p1* and *p2* values for the dataset
`galbraith` yourself\!

## Parameters

In its current form, the function `imposters()` works with the Delta
method only. Next versions will provide SVM, NSC, kNN and NaiveBayes. As
most of you know very well, the general Delta framework can be combined
with many different distance measures. E.g. in their paper introducing
the imposters method (Kestemont et al., 2016b), the authors argue that
the Ruzicka metrics (aka Minmax) outperforms other measures. Similarly,
the Wurzburg guys (Evert et al., 2017) show that the Cosine Delta
metrics does really well when compared to other distances. It’s true
that my implementation of the `imposters()` invokes Classic Delta by
default, but other measures can be used as well. Try the following
options:

``` r
# activating the package 'stylo':
library(stylo)

# activating one of the datasets provided by the package 'stylo':
data(galbraith)

# Classic Delta distance
imposters(galbraith, distance = "delta")

# Cosine Delta (aka Wurzburg Distance)
imposters(galbraith, distance = "wurzburg")

# Ruzicka Distance (aka Minmax Distance)
# (please keep in mind that it takes AGES to compute it!)
imposters(galbraith, distance = "minmax")
```

Not really impressed, right? This is because the signal of JK Rowling is
really strong, and all the measures perform just fine. Let’s try
something more difficult. Did you know that “In Cold Blood” by Truman
Capote is stylometrically hard to associate with its actual author?
Execute the following code:

``` r
# activating the package 'stylo':
library(stylo)

# activating another dataset, which contains Southern American novels:
data(lee)

# defining the test text, i.e. "In Cold Blood"
my_text_to_be_tested = lee[1,]

# defining the comparison corpus
my_reference_set = lee[-c(1),]

# NOW, time to test 4 different distance measures:

# Classic Delta distance
imposters(my_reference_set, my_text_to_be_tested, distance = "delta")

# Eder's Delta distance
imposters(my_reference_set, my_text_to_be_tested, distance = "eder")

# Cosine Delta (aka Wurzburg Distance)
imposters(my_reference_set, my_text_to_be_tested, distance = "wurzburg")

# Ruzicka Distance (aka Minmax Distance)
# (please keep in mind that it takes AGES to compute it!)
imposters(my_reference_set, my_text_to_be_tested, distance = "minmax")
```

Have you noticed the reasonable improvement of Wurzburg Delta over the
other measures? It’s really cool\!

Other parameters of the function `imposters()` include:

  - `iterations` (default: 100) is a parameter defining the number of
    independent tests to be performed, provided that in each iteration a
    variety of randomly chosen features and/or imposters’ texts is being
    assessed.
  - `features` (default: 0.5) indicates the share of features
    (e.g. words) to be randomly picked in each iteration. If the
    feature vector has 500 most frequent words, and the `features`
    parameter is set to the value 0.1, then in each iteration a random
    subset of 10% of the words (i.e. 50) is selected.
  - `imposters` (default: 0.5) is very similar to the `features`, except
    that it indicates the proportion of imposters’ texts to be randomly
    assessed. The default value 0.5 means that in each iteration one
    half of the texts is picked by the algorithm.

Some other, more techical, parameters can be found in the manual page of
the function. Type `help(imposters)` for the details.

Certainly, the same applies to the `imposters.optimize()` function. The
same parameters that were introduced immediately above, can be passed to
the fine-tuning function, e.g.:

``` r
results = imposters(my_reference_set, distance = "wurzburg")

results1 = imposters(my_reference_set, distance = "wurzburg", imposters = 0.8)
```

Try all of them\!

## References


**Eder, M.** (2012). Computational stylistics and Biblical translation:
How reliable can a dendrogram be? In Piotrowski, T. and Grabowski, Ł.
(eds), *The Translator and the Computer*. Wrocław: WSF Press, pp. 155–70
<https://www.wsf.edu.pl/upload_module/wysiwyg/Wydawnictwo%20WSF/The%20Translator%20and%20the%20Computer_Piotrowski_Grabowski.pdf>.

**Eder, M., Rybicki, J. and Kestemont, M.** (2016). Stylometry with R: A
package for computational text analysis. *R Journal*, **8**(1): 107–21
<https://journal.r-project.org/archive/2016/RJ-2016-007/index.html>.

**Evert, S., Proisl, T., Jannidis, F., Reger, I., Pielström, S., Schöch,
C. and Vitt, T.** (2017). Understanding and explaining Delta measures
for authorship attribution. *Digital Scholarship in the Humanities*,
**32**(suppl. 2): 4–16
doi:[10.1093/llc/fqx023](https://doi.org/10.1093/llc/fqx023).
<http://dx.doi.org/10.1093/llc/fqx023>.

**Juola, P.** (2015). The Rowling case: A proposed standard protocol for
authorship attribution. *Digital Scholarship in the Humanities*,
**30**(suppl. 1): 100–13
doi:[10.1093/llc/fqv040](https://doi.org/10.1093/llc/fqv040).

**Kestemont, M., Stover, J., Koppel, M., Karsdorp, F. and Daelemans,
W.** (2016a). Authenticating the writings of Julius Caesar. *Expert
Systems with Applications*, **63**: 86–96.

**Kestemont, M., Stover, J., Koppel, M., Karsdorp, F. and Daelemans,
W.** (2016b). Authorship verification with the Ruzicka metric. In,
*Digital Humanities 2016: Conference Abstracts*. Kraków: Jagiellonian
University & Pedagogical University, pp. 246–49
<http://dh2016.adho.org/abstracts/402>.

**Koppel, M. and Winter, Y.** (2014). Determining if two documents are
written by the same author. *Journal of the Association for Information
Science and Technology*, **65**(1): 178–87
doi:[10.1002/asi.22954](https://doi.org/10.1002/asi.22954).
<http://dx.doi.org/10.1002/asi.22954>.

**Peñas, A. and Rodrigo, A.** (2011). A simple measure to assess
non-response. In, *Proceedings of the 49th Annual Meeting of the
Association for Computational Linguistics: Human Language Technologies*,
vol. 1. Portland, Oregon, pp. 1415–24.

**Stamatatos, E.** (2006). Authorship attribution based on feature set
subspacing ensembles. *International Journal on Artificial Intelligence
Tools*, **15**(05): 823–38
doi:[10.1142/S0218213006002965](https://doi.org/10.1142/S0218213006002965).
