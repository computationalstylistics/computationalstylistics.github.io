---
layout: page
title: Discours de la méthode
description: stylometric methodology
img: /assets/img/heatmap_LL_trimmed.png
---

The Computational Stylistics Group has always had an ambition to understand – on a deeper level – the methodological assumptions behind text-analysis techniques. Consequently, most of the studies conducted by the members of the Group are somewhat methodology-centric. Below, we present a selection of the studies that, as we believe, contribute to the state-of-the-art stylometric methodology. Two of these contributions, namely [Bootstrap Consensus Networks]({{ site.baseurl }}/projects/04_bootstrap_networks/) and [Rolling Stylometry]({{ site.baseurl }}/projects/05_rolling_stylometry/), are featured in separate posts.


## Sample size in stylometry

The aim of this study (Eder, 2015; cf. [pre-print](https://github.com/computationalstylistics/preprints/blob/master/Eder_Does_size_matter.pdf)) was to find such a minimal size of text samples for authorship attribution that would provide stable results independent of random noise. A few controlled tests for different sample lengths, languages and genres are discussed and compared. 

Although it seems tempting to perform a contrastive analysis of naturally long vs. naturally short texts (e.g. novels vs. short stories, essays vs. blog posts, etc.), to estimate the possible correlation between sample length and attribution accuracy, the results might be biased by inherent cross-genre differences between the two groups of texts. To remedy this limitation, in the present study the same dataset was used for all the comparisons: the goal was to extract shorter and longer virtual samples from the original corpus, using intensive re-sampling in a large number of iterations. The advantage of such a gradual increase of excerpted virtual samples is that it covers a wide range between “very short” and “very long” texts, and further enables one to capture a break point of the minimal sample size for a reliable attribution.

The research procedure was as follows. For each text in a given corpus, 500 randomly chosen single words were concatenated into a new sample. These new samples were analyzed using the classical Delta method; the percentage of successful attributions was regarded as a measure of effectiveness of the current sample length. The same steps of excerpting new samples from the original texts, followed by the stage of “guessing” the correct authors, were repeated for the length of 500, 600, 700, 800, ..., 20,000 words per sample.

<div>
    <img class="col two left" src="{{ site.baseurl }}/assets/img/sample_size_EN.png" alt="" title="Dependence of attribution accuracy and length of text samples: 63 English novels"/>
</div>
<div class="col two caption">
    Fig. 1. Dependence of attribution accuracy and length of text samples: 63 English novels (200 MFWs tested). Black circles indicate the ‘bags of words’ type of sampling, grey circles indicate excerpted passages.
</div>

The results for the corpus of 63 English novels are shown in Fig. 1. The observed scores (black circles on the graph; grey circles are discussed in the [full-length paper](https://github.com/computationalstylistics/preprints/blob/master/Eder_Does_size_matter.pdf)) clearly reveal a trend (solid line): the curve, climbing up very quickly, tends to stabilize at a certain point, which indicates the minimal sample size for the best attribution success rate. Although it is difficult to find the precise position of that point, it becomes quite obvious that **samples shorter than 5,000 words provide a poor “guessing”**, because they can be immensely affected by random noise. Below the size of 3,000 words, the obtained results are simply disastrous (more than 60% of false attributions for 1,000-word samples may serve as a convincing caveat). Other analyzed corpora showed quite similar shapes of the “learning curves”.

The above findings, however, have been (partially) falsified in a subsequent study (Eder, 2017; see [here](https://dh2017.adho.org/abstracts/341/341.pdf)). It turnes out that the minimal sample size varies considerably between different authors and different texts: sometimes as little as 1,500 words is enough to see the signal, and in other cases 20,000 words is still too little. A full-length paper is pending.





## Do we need the most frequent words?

The aim of this study (Rybicki and Eder, 2011; cf. [pre-print](https://github.com/computationalstylistics/preprints/blob/master/Rybicki%20Eder%20Deeper%20Delta%20LLC%20corrected%20and%20submitted.pdf)) was to examine the strength of the authorial signal in correlation with different vectors of frequent words. Contrary to usual approaches that investigate the performance of the very top of the list of the most frequent words, hundreds of possible combinations of word vectors were tested in this study, not solely starting with the most frequent word in each corpus.

Each analysis was first made with the top 50 most frequent words in the corpus; then the 50 most frequent words would be omitted and the next 50 words (i.e. words ranked 51 to 100 in the descending word frequency list) would be taken for analysis; then the next 50 most frequent words (those ranked 101 to 150), and so on until the required limit (usually the 5000th most frequent word) would be reached. Then the procedure would restart with the first 100 words (1-100), the second 100 words (101-100), and so on. At every subsequent restart, the number of the words omitted from the top of the frequency list would be increased by 50 until the length of this “moving window” descending down the word frequency list reached another limit (usually 5000).

<div class="img_row">
    <img class="col one left" src="{{ site.baseurl }}/assets/img/heatmap_EN.png" alt="" title="Attribution accuracy (percentage of correct attributions) for 65 English novels"/>
    <img class="col one left" src="{{ site.baseurl }}/assets/img/heatmap_LL.png" alt="" title="Attribution accuracy (percentage of correct attributions) for 94 Latin prose texts"/>
    <img class="col one left" src="{{ site.baseurl }}/assets/img/heatmap_PL.png" alt="" title="Attribution accuracy (percentage of correct attributions) for 69 Polish novels"/>
</div>
<div class="col three caption">
    Fig. 2. Attribution accuracy (percentage of correct attributions) for three corpora: 65 English novels (left), 94 Latin prose texts (center), and 69 Polish novels (right). Color coding is from low (blue) to high (brown). 
</div>

The English novel corpus (Fig. 2, left) was the one with the best attributions for all available vector sizes starting at the top of the reference corpus word frequency list; it was equally easy to attribute even if the first 2,000 most frequent words were omitted in the analysis – or even the first 3,000 for longer vectors. This was also the only corpus where a perfect attributive score (100%) was achieved almost constantly, which is reflected, in the graph, by the widespread and smooth dark colour in the heatmap.

For instance, the corpus of Latin prose texts (Fig. 2, right) could serve as excellent evidence for a minimalist approach in authorship attribution based on most frequent words, as the best (if not perfect) results were obtained by staying close to the axis intersection point: no more than 750 words, taken no further than from the 50<sup>th</sup> place on the frequency rank list. The top score, 75%, was in fact achieved only once – at 250 MFWs from the top of the list. Other corpora tested in this study are discussed in detail in the above-mentioned paper.



## Fake authorships

This study (Ochab, 2017) was conducted to test to which extent the authorial signal is hidden in the lexical level (i.e. the choice of words), and to which extent it is determined by grammatical structures.

<div class="col three caption">
    Fig. 3. ............................ 
</div>






## How to choose training samples?

This study (Eder and Rybicki, 2013; cf. [pre-print](https://github.com/computationalstylistics/preprints/blob/master/Eder-Rybicki_How_to_choose.pdf)) investigates the problem of appropriate choice of texts for the training set in machine-learning classification techniques. Intuition suggests composing the training set from the most typical texts (whatever “typical” means) by the authors studied (thus, for Goethe, _Werther_ rather than _Farbenlehre_; for Dickens, _Great Expectations_ rather than _A Tale of Two Cities_; for Sienkiewicz, his historical romances rather than his _Letters from America_). Certainly, the world of machine-learning knows the idea of _k_-fold cross-validation, or composing the training test iteratively (and randomly) in _k_ turns. No matter how useful this technique is, however, the question is still there: to which extent non-typical works might bias the results of an authorship attribution experiment?

The idea applied in this study was quite simple: a controlled experiment of 500 iterations of attributive tests was performed, each with random selection of the training and the test sets. The selections were made so that each author was always represented in the training set by a single (randomly-chosen) text, and that the test set always contained the same number of texts by each author. This was done to prevent a situation in which no works at all by one or more of the test authors would be found in the training set. Then the number of correct author guesses were compared, in the context of the hypothesis that the more resistant a corpus is to changes in the choice of the two sets, the more stable the results. The peak of the distribution curve would indicate the real effectiveness of the method, while its tails – the impact of random factors. A thin and tall peak would thus imply stable results resistant to changes in the training set.

<div class="img_row">
    <img class="col one left" src="{{ site.baseurl }}/assets/img/cv_EN.png" alt="" title="Density (vertical axis) of attributive success percentage rates (horizontal axis) in the corpus of English novels"/>
    <img class="col one left" src="{{ site.baseurl }}/assets/img/cv_IT.png" alt="" title="Density (vertical axis) of attributive success percentage rates (horizontal axis) in the corpus of Italian novels"/>
    <img class="col one left" src="{{ site.baseurl }}/assets/img/cv_PL.png" alt="" title="Density (vertical axis) of attributive success percentage rates (horizontal axis) in the corpus of Polish novels"/>
</div>
<div class="col three caption">
    Fig. 4. Density (vertical axis) of attributive success percentage rates (horizontal axis) in three corpora: English novels (left), Italian novels (center), Polish novels (right). 
</div>

As expected, the density of the 500 iterations for the corpus of 63 English novels follows a (skewed) bell curve (Fig. 4, left). At the same time, its gentler left slope suggests that, depending on the choice of the training set, the percentage of correct attributions can vary, with bad luck, to below 90%. The Italian corpus is a _quintessenza_ of consistency but, at this time, the most frequent accuracy rate has receded to below 85%, i.e. into regions rarely visited even by the worst combinations of training- and test-set texts in the English or even the French corpus. By contrast, the results for the Polish corpus are a true _katastrofa_: any attempt at broadening the corpus brings both accuracy and consistency below any standards acceptable. Other corpora tested in this study are discussed in detail in the above-mentioned paper.







## Bootstrapped Delta

The following study (Eder, 2013b; cf. [pre-print](https://github.com/computationalstylistics/preprints/blob/master/m-eder_bootstrapping_delta.pdf)) investigates the so-called “open-set” attribution problem: when an investigated anonymous text might have been written by any contemporary writer, and the attributor has no prior knowledge whether a sample written by a possible candidate is included in the reference corpus. A vast majority of methods used in stylometry establish a classification of samples and strive to find the _nearest neighbors_ among them. Unfortunately, these techniques of classification are not resistant to a common mis-classification error: any two nearest samples are claimed to be similar, no matter how distant they are.

The method presented here relies on the author’s empirical observation that the distance between samples similar to each other is quite stable despite different vectors of most frequent words tested, while the distance between heterogeneous samples often displays some unsteadiness depending on the number of MFWs analyzed. The core of the procedure is to perform a series of attribution tests in, say, 1,000 iterations, where the number of MFWs to be analyzed is chosen randomly (e.g., 334, 638, 72, 201, 904, 145, 134, 762, …); in each iteration, the nearest neighbor classification is performed. Next, the tables are arranged in a large three-dimensional table-of-tables. 

<div>
    <img class="col two left" src="{{ site.baseurl }}/assets/img/bootstrapped_delta_table.png" alt="" title="Distance distributions between texts, across 1,000 bootstrap iterations"/>
</div>
<div class="col two caption">
    Fig. 5. Distance distributions between texts, across 1,000 iterations with randomly chosen selections of frequent words.
</div>

The next stage is to estimate the distribution for each cell across 1,000 layers of the composite table. This is a crucial point of the whole procedure. While classical nearest neighbor classifications rely on _point estimation_ (i.e. the distance between two samples is always represented by a single numeric value), the new technique introduces the concept of _distribution estimation_, as shown in Fig. 5. Using some properties of these distributions, one can establish confidence intervals. Namely, the distance between two samples is a range of values represented by the mean of 1,000 bootstrap trials plus 1.64σ<sub>ij</sub> below and 1.64σ<sub>ij</sub> above the arithmetic mean of the distribution.

<div class="img_row">
    <img class="col one left" src="{{ site.baseurl }}/assets/img/bootstrapped_delta_1.png" alt="" title="Classic Delta procedure (500 MFWs tested) applied to assess the authorship of Phineas Finn"/>
    <img class="col one left" src="{{ site.baseurl }}/assets/img/bootstrapped_delta_2.png" alt="" title="Phineas Finn assessed using confidence intervals"/>
    <img class="col one left" src="{{ site.baseurl }}/assets/img/bootstrapped_delta_3.png" alt="" title="Ranking of candidates for The Portrait of Dorian Gray using confidence intervals"/>
</div>
<div class="col three caption">
    Fig. 6. Comparison of Delta distances with and without confidence intervals: classic Delta procedure (500 MFWs tested) applied to assess the authorship of <i>Phineas Finn</i> (left); the same novel assessed using confidence intervals (center); ranking of candidates for <i>The Portrait of Dorian Gray</i> using confidence intervals.
</div>

An exemplary ranking of candidates is shown in Fig. 6. The most likely author of _Phineas Finn_ is Trollope (as expected), and the calculated confidence interval does not overlap with any other range of uncertainty. The real strength of the method, however, is evidenced in the case of _The Portrait of Dorian Gray_, where the training set does not contain (intentionally) samples of Wilde. Classic Delta simply ranks the candidates, Hardy being the first, while in the new technique, confidence intervals of the first three candidates partially overlap with one another. Consequently, the assumed probability of authorship of Dorian Gray is shared between Galsworthy (54.2%), Hardy (34.8%) and Charlotte Brontë (11%). The ambiguous probabilities strongly indicate fake candidates in an open-set attribution case.





## Systematic errors in stylometry

This study (Eder, 2013a; cf. [pre-print](https://github.com/computationalstylistics/preprints/blob/master/m-eder_systematic_errors.pdf)) attempts to verify the impact of unwanted noise – e.g. caused by an untidily-prepared corpus – in a series of experiments conducted on several corpora of English, German, Polish, Ancient Greek and Latin prose texts. Since it is rather naive to believe that noise can be entirely neutralized, the actual question at stake is: what degree of nonchalance is acceptable to obtain sufficiently reliable results?

The nature of noise affecting stylometric results is quite complex. On the one hand, a machine-readable text might be contaminated by poor OCR, mismatched codepages, improperly removed XML tags; by including non-authorial textual additions, such as prefaces, footnotes, commentaries, disclaimers, etc. On the other hand, there are some types of unwanted noise that can by no means be referred to as systematic errors; they include scribal textual variants (_variae lectiones_), omissions (_lacunae_), interpolations, hidden plagiarism, editorial decisions for uniform spelling, modernizing the punctuation, and so on. Both types of noise, however, share a very characteristic feature. Namely, the longer the distance between the time when a given text was written and the moment of its digitization, the more opportunities of potential error to occur, for different reasons.

The first experiment was designed to simulate the impact of poor OCR. In 100 iterations, a given corpus was gradually damaged, and controlled tests for authorship were applied. In each of the 100 iterations, an increasing percentage of randomly chosen letters (excluding spaces) were replaced with other randomly chosen letters. E.g. in the 20<sup>th</sup> iteration, every letter of the input text was intended to be damaged with a probability of 20%; consequently, the corpus contained roughly 20% of independently damaged letters: “Mrs Lon**r** sa**a**s **k**h**a**t **t**etherfi**i**ld is tak**s**n by a y**s**ung man of l**s**r**c**e fo**o**tune” etc.

<div class="img_row">
    <img class="col one left" src="{{ site.baseurl }}/assets/img/damaged_english.png" alt="" title="Simulation of poor OCR quality in the corpus of English novels"/>
    <img class="col one left" src="{{ site.baseurl }}/assets/img/damaged_german.png" alt="" title="Simulation of poor OCR quality in the corpus of German novels"/>
    <img class="col one left" src="{{ site.baseurl }}/assets/img/damaged_polish.png" alt="" title="Simulation of poor OCR quality in the corpus of Polish novels"/>
</div>
<div class="img_row">
    <img class="col one left" src="{{ site.baseurl }}/assets/img/damaged_latin.png" alt="" title="Simulation of poor OCR quality in the corpus of Latin texts"/>
    <img class="col one left" src="{{ site.baseurl }}/assets/img/damaged_greek.png" alt="" title="Simulation of poor OCR quality in the corpus of Ancient Greek texts"/>
    <img class="col one left" src="{{ site.baseurl }}/assets/img/damaged_english_4-grams.png" alt="" title="Simulation of poor OCR quality in the corpus of English novels (character 4-grams)"/>
</div>
<div class="col three caption">
    Fig. 7. Simulation of poor OCR quality in a few corpora: in 100 iterations, increasing percentage of intentionally misspelled characters has been tested for 30 different MFW vectors. Color coding is indicated by the legend. In the upper row: English novels (left), German novels (center), Polish novels (right); in the bottom row: Latin prose (left), Ancient Greek prose (center), English novels but this time character 4-grams were used instead of words (right). 
</div>

The results were quite similar for most of the corpora tested. As shown in Fig. 7, short vectors of MFWs (up to 500 words) usually provide no significant decrease of performance despite a considerably large amount of noise added (the corpus of Polish novels being an exception). Even 20% of damaged letters would not affect the results in some cases! However, longer MFW vectors are _very sensitive_ to misspelled characters: any additional noise means a steep decrease of performance. This means that the “garbage in, gospel out” optimism is in fact illusory.

Character-based markers, however, revealed an impressive increase of performance, regardless of the classification method used. As evidenced in Fig. 7 (bottom-right, for character 4-grams), the threshold where the noise finally starts to overwhelm the attributive scores is settled somewhere around the point of 40% distorted characters. It is hard to believe how robust this type of style-marker is when confronted with a dirty corpus – to kill the authorial signal efficiently, one needs to distort more than 60% of original characters (!).

A detailed comparison of different corpora, classifiers and feature types, as well as an alternative experiment aimed at measuring the impact of intertextuality, is provided by the above-mentioned full-length paper. 




## References


**Eder, M.** (2013a). [Mind your corpus: systematic errors in authorship attribution](http://llc.oxfordjournals.org/content/28/4/603). _Literary and Linguistic Computing_, **28**(4): 603-14, [[pre-print](https://github.com/computationalstylistics/preprints/blob/master/m-eder_systematic_errors.pdf)].

**Eder, M.** (2013b). Bootstrapping Delta: a safety-net in open-set authorship attribution. _Digital Humanities 2013: Conference Abstracts_. Lincoln: University of Nebraska-Lincoln, pp. 169-72, [http://dh2013.unl.edu/abstracts/index.html](http://dh2013.unl.edu/abstracts/index.html), [[pre-print](https://github.com/computationalstylistics/preprints/blob/master/m-eder_bootstrapping_delta.pdf)].

**Eder, M.** (2015). [Does size matter? Authorship attribution, small samples, big problem](https://academic.oup.com/dsh/article/30/2/167/390738). _Digital Scholarship in the Humanities_, **30**(2): 167-182, [[pre-print](https://github.com/computationalstylistics/preprints/blob/master/Eder_Does_size_matter.pdf)].

**Eder, M.** (2017). Short samples in authorship attribution: A new approach. _Digital Humanities 2017: Conference Abstracts_. Montreal: McGill University, pp. 221–24, [https://dh2017.adho.org/abstracts/341/341.pdf](https://dh2017.adho.org/abstracts/341/341.pdf).

**Eder, M. and Rybicki, J.** (2013). [Do birds of a feather really flock together, or how to choose training samples for authorship attribution](http://llc.oxfordjournals.org/content/28/2/229). _Literary and Linguistic Computing_, **28**(2): 229-36, [[pre-print](https://github.com/computationalstylistics/preprints/blob/master/Eder-Rybicki_How_to_choose.pdf)].

**Ochab, J. K.** (2017). Stylometric networks and fake authorships. _Leonardo_, **50**(5): 502, [doi:10.1162/LEON_a_01279](http://dx.doi.org/10.1162/LEON_a_01279).

**Rybicki, J. and Eder, M.** (2011). [Deeper Delta across genres and languages: do we really need the most frequent words?](https://academic.oup.com/dsh/article/26/3/315/1149353) _Literary and Linguistic Computing_, **26**(3): 315-21, [[pre-print](https://github.com/computationalstylistics/preprints/blob/master/Rybicki%20Eder%20Deeper%20Delta%20LLC%20corrected%20and%20submitted.pdf)].


