Authorship verification with the package `stylo`
================
Maciej Eder
27/05/2018

## Introduction

This post introduces to a new feature of the package `stylo` (ver.
0.6.7), namely the General Imposters (GI) method, also referred to as
the second verification system (o2), introduced by Koppel and Winter
(2014) and applied to the study of Julius Caesar’s disputed writings
(Kestemont, Stover, Koppel, Karsdorp, & Daelemans, 2016a). To quote the
authors, “\[t\]he general intuition behind the GI, is not to assess
whether two documents are simply similar in writing style, given a
static feature vocabulary, but rather, it aims to assess whether two
documents are significantly more similar to one another than other
documents, across a variety of stochastically impaired feature spaces
(Eder, 2012; Stamatatos, 2006), and com- pared to random selections of
so-called distractor authors (Juola, 2015), also called ‘imposters’.”
(Kestemont et al., 2016a, p. 88).

The implementation provided by the package `stylo` is a rather faithful
interpretation of two algorithms described in a study on authorship
verification (Kestemont, Stover, Koppel, Karsdorp, & Daelemans, 2016b).
A tiny function for computing the score `c@1` used to evaluate the
system is directly transplanted from the original implementation
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
install.pacgages("stylo")
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

    ## coben     0.3

    ## lewis     0

    ## rowling   1

    ## tolkien   0

    ##   coben   lewis rowling tolkien 
    ##     0.3     0.0     1.0     0.0

The interpretation of the results is rather straightforward: “The
Cuckoo’s Calling” was not written by CS Lewis, nor was it penned by
JRR Tolkien. Similarly, the score for JK Rowling turned out to be very
high (could not be higher), which clearly suggests the author of the
analyzed novel. The only class that is difficult to interpret is Harlan
Coben, since he was assigned 0.29. The score obviously falls into the
\<0.5 category, but still: can we reliably say that this candidate
should be rulled out or, rather, should we abstain from any conclusions
here? The problem of defining the grey area around the score 0.5 will be
discussed below.

## Details

As you might have noticed, the dataset `galbraith` contains frequencies
for different texts by a few authors, the class *GALBRAITH* being
represented by a single text, though. Having no additional parameters,
the function tries to identify such a single text and then assumes that
this is the anonymous sample to be assessed.

In a vast majority of cases, however, one would like to have some
control on choosing the text to be contrasted against the corpus. The
function provides a dedicated parameter `test` to do the trick. Note the
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

Consequently, if you want to test who wrote “The Lord of the Rings”,
part 1, get the 24th row from the table:

``` r
my_text_to_be_tested = galbraith[24,]
my_frequency_table = galbraith[-c(24),]
imposters(reference.set = my_frequency_table, test = my_text_to_be_tested)
```

So far, I’ve been neglecting one important feature of the imposters
method. As Kestemont et al. (2016b) show in their “Algorithm 1”, the
method tries to compare an anonymous text against (1) a candidate set,
containing the works of a probable candidate author, and (2) the
imposters set, containing lots of text by people who could not have
written the text in question. In the previous examples, where no
canditate set was explicitly indicated, the method repeatedly tested all
of possible authors as potential candidates (one at a time). It is a
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
task. This will serve as an additional cross-validation step, because I
will be able to check if all the remaining candidates will be assigned
zeros (as expected). In other words, I’d rather compare the behavior of
JK Rowling in comparison to all possible candidate authors, even if
Rowling is the only class I believe would get a reasonable score.

## Loading a corpus from files

I am fully aware that the function `imposters()` in its current form
requires some advanced knowledge of R, since it does not provide any
corpus pre-processing (as the main functions of the package `stylo` do).
Specifically, one needs to know in advance how to produce a table of
frequencies. This step has been already described elsewhere (Eder,
Rybicki, & Kestemont, 2016, pp. 109–111), therefore I will not go into
nuanced details here. A straightforward way to get from raw text files
to the imposters results might look as follows:

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

