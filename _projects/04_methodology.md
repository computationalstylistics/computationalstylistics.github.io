---
layout: page
title: Discours de la méthode
description: stylometric methodology
img: /assets/img/English_poetry_trimmed.png
---

The Computational Stylistics Group has always had an ambition to understand – on a deeper level – the methodological assumptions behind text-analysis techniques. Consequently, most of the studies conducted by the members of the Group are somewhat methodology-centric. Below, we present a selection of the studies that, as we believe, contribute to the state-of-the-art stylometric methodology. Two of these contributions, namely [Bootstrap Consensus Networks](https://computationalstylistics.github.io/projects/06_bootstrap_networks/) and [Rolling Stylometry](https://computationalstylistics.github.io/projects/05_rolling_stylometry/), are featured in separate posts.


## Sample size in stylometry


<div>
    <img class="col two left" src="{{ site.baseurl }}/assets/img/sample_size_EN.png" alt="" title="example image"/>
</div>
<div class="col two caption">
    Fig. 1. Dependence of attribution accuracy and length of text samples: 63 English novels (200 MFWs tested). Black circles indicate the ‘bags of words’ type of sampling, grey circles indicate excerpted passages.
</div>




**Eder, M.** (2015). [Does size matter? Authorship attribution, small samples, big problem](https://academic.oup.com/dsh/article/30/2/167/390738). _Digital Scholarship in the Humanities_, **30**(2): 167-182, [[pre-print](https://github.com/computationalstylistics/preprints/blob/master/Eder_Does_size_matter.pdf)].

**Eder, M.** (2017). Short samples in authorship attribution: A new approach. _Digital Humanities 2017: Conference Abstracts_. Montreal: McGill University, pp. 221–24, [https://dh2017.adho.org/abstracts/341/341.pdf](https://dh2017.adho.org/abstracts/341/341.pdf).



## Do we need the most frequent words?


<div class="img_row">
    <img class="col one left" src="{{ site.baseurl }}/assets/img/heatmap_EN.png" alt="" title="example image"/>
    <img class="col one left" src="{{ site.baseurl }}/assets/img/heatmap_LL.png" alt="" title="example image"/>
    <img class="col one left" src="{{ site.baseurl }}/assets/img/heatmap_PL.png" alt="" title="example image"/>
</div>
<div class="col three caption">
    Fig. 2. Attribution accuracy (percentage of correct attributions) for three corpora: 65 English novels (left), 94 Latin prose texts (center), and 69 Polish novels (right). Color coding is from low (blue) to high (brown). 
</div>


**Rybicki, J. and Eder, M.** (2011). [Deeper Delta across genres and languages: do we really need the most frequent words?](https://academic.oup.com/dsh/article/26/3/315/1149353) _Literary and Linguistic Computing_, **26**(3): 315-21, [[pre-print](https://github.com/computationalstylistics/preprints/blob/master/Rybicki%20Eder%20Deeper%20Delta%20LLC%20corrected%20and%20submitted.pdf)].


## Fake authorships



<div class="col three caption">
    Fig. 3. ............................ 
</div>


**Ochab, J. K.** (2017). Stylometric networks and fake authorships. _Leonardo_, **50**(5): 502, [doi:10.1162/LEON_a_01279](http://dx.doi.org/10.1162/LEON_a_01279).




## How to choose training samples?


<div class="img_row">
    <img class="col one left" src="{{ site.baseurl }}/assets/img/cv_EN.png" alt="" title="example image"/>
    <img class="col one left" src="{{ site.baseurl }}/assets/img/cv_IT.png" alt="" title="example image"/>
    <img class="col one left" src="{{ site.baseurl }}/assets/img/cv_PL.png" alt="" title="example image"/>
</div>
<div class="col three caption">
    Fig. 4. ............................ 
</div>


**Eder, M. and Rybicki, J.** (2013). [Do birds of a feather really flock together, or how to choose training samples for authorship attribution](http://llc.oxfordjournals.org/content/28/2/229). _Literary and Linguistic Computing_, **28**(2): 229-36, [[pre-print](https://github.com/computationalstylistics/preprints/blob/master/Eder-Rybicki_How_to_choose.pdf)].



## Bootstrapped Delta



<div>
    <img class="col two left" src="{{ site.baseurl }}/assets/img/bootstrapped_delta_table.png" alt="" title="example image"/>
</div>
<div class="col two caption">
    Fig. 5. ............................
</div>


<div class="img_row">
    <img class="col one left" src="{{ site.baseurl }}/assets/img/bootstrapped_delta_1.png" alt="" title="example image"/>
    <img class="col one left" src="{{ site.baseurl }}/assets/img/bootstrapped_delta_2.png" alt="" title="example image"/>
    <img class="col one left" src="{{ site.baseurl }}/assets/img/bootstrapped_delta_3.png" alt="" title="example image"/>
</div>
<div class="col three caption">
    Fig. 6. ............................ 
</div>



**Eder, M.** (2013b). Bootstrapping Delta: a safety-net in open-set authorship attribution. _Digital Humanities 2013: Conference Abstracts_. Lincoln: University of Nebraska-Lincoln, pp. 169-72, [http://dh2013.unl.edu/abstracts](http://dh2013.unl.edu/abstracts), [[pre-print](https://github.com/computationalstylistics/preprints/blob/master/m-eder_bootstrapping_delta.pdf)].



## Systematic errors in stylometry


<div class="img_row">
    <img class="col one left" src="{{ site.baseurl }}/assets/img/damaged_english.png" alt="" title="example image"/>
    <img class="col one left" src="{{ site.baseurl }}/assets/img/damaged_german.png" alt="" title="example image"/>
    <img class="col one left" src="{{ site.baseurl }}/assets/img/damaged_polish.png" alt="" title="example image"/>
</div>
<div class="img_row">
    <img class="col one left" src="{{ site.baseurl }}/assets/img/damaged_latin.png" alt="" title="example image"/>
    <img class="col one left" src="{{ site.baseurl }}/assets/img/damaged_greek.png" alt="" title="example image"/>
    <img class="col one left" src="{{ site.baseurl }}/assets/img/damaged_english_4-grams.png" alt="" title="example image"/>
</div>
<div class="col three caption">
    Fig. 7. ........................... 
</div>