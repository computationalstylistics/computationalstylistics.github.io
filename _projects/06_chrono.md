---
layout: page
title: Language Change
description: 
img: /assets/img/coha_features_trimmed.png
---





This 3-year project, founded by the [National Science Centre](https://ncn.gov.pl/?language=en) (2013/11/B/HS2/02795), entitled “Przebiegi zmian gramatycznych i leksykalnych w historii języka polskiego - metody korpusowe i kwantytatywne w językoznawstwie diachronicznym” (“Course of grammatical and lexical changes in the history of the Polish language - corpus-driven quantitative methods in diachronic linguistics”), is aimed at an investigation of grammatical and lexical changes, focusing on trends and dynamics of changes in the middle and modern Polish period. What makes this approach innovative is an extensive use of methods elaborated by quantitative and corpus linguistics. A purpose-built diachronic corpus of Polish will be statistically analysed in order to observe various changes in the course of development of the Polish language. We also intend to date the changes and determine their exact character.

The second objective (considered even more important by the applicants) is to elaborate statistical tools, which allow for description of the course of linguistic changes, their dynamics, and particularly their parallel coocurrences. The applicants aim at developing a methodology, which will combine a diachronic large-scale analysis with an automatic identification of the specific grammatical and lexical features responsible for a language change.

Below, we briefly present – as appetizers of full-length papers to appear – two studies conducted within the project. The first study aims at modeling isolated language changes using logistic regression, whereas the second introduces a new method of assessing the dynamics of language change _en mass_.


## Piotrowski’s law

One can hardly imagine a different picture of a language change than that it starts among a small (possibly sociologically or spatially restricted) group of speakers, gaining gradually more and more users over time, even if an opposition of conservative speakers retard the change. After the first period of slow dissemination, however, the change accelerates, until the newly introduced form is broadly accepted by language users. The recessive form gradually becomes rare, and finally dies out, partly because its adherents die as well. Certainly, it takes time for the change to be completed.

On theoretical grounds, a change in language can follow two main scenarios. Firstly, it can be an innovation that affects a language system without displacing any already-existing forms. In general, newly introduced vocabulary falls into this category (e.g. the emergence of the word _nettiquette_ in the system does not force the word _etiquette_ to disappear). The second scenario occurs when a new form simply replaces the old one, e.g. the degree to which the form _burned_ (the past form of the verb _to burn_) spreads in English, by definition equals to the withdrawal of the irregular form _burnt_. In mathematical terms, the probability of finding a new form and and old form (denoted as _n_ and _o_, respectively) in such a scenario is P(_n_) = 1 – P(_o_), which also implies that P(_o_) = 1 – P(_n_). Consequently, the joint frequency of the two forms might remain constant over the centuries, while their mutual proportions usually vary to a significant degree.

This study explores language change that can be modelled using logistic regression, which in the context of historical linguistics is often referred to as Piotrowski’s law. The examples are drawn from the Polish language. Namely, a few changes that are reported in handbooks of the history of Polish to have taken place between mid-15<sup>th</sup> and mid-19<sup>th</sup> centuries, have been used to validate the theoretical models.

<div>
    <img class="col three left" src="{{ site.baseurl }}/assets/img/piotrowski_wiekszy.png" alt="" title="example image"/>
</div>
<div class="col three caption">
    Fig. 1. Piotrowski’s law (logistic regression) used to model the change <i>większy::więtszy</i>.
</div>


Interesting as it is, such a model cannot overcome the problem of possible co-occurrences of several language changes. In our approach, we propose to combine multiple logistic regression models into one broader picture. An exemplary plot of such a combination is shown in Fig. 2.


<div>
    <img class="col three left" src="{{ site.baseurl }}/assets/img/piotrowski_multiple.png" alt="" title="example image"/>
</div>
<div class="col three caption">
    Fig. 2. Logistic regression model applied to multiple language changes.
</div>



## the dynamics of language change

This study aims at capturing the dynamics of language changes without manual pre-selection of the features that might be responsible for the changes. Our approach was to analyze a considerably large set of 1,000 most frequent words without any further filters. Arguably, in such a big set one should find a few dozen of function words, and a vast majority of content words.

The most natural choice to assess the discriminative power of numerous features at a time is to apply one of the multivariate methods. To this end, an iterative procedure of automatic text classification was applied. Its underlying idea is fairly simple: first, we formulate a working hypothesis that a certain year – be it 1835 – marks a major linguistic break. The procedure randomly picks _n_ text samples written before and after the assumed break; the samples then go into the _ante_ and _post_ subsets. In this study, a period of 20 years before and after the assumed break was covered (with an additional gap of 10 years), 500 text samples of 1,000 tokens were harvested into each of the subsets. To give an example: for the year 1835, 500 random samples covering the time span 1810–1830 were picked into the first subset, and another 500 samples from the years 1840–1860 into the second subset. Next, the both subsets are randomly divided into two halves, so that the training set and the test contain 500 samples representing two classes (_ante_ and _post_). Then we train a supervised classifier – in this case, Nearest Shrunken Centroids – and record the cross-validated accuracy rates. Then we _dismiss_ the original hypothesis, in order to test new ones: we iterate over the timeline, testing the years 1836, 1837, 1838, 1839, ... for their discriminating power. The assumption is simple here: any acceleration of linguistic change will be reflected by higher accuracy scores.


<div>
    <img class="col three left" src="{{ site.baseurl }}/assets/img/coha_accuracy.png" alt="" title="example image"/>
</div>
<div class="col three caption">
    Fig. 3. Language change accelleration in the American English corpus: classification accuracy over the years 1835–1985.
</div>


Despite the above general picture, quite interesting are individual trajectories of the high-impact words. In Fig. 4, one can observe a collinearity of function words: _the_, _and_, _that_, _is_, _been_, as opposed to the possessive _’s_. These function words seem to have impacted the language change at the turn of the 19<sup>th</sup> century.

<div>
    <img class="col three left" src="{{ site.baseurl }}/assets/img/coha_funciton_words.png" alt="" title="example image"/>
</div>
<div class="col three caption">
    Fig. 4. Function words of the biggest impact on the stylistic drift.
</div>







## papers

**Eder, M.** (2018). Words that have made history, or modeling the dynamics of linguistic changes. _Digital Humanities 2018: Book of Abstracts_. Mexico City, pp. 362–65 [https://dh2018.adho.org/en/abstracts/](https://dh2018.adho.org/en/abstracts/).

**Eder, M. and Górski, R. L.** (2016). Historical linguistics’ new toys, or stylometry applied to the study of language change. _Digital Humanities 2016: Conference Abstracts_. Kraków: Jagiellonian University & Pedagogical University, pp. 182–84 [http://dh2016.adho.org/abstracts/398](http://dh2016.adho.org/abstracts/398).

**Eder, M.** (2016). Słowa znaczące, słowa kluczowe, słowozbiory – o statystycznych metodach wyszukiwania wyrazów istotnych. _Przegląd Humanistyczny_, 60(3): 31–44.

**Eder, M., Klapper, M. and Kołodziej, D.** (2015). Dawna polszczyzna i nowe technologie: testowanie metod przetwarzania języka naturalnego na materiale  polskiego piśmiennictwa od średniowiecza po wiek XX. _Biuletyn Polskiego Towarzystwa Językoznawczego_, 71: 189–202.



## recent presentations

link to “Qualico 2018” [presentation](https://computationalstylistics.github.io/history_of_words/)

link to “Digital Humanities 2018” [presentation](https://computationalstylistics.github.io/history_of_words/dh2018_presentation.html) (a short version of the above one)




