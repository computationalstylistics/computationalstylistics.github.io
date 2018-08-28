---
layout: page
title: Rolling Stylometry
description: a method of inspecting text fragments
permalink: /projects/rolling-stylometry/
img: /assets/img/rolling-svm_100-features_5000-per-slice.png
---



<div>
    <img class="col three left" src="{{ site.baseurl }}/assets/img/rolling-svm_100-features_5000-per-slice.png" alt="" title="Roman de la Rose assessed using Rolling Stylometry"/>
</div>
<div class="col three caption">
    Fig. 1. <i>Roman de la Rose</i> examined using Rolling Stylometry (in SVM flavor), with the following parameters: 100 MFWs, window size of 5,000 words, sample overlap of 4,500 words.
</div>


## Abstract

This little project started from the following thought experiment: while most state-of-the-art stylometric approaches aim at broadening the scope of the analysis according to the “distant reading” paradigm, do we really understand what a single text is? In other words, the question here was: what about applying a microscope perspective rather than the usual large-scale analysis approach? This thinking led to introducing **a new method**, supported with compact visualization, that tries to look inside a text, represented as a set of linearly sliced chunks, in order to test their stylistic consistency. Since it is based on the idea of moving slowly through a text to be stylometrized, it has been named **Rolling Stylometry**.

The following description is but an appetizer. A quick start, supplemented by applicable/reusable snippets of code, can be found in [this blog post]({{ site.baseurl }}/blog/rolling_stylometry/). For a detailed explanation of the method’s theoretical assumptions, features, and implementation refer to the following paper:

