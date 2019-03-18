---
layout: post
title: Custom distance measures
author: Maciej Eder
date:   2015-08-27 16:40:16
#description: Custom distance measures
---





Distance measures in stylometry… This is definitely the topic one never
gets bored with. I’ve been promising myself to write a longer piece on
this one day: not this time, though. In this short post, I’m going to
introduce a functionality of the R package `stylo` (ver. \>= 0.6.0) that
allows for testing *any* distance.

Apart from the already-implemented distance measures (most of them can
be conveniently selected via GUI), the package `stylo` features a socket
for plugging in your own custom distances. In short, a bit of coding
combined with some expertise in maths – that’s basically all we need. We
have to design a function which takes a table with frequencies as an
input parameter, and returns a square table of distances: it can be
either an object of the generic class `dist` (the lower triangle of the
distance matrix stored by columns in a vector), or a regular full
matrix, symmetric across the diagonal. Whatever.

Suppose you want to test the distance discussed in a great paper by
Jannidis, Schoch, Pielstrom & Vitt (Jannidis et al., 2015) presented at
DH2015. This is a regular Cosine Distance applied to z-scored data.
Interestingly enough, this measure has been (sort of) introduced in an
earlier study (Smith and Aldridge, 2011), but never tested before the
Würzburg guys took over. First, we prepare a custom function (this is a
simple version: a real function should check if the input dataset can be
further processed, if it is a matrix, etc.). Type the following code:

``` r
my.cosine.distance = function(x){
    
    # z-scoring the input matrix of frequencies
    x = scale(x)
    
    # computing cosine dissimilarity
    y = as.dist( x %*% t(x) / (sqrt(rowSums(x^2) %*% t(rowSums(x^2)))) ) 
    
    # then, turning it into cosine similarity
    z = 1 - y
    
    # getting the results
    return(z)
}
```

Once the above code is copy-pasted to the R console, it becomes a new
function named `my.cosine.distance()`, and it becomes visible for other
R objects. The function, however, is not persistent: the paste-copying
step has to be repeated every time a new R session launched.

Having completed the above step, we’re all set. Now, one can use the
tailored distance function with any of the main functions of the package
`stylo`. Note the following examples:

``` r
stylo(distance.measure = "my.cosine.distance")

classify(distance.measure = "my.cosine.distance")

rolling.classify(distance.measure = "my.cosine.distance")
```

The Cosine Delta (aka Würzburg Delta) is but one example of replacing
the original kernel of the Delta method with a custom distance. What
about trying something else? Assume that you plan to test if the Entropy
Distance outperforms other similarity measures. It has been reported in
the literature (Juola and Baayen, 2005) that entropy-based distances are
generally accurate in stylometry. Let’s define a tailored function:

``` r
dist.entropy = function(x) {
    A = t(t(x + 1) / colSums(x + 1))
    B = t(t(log(x + 2)) / -(colSums(A * log(A))))
    y = dist(B, method="manhattan")
    return(y)
}
```

The next step is rather obvious, given the already-discussed examples:

``` r
stylo(distance.measure = "dist.entropy")
```

Now, what about an inverse correlation distance? It has been
successfully applied in a cross-language benchmark study distances in
stylometry (Forsyth and Sharoff, 2014), in which, by the way, a few
other interesting measures have been tested. The following code was
contributed by Richard Forsyth:

``` r
##  Additional distance function for Stylo() :
##  submitted by R.S. Forsyth.
##  First version : 30/10/2013
##  Last revision : 30/10/2013

cordist = function (freqvec,cols=89,usemeth="spearman") {
    ##  takes 2D vector of word frex [,1:cols] (table.with.all.freqs);
    ##  returns a distance matrx 2b used in clustering or MDS.
    ##  Distance index is inverse correlation (Rank.Corr default).

    if (cols < 2)  stop("Too few cols!!")
    ##  table.with.all.freqs usually has too many cols;
    ##  don't know where correct number to be used is saved;
    ##  therefore currently needed as function argument.
    tranfrex = t(freqvec[,1:cols])  ##  columns are features (words/grams)
    dmat = 1-cor(tranfrex,meth=usemeth)
    ##  meth cd also be "kendall" or "pearson" (not recommended).

    return  (as.dist(dmat))
    ##  names seem to stay attached, as attr(*,"Labels").

}  ##  ready for hclust() or sammon() scaling.
```

Etc. etc. etc. It is claimed that over 5,000 distance measures have been
introduced so far in exact sciences (Moisl, 2014). Try them all\!





## References


**Forsyth, R. and Sharoff, S.** (2014). Document dissimilarity within
and across languages: A benchmarking study. *Literary and Linguistic
Computing*, **29**(1): 6–22
doi:[10.1093/llc/fqt002](https://doi.org/10.1093/llc/fqt002) (accessed
31 May 2018).

**Jannidis, F., Pielström, S., Schöch, C. and Vitt, T.** (2015).
Improving Burrows’ Delta – An empirical evaluation of text distance
measures. In, *Digital Humanities 2015: Conference Abstracts*. Sydney,
Australia: University of Western Sydney <http://dh2015.org/abstracts>.

**Juola, P. and Baayen, H.** (2005). A controlled-corpus experiment in
authorship attribution by cross-entropy. *Literary and Linguistic
Computing*, **20**(1): 59–67.

**Moisl, H.** (2014). *Cluster Analysis for Corpus Linguistics*. Berlin:
Mouton de Gruyter.

**Smith, P. W. H. and Aldridge, W.** (2011). Improving authorship
attribution: Optimizing Burrows’ Delta method. *Journal of Quantitative
Linguistics*, **18**(1): 63–88
doi:[10.1080/09296174.2011.533591](https://doi.org/10.1080/09296174.2011.533591)
(accessed 22 April 2018).