## Optimizing the decision scores

Score shifting algorighm

    imposters.optimize()

Be prepared to wait…

## Parameters

In its current form, the function `imposters()` works with the Delta
method only. Next versions will provide SVM, NSC, kNN and NaiveBayes. As
most of you know very well, the general Delta framework can be combined
with many different distance measures. E.g. in their paper introducing
the imposters method (Kestemont et al., 2016b), the authors argue that
the Ruzicka metrics (aka Minmax) outperforms other measures. Similarly,
the Wurzburg guys (Evert et al., 2017) show that Cosine Delta rocks when
compared to other distances. My implementation of the `imposters()`
applies Classic Delta by default, but other measures can be used as
well. Try the following options:

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

Have you noticed the amazing improvement of Wurzburg Delta over the
other measures? It’s really cool\!

Certainly, the same applied to the `imposters.optimize()` function. The
same parameters that were introduced immediately above, can be passed to
the fine-tuning function, e.g.:

``` r
results = imposters(my_reference_set, distance = "wurzburg")
```

## References

<div id="refs" class="references">

<div id="ref-eder_computational_2012">

Eder, M. (2012). Computational stylistics and Biblical translation: How
reliable can a dendrogram be? In T. Piotrowski & Ł. Grabowski (Eds.),
*The translator and the computer* (pp. 155–170). Wrocław: WSF Press.
Retrieved from
<https://www.wsf.edu.pl/upload_module/wysiwyg/Wydawnictwo%20WSF/The%20Translator%20and%20the%20Computer_Piotrowski_Grabowski.pdf>

</div>

<div id="ref-eder_stylometry_2016">

Eder, M., Rybicki, J., & Kestemont, M. (2016). Stylometry with R: A
package for computational text analysis. *R Journal*, *8*(1), 107–121.
Retrieved from
<https://journal.r-project.org/archive/2016/RJ-2016-007/index.html>

</div>

<div id="ref-evert_understanding_2017">

Evert, S., Proisl, T., Jannidis, F., Reger, I., Pielström, S., Schöch,
C., & Vitt, T. (2017). Understanding and explaining Delta measures for
authorship attribution. *Digital Scholarship in the Humanities*,
*32*(suppl. 2), 4–16. <https://doi.org/10.1093/llc/fqx023>

</div>

<div id="ref-juola_rowling_2015">

Juola, P. (2015). The Rowling case: A proposed standard protocol for
authorship attribution. *Digital Scholarship in the Humanities*,
*30*(suppl. 1), 100–113. <https://doi.org/10.1093/llc/fqv040>

</div>

<div id="ref-kestemont_authenticating_2016">

Kestemont, M., Stover, J., Koppel, M., Karsdorp, F., & Daelemans, W.
(2016a). Authenticating the writings of Julius Caesar. *Expert Systems
with Applications*, *63*, 86–96.

</div>

<div id="ref-kestemont_authorship_2016">

Kestemont, M., Stover, J., Koppel, M., Karsdorp, F., & Daelemans, W.
(2016b). Authorship verification with the Ruzicka metric. In *Digital
Humanities 2016: Conference Abstracts* (pp. 246–249). Kraków:
Jagiellonian University & Pedagogical University. Retrieved from
<http://dh2016.adho.org/abstracts/402>

</div>

<div id="ref-koppel_determining_2014">

Koppel, M., & Winter, Y. (2014). Determining if two documents are
written by the same author. *Journal of the Association for Information
Science and Technology*, *65*(1), 178–187.
<https://doi.org/10.1002/asi.22954>

</div>

<div id="ref-stamatatos_authorship_2006">

Stamatatos, E. (2006). Authorship attribution based on feature set
subspacing ensembles. *International Journal on Artificial Intelligence
Tools*, *15*(05), 823–838. <https://doi.org/10.1142/S0218213006002965>

</div>

</div>