> Eder, M. (2016). [Rolling stylometry](https://academic.oup.com/dsh/article/31/3/457/1745764). _Digital Scholarship in the Humanities_, 31(3): 457-469, [[pre-print](https://github.com/computationalstylistics/preprints/blob/master/Eder_Rolling_stylometry_draft.pdf)].


## Motivation

Sequential analysis is a very attractive way of studying linear phenomena. The concept of the moving window is particularly important for measuring given elements in their sequential order. It has been introduced to stylometry and extended by van Dalen-Oskam and van Zundert in their study on the medieval Dutch poem titled _Roman van Walewein_ (van Dalen-Oskam and van Zundert, 2007). Other notable approaches to visualize stylistic shifts using moving windows include papers on Middle Dutch rhyme words (Kestemont, 2010), on three disputed English prose texts (Burrows, 2010), and on _The Tutor’s Story_ by Kingsley and Mallet approached with t-tests (Hoover, 2011). Recently, Rolling Delta has been applied to examine collaborative works by Joseph Conrad and Ford Madox Ford (Rybicki et al., 2014).

The Rolling Stylometry method is based on the above approaches. Its general idea is very simple: a text to be analyzed (e.g., an anonymous text to be attributed) is chunked into equal-sized blocks (partially overlapping). Then, instead of attributing the text in its entirety, the goal is to perform an independent similarity test for each chunk, and to inspect the results as a sequence of ordered stylistic signals. Arguably, any classification method can be combined with this procedure. However, so far, the method implementation in _stylo_ includes support vector machines (SVM), nearest shrunken centroids (NSC), and Delta in its classical Burrowsian flavor (Eder, 2015).

## An example

The method is designed to detect stylistic takeovers. One example is _The World’s Desire_, a classic fantasy novel written collaboratively by Henry Rider Haggard and Andrew Lang in 1890. It is a story of the hero Odysseus, who returns home to Ithaca from his journey: however, instead of finding his home at peace, he is involved in several new adventures. The plot of the novel, as well as its mythological background, was set by Lang, while Haggard – the author of several appreciated adventure novels – contributed his imagination and style. It is assumed that Haggard reworked Lang’s drafts and actually wrote most of the novel except the first four chapters, which were written entirely by Lang.

<div>
    <img class="col three left" src="{{ site.baseurl }}/assets/img/rolling-svm_haggard_100.png" alt="" title="Sequential analysis of The World’s Desire by Haggard and Lang"/>
</div>
<div class="col three caption">
    Fig. 2. Sequential analysis of _The World’s Desire_ by Haggard and Lang: Rolling SVM and 100 MFWs.
</div>

A simple experiment involving a reference corpus of eight novels by Haggard and eight by Lang corroborates the hypothesis. Fig. 2 shows the results of the Rolling Classify technique applied to _The World’s Desire_ using 100 MFWs. You can easily observe a stylistic takeover in the first part of the text. The break point takes place in the middle of the sixth chapter. Also, some sections in the central part of the novel appear to be Lang's. However, these apparent Lang’s sectors evaporate when a different MFW strata is used for the test. 

<div>
    <img class="col three left" src="{{ site.baseurl }}/assets/img/rolling-svm_haggard_1000.png" alt="" title="Sequential analysis of The World’s Desire by Haggard and Lang"/>
</div>
<div class="col three caption">
    Fig. 3. Sequential analysis of <i>The World’s Desire</i> by Haggard and Lang: Rolling SVM and 1000 MFWs.
</div>

For 500 MFWs, Haggard’s signal shows up for a short moment in the first chapters of the novel. When 1000 MFWs are taken into consideration (Fig. 3), the distinction between two authorial voices in the sixth chapter is the only takeover that can be observed.


## Appications

The method has been successfully applied in a number of studies by the members of the Group. Probably the most spectacular is [a short study on Harper Lee]({{ site.baseurl }}/blog/harper-lee/) that has been featured in the [Wall Street Journal](https://www.wsj.com/articles/data-miners-dig-into-go-set-a-watchman-1437096631), and then evolved into a regular [research project]({{ site.baseurl }}/projects/harper-lee/). Another example is a study on Elena Ferrante as a “virtual author”, having a different voice from the actual person behind the pseudonym (Eder, 2018).




## References

**Burrows, J.** (2010). Never say always again: Reflections on the numbers game. In McCarty, W. (ed.), _Text and Genre in Reconstruction: Effects of Digitalization on Ideas, Behaviors, Products and Institutions_. Cambridge: Open Book Publishers, pp. 13–36.

**Eder, M.** (2015). Through the magnifying glass: rolling stylometry for collaborative authorship. In: _Digital Humanities 2015: Book of Abstracts_, University of Western Sydney, [http://dh2015.org/abstracts](http://dh2015.org/abstracts), [[the poster itself](https://github.com/computationalstylistics/preprints/blob/master/poster_DH2015.pdf)].

**Eder, M.** (2016). [Rolling stylometry](https://academic.oup.com/dsh/article/31/3/457/1745764). _Digital Scholarship in the Humanities_, **31**(3): 457-469, [[pre-print](https://github.com/computationalstylistics/preprints/blob/master/Eder_Rolling_stylometry_draft.pdf)].

**Eder, M.** (2018). Elena Ferrante: a virtual author. In Tuzzi, A. and Cortelazzo, M. A. (eds), _Drawing Elena Ferrante’s Profile_. Padova: Padova University Press, pp. 31–45, [http://www.padovauniversitypress.it/publications/9788869381300](http://www.padovauniversitypress.it/publications/9788869381300).

**Hoover, D. L.** (2011). ‘The Tutor’s Story’: A Case Study of Mixed Authorship. In _Digital Humanities: Conference Abstracts_, Stanford, CA, pp. 149–51.

**Kestemont, M.** (2010). Velthem et al.: A Stylometric Analysis of the Rhyme Words in the Account of the Battle of the Golden Spurs in the Fifth part of the Spiegel Historiael. _Queeste_, **17**: 1–34.

**Rybicki, J., Kestemont, M. and Hoover D.** (2014). Collaborative Authorship: Conrad, Ford, and Rolling Delta. _Literary and Linguistic Computing_, **29**(3): 422–31.

**van Dalen-Oskam, K. and van Zundert, J.** (2007). Delta for Middle Dutch: Author and Copyist Distinction in Walewein. _Literary and Linguistic Computing_, **22**: 345–62.

