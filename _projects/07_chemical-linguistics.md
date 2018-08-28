---
layout: page
title: Chemical Linguistics
description: between linguistics and organic chemistry
permalink: /projects/chemical-linguistics
img: /assets/img/topic-54.png
---


This 5-year project entitled “Development of Computational Chemical Linguistics and its Applications to the Efficient Planning of Multistep Chemical Syntheses” and founded by the [National Science Centre](https://ncn.gov.pl/?language=en) (SYMFONIA 2014/12/W/ST5/00592), is a joint initiative of three research teams, based at the Institute of Organic Chemistry (Polish Academy of Sciences), the Institute of Mathematics (University of Warsaw) and at the Institute of Polish Language (Polish Academy of Sciences), representing three different disciplines: chemistry, computer science, and linguistics. 

The project’s PI is prof. Bartosz Grzybowski from the Institute of Organic Chemistry (Polish Academy of Sciences) and the Ulsan National Institute of Science and Technology. The linguistic team has been represented by the following scholars:

* Maciej Eder (head of the linguistic team)
* Rafał L. Górski
* Jan Winkowski
* Michał Woźniak
* Urszula Modrzyk

The project addresses one of the greatest and outstanding challenges of modern chemistry – namely, the use of computers to design optimal, multistep chemical pathways leading to lifesaving drugs, pigments or dyes, complex natural products, and many more. Our proposal unites the efforts of Poland’s best chemists, computer scientists and linguists to challenge this prevailing view of chemistry and demonstrate – both in silico and through experimental validation – that by uniting the tools of computational linguistics (or corpus linguistics), data mining, machine learning, and algorithm theory, it is possible to teach computers chemistry to the level of top-notch organic chemists and then use these computers to plan complex synthetic transformations.




<div>
    <img class="col two left" src="{{ site.baseurl }}/assets/img/41598_2018_25440_Fig1_HTML.jpg" alt="" title="Chemical words and vocabularies"/>
</div>
<div class="col two caption">
    Fig. 1. Chemical words and vocabularies. (a) A common maximal substructure, MCS (colored red), between two molecules. (b) Language laws in MSC “words” for the entire 1.75-million-rich chemical vocabulary, compared with the works by Conan Doyle, Shakespeare, and Joyce’s <i>Finnegans Wake</i>. (c) Examples of chemical words – frequent “function” versus unfrequent “content” words (from left to right: penicillins, coumarins, carbohydrates, steroids).
</div>




## Chemical “keywords”? 

Interested in identifying molecule fragments that are “meaningful”? Want to see how keyword extraction works outside the text analysis world? This paper describes how such corpus-linguistic concepts can be extended to chemistry based on characteristic “chemical words” that span more than traditional functional groups and, instead, look at common structural fragments molecules share. Using these words, it is possible to quantify the diversity of chemical collections/databases in new ways and to define molecular “keywords” by which such collections are best characterized and annotated:

**Woźniak, M., Wołos, A., Modrzyk, U., Górski, R. L., Winkowski, J., Bajczyk, M., Szymkuć, S., Grzybowski, B. and Eder, M.** (2018). [Linguistic measures of chemical diversity and the ‘keywords’ of molecular collections](http://www.nature.com/articles/s41598-018-25440-6). _Scientific Reports_, **8**(1), 7598.


## “Words” in chemical molecules

If we name the “meaningful” groups of atoms as “words”, we need a device
for finding them in our corpus since there are no explicit word boundaries. In the approach presented in this study, we adopt a method for establishing word boundaries in Chinese. The method uses the concept of sliding window, which divides a string of characters into chunks, and then computes an association measures inside the window as it moves. The association measure is a combination of two classical indexes: Mutual Information and t-tests. Here’s the paper:

**Eder, M., Woźniak, M., Modrzyk, U. and Górski, R. L.** (2017). If an atom is a letter, then a molecule is a word: applying corpus linguistic methods to chemistry. _Corpus Linguistics 2017: Conference Abstracts_. University of Birmingham, pp. 743–44, [link to the paper](https://www.birmingham.ac.uk/Documents/college-artslaw/corpus/conference-archives/2017/general/paper366.pdf).




## Topic modeling applied to chemistry

In this paper, we analyzed a corpus of chemical molecules using topic modeling, a technique that attracted a good share of attention in Digital Humanities, but has never been popular beyond text-centric applications. The aim was to identify any relations between chemical “words”. Topic modeling belongs to a group of distributional semantics methods, which are based on a general assumption that the meaning of a word is defined by its lexical context. Topic modeling, usually performed with the LDA algorithm, assumes the “bag-of-words” type of context, which means that the sequence of words in a sentence is irrelevant. This feature allows for computing chemical “words”, which, essentially, do not follow any linear sequence. Here’s the poster we presented at the Digital Humanities 2018 conference; a link to the paper goes below:

<div>
    <img class="col three left" src="{{ site.baseurl }}/assets/img/CHEM_poster_ver7.png" alt="" title="Topic modeling applied to organic chemistry"/>
</div>
<div class="col three caption">
    Fig. 2. Topic modeling applied to organic chemistry.
</div>

**Eder, M., Winkowski, J., Woźniak, M., Górski, R. L., and Grzybowski, B.** (2018). 
Text mining methods to solve organic chemistry problems, or topic modeling applied to chemical molecules. _Digital Humanities 2018: Book of Abstracts_. Mexico City, pp. 562–65, [https://dh2018.adho.org/en/abstracts/](https://dh2018.adho.org/en/abstracts/).





