---
layout: page
title: Bootstrap Consensus Networks
description: a method of clustering
img: /assets/img/bootstrap_network.png
---



<div>
    <img class="col three left" src="{{ site.baseurl }}/assets/img/66_English_novels_network.png" alt="" title="Bootstrap consensus network of 66 English novels"/>
</div>
<div class="col three caption">
    Fig. 1. Bootstrap consensus network of 66 English novels. Calculations performed by R and ‘Stylo’, network visualization prepared using Gephi, labels added with Adobe Illustrator.
</div>


## Abstract

The aim of this project (it started as an _ad-hoc_ idea, and then turned into something bigger...) is to discuss reliability issues of a few visual techniques used in stylometry, and to introduce **a new method** that enhances the explanatory power of visualization with a procedure of validation inspired by advanced statistical methods. Since it is based on the idea of Bootstrap Consensus Trees (Eder, 2013), it has been named accordingly: **Bootstrap Consensus Networks**.

The following description is but an appetizer. For a detailed explanation of the method’s theoretical assumptions, features, and implementation refer to the following paper:

> Eder, M. (2017). [Visualization in stylometry: cluster analysis using networks](http://dsh.oxfordjournals.org/content/early/2015/12/02/llc.fqv061). _Digital Scholarship in the Humanities_, 32(1): 50-64, [[pre-print](https://github.com/computationalstylistics/preprints/blob/master/m-eder_visualization_in_stylometry.pdf)].



## Motivation

Most unsupervised (explanatory) methods used in stylometry, such as principal components analysis, multidimensional scaling or cluster analysis, lack an important feature: it is hard to assess the robustness of the estimated model. While supervised classification methods exploit the idea of cross-validation, unsupervised clustering techniques remain, well..., unsupervised. On the other hand, however, the results obtained using these techniques “speak for themselves”, which gives a practitioner an opportunity to notice with the naked eye any peculiarities or unexpected behavior in the analyzed corpus. Also, given a tree-like graphical representation of similarities between particular samples, one can easily interpret the results in terms of finding out the group of texts to which a disputed sample belongs.

One of the biggest problems with cluster analysis, however, is that it highly depends on the number of analyzed features (e.g. frequent words), the linkage algorithm, and the distance measure applied. The decision which of the parameters reveal the actual separation of the samples and which show fake similarities is not trivial at all. Worse, generating hundreds of dendrograms covering the whole spectrum of MFWs, a variety of linkage algorithms, and a number of distance measures, would make this choice even more difficult. At this point, a stylometrist inescapably faces the above-mentioned cherry-picking problem (Rudman, 2003). When it comes to choosing the plot that is the most likely to be “true”, scholars are often in danger of more or less unconsciously picking the one that looks more reliable than others, or that simply confirms their hypotheses.



## Bootstrap consensus trees

A partial solution of the cherry-picking problem involves combining the information revealed by numerous dendrograms into a single consensus plot. This technique has been developed in phylogenetics (Paradis et al., 2004) and later used to assess differences between Papuan languages (Dunn et al., 2005). It has been also introduced into stylometry (Eder, 2013) and applied in a number of stylometric studies (many of them mentioned elsewhere on this website). This approach assumes that, in a large number of “snapshots” (e.g. for 100, 200, 300, 400, …, 1,000 MFWs), actual groupings tend to reappear, and apparent similarities are likely to remain accidental. The goal, then, is to capture the robust patterns across a set of generated snapshots. The procedure is aimed at producing a number of virtual dendrograms, and then at evaluating robustness of groupings across these dendrograms (Fig. 2). 

<div>
    <img class="col two left" src="{{ site.baseurl }}/assets/img/English_poetry.png" alt="" title="An example of a bootstrap consensus tree"/>
</div>
<div class="col two caption">
    Fig. 2. An example of a bootstrap consensus tree: 18 English epic poems clustered according to their stylistic similarities.
</div>


## Bootstrap consensus networks

Although the problem of unstable results can be partially by-passed using consensus techniques, two other issues remain unresolved. Firstly, when the number of analyzed texts exceeds a few dozen, the consensus tree becomes considerably cluttered. Secondly, the procedure of hammering out the consensus is aimed at identifying nearest neighbors only, which means extracting the strongest patterns (usually, the authorial signal) and filtering out weaker textual similarities. To overcome the two aforementioned issues, two tailored algorithms have been introduced.

<div>
    <img class="col three left" src="{{ site.baseurl }}/assets/img/diagram_1.png" alt="" title="Two algorithms of establishing network connections"/>
</div>
<div class="col three caption">
    Fig. 3. Two algorithms of establishing network connections.
</div>

Let the first algorithm establish, for every single node, a strong connection to its nearest neighbor (i.e. the most similar text), and two weaker connections to the 1st and the 2nd runner-up (Fig. 3, top). Consequently, the final network will contain a number of weighted links, some of them being thicker (close similarities), some other revealing weaker connections between samples. The second algorithm (Fig. 3, bottom) is aimed at overcoming the problem of unstable results. It is an implementation of the idea of consensus dendrograms as discussed above into network analysis. The goal is to perform a large number of tests for similarity with different number of features analyzed (e.g. 100, 200, 300, ..., 1,000 MFWs). Finally, all the connections produced in particular “snapshots” are added, resulting in a consensus network. Weights of these final connections tend to differ significantly: the strongest ones mean robust nearest neighbors, while weak links stand for secondary and/or accidental similarities. Validation of the results – or rather self-validation – is provided by the fact that consensus of many single approaches to the same corpus sanitizes robust textual similarities and filters out apparent clusterings.

What’s the added value here? Why include not only the first-ranked candidate (i.e. the nearest neighbor), but also two runners-up? Why bother? Frankly, the idea might seem a bit odd indeed. However, this is exactly the reason why this method proves so powerful. Since it is not surprising to see _Tristam Shandy_ by Sterne linked to _Sentimental Journey_ by the same author, it is much more interesting to learn that next similar authors are Swift and Scott. It can be represented as a network of mutual similarities, where some of the connections are very strong, and some other remain ethereal. More specifically, the algorithms used in Bootstrap Consensus Networks are, in a way, equivalent to the _k_-NN classifier with _k_ = 3.

Establishing the links between the texts is undoubtedly the most important part of the procedure. However, the final step is to arrange the nodes on a plane in such a way that they reveal as much information about linkage as possible. There is a number of out-of-the-box layout algorithms reported in the literature. The members of the Computational Stylistics Group, however, usually choose one of the force-directed layouts: ForceAtlas2 embedded in [Gephi](https://gephi.org/), an open-source tool for network manipulation and visualization (Bastian et al., 2009).



<div>
    <img class="col three left" src="{{ site.baseurl }}/assets/img/124_Greek_texts.png" alt="" title="Bootstrap consensus network of 124 ancient Greek texts"/>
</div>
<div class="col three caption">
    Fig. 4. Bootstrap consensus network of 124 ancient Greek texts (prose, poetry, drama).
</div>


The networks are quite neat as they are, but at the same time they can be enhanced by adding more information. E.g., one can perform Modularity Detection as implemented in Gephi, and color the nodes according to their modularity class. Fig. 4 shows a network of 124 Ancient Greek texts – the identified modularity classes cluster texts written by stylistically similar authors.



## Applications 

Bootstrap consensus networks prove to be very attractive in any “distant reading” approaches to literature, or experiments in which one tries to capture a broader picture of literary periods, genres, and so forth. Below (Fig. 5), a large-ish corpus of 150 Latin texts is shown, where the colors represent three different periods of Latin literature. As one can see, there is some separation between ancient, medieval, and early modern texts, although the separation is not clear-cut. This example comes from a study on distant reading and style variation in Latin (Eder, 2016).

<div>
    <img class="col three left" src="{{ site.baseurl }}/assets/img/latin_network.jpg" alt="" title="Bootstrap consensus network of 150 Latin texts"/>
</div>
<div class="col three caption">
    Fig. 5. Bootstrap consensus network of 150 Latin texts (ancient, medieval, early modern).
</div>

What about a really large-scale experiment? Here’s a network of 2,000 novels, produced by Jan Rybicki (Fig. 6). It consists of 1,000 novels written originally in Polish, and 1,000 translations into Polish from a few languages, including English, Russian, and French. Refer to this [post](https://sites.google.com/site/computationalstylistics/projects/translationese) for more details!

<div>
    <img class="col three left" src="{{ site.baseurl }}/assets/img/network_translationese.png" alt="" title="Bootstrap consensus network of 2,000 texts in Polish"/>
</div>
<div class="col three caption">
    Fig. 6. Bootstrap consensus network of 1,000 texts originally written in Polish, and 1,000 translations into Polish from a few languages.
</div>


The method has been quite extensively applied by the members of the Computational Stylistics Group. Some of the references can be found at the bottom of this post; vast majority of the applications are listed in the [publications](https://computationalstylistics.github.io/publications/) section of this website.




## References

**Bastian, M., Heymann, S. and Jacomy, M.** (2009). Gephi: an open source software for exploring and manipulating networks. In: _International AAAI Conference on Weblogs and Social Media_, [http://www.aaai.org/ocs/index.php/ICWSM/09/paper/view/154](http://www.aaai.org/ocs/index.php/ICWSM/09/paper/view/154).

**Dunn, M., Terrill, A., Reesink, G., Foley, R. and Levinson, S.** (2005). Structural phylogenetics and the reconstruction of ancient language history. _Science_, **309**: 2072–75.

**Eder, M.** (2013). [Computational stylistics and Biblical translation: how reliable can a dendrogram be?](http://www.wsf.edu.pl/upload_module/wysiwyg/Wydawnictwo%20WSF/The%20Translator%20and%20the%20Computer_Piotrowski_Grabowski.pdf) In: T. Piotrowski and Ł. Grabowski (eds.) _The translator and the computer_. Wrocław: WSF Press, pp. 155–170, [[pre-print](https://github.com/computationalstylistics/preprints/blob/master/Eder_Reliability_issues_11122012.pdf)].

**Eder, M.** (2014a). Stylometry, network analysis and Latin literature. In: _Digital Humanities 2014: Book of Abstracts_, EPFL-UNIL, Lausanne, pp. 457-58, [http://dharchive.org/paper/DH2014/Poster-324.xml](http://dharchive.org/paper/DH2014/Poster-324.xml), [[the poster itself](https://github.com/computationalstylistics/preprints/blob/master/m-eder_poster_DH2014.pdf)].

**Eder, M.** (2014b). Metody ścisłe w literaturoznawstwie i pułapki pozornego obiektywizmu - przykład stylometrii. _Teksty Drugie_, **2**: 90-105.

**Eder, M.** (2017). [Visualization in stylometry: cluster analysis using networks](http://dsh.oxfordjournals.org/content/early/2015/12/02/llc.fqv061). _Digital Scholarship in the Humanities_, **32**(1): 50-64, [[pre-print](https://github.com/computationalstylistics/preprints/blob/master/m-eder_visualization_in_stylometry.pdf)].

**Eder, M.** (2016). A bird’s eye view of early modern Latin: distant reading, network analysis and style variation. In: M. Ullyot, D. Jakacki, and L. Estill (eds.), _Early Modern Studies and the Digital Turn_. Toronto and Tempe: Iter and ACMRS, pp. 63-89 (New Technologies in Medieval and Renaissance Studies, vol. 6), [http://ems.itercommunity.org](http://ems.itercommunity.org), [[pre-print](https://github.com/computationalstylistics/preprints/blob/master/Early_modern_latin_PRE-PRINT.pdf)].

**Paradis, E., Claude, J. and Strimmer, K.** (2004). APE: analyses of phylogenetics and evolution in R language. _Bioinformatics_, **20**: 289–90.

**Rudman, J.** (2003). Cherry picking in nontraditional authorship attribution studies. _Chance_, **16**: 26–32.

**Rybicki, J.** (2015). Vive la différence: Tracing the (authorial) gender signal by multivariate analysis of word frequencies. _Digital Scholarship in the Humanities_, [[pre-print](https://github.com/computationalstylistics/preprints/blob/master/Rybicki%20Difference%20preprint.pdf)].

**Rybicki, J., Eder, M. and Hoover, D.** (2016). Computational stylistics and text analysis. In: C. Crompton, R. L. Lane and R. Siemens (eds.), _Doing Digital Humanities_, London and New York: Routledge, pp. 123-144.


