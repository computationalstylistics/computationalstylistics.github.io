---
layout: page
title: Bootstrap Consensus Networks
description: a method of clustering texts
img: /assets/img/bootstrap_network.png
---



In the present study, stylometric techniques are combined with network analysis to reveal the strongest similarities between analyzed texts on the one hand, and some deeper or less obvious relations, usually filtered out by standard nearest neighbor methods, on the other (Eder, forthcoming)5. Consensus network visualizations (cf. Fig. 1) attempt to overcome drawbacks of Cluster Analysis and other explanatory multidimensional techniques. Firstly, these methods are highly dependent on the number of features (e.g. word frequencies) analyzed, secondly, they are not suitable to visualize large datasets. The technique applied in this study counts frequencies of frequent words in a corpus, computes distances (differences) between samples, and for each sample identifies its nearest neighbors (i.e. the samples that turned out to be the most similar). Next, neighboring samples are turned into connected nodes of a network. The above procedure is repeated many times, in each iteration a different range of frequent words is analyzed. Finally, particular networks produced for each iteration are combined into a single consensus network.


<div>
    <img class="col three left" src="{{ site.baseurl }}/assets/img/diagram_1.png" alt="" title="example image"/>
</div>
<div class="col three caption">
    Fig. 1. Two algorithms of establishing network connections.
</div>


What about an idea of representing nearest neighbors as connections in a network? And what about including not only the first-ranked candidate (i.e. the nearest neighbor), but also two runners-up? Since it is not surprising to see _Tristam Shandy_ by Sterne linked to _Sentimental Journey_ by the same author, it is much more interesting to learn that next similar authors are Swift and Scott. It can be represented as a network of mutual similarities. The above algorithm, introduced by Eder, has been implemented in recent versions of the package 'Stylo'. When the results are loaded into network visualization software, e.g. Gephi, then... Well, have a look at the following pictures:

<div>
    <img class="col three left" src="{{ site.baseurl }}/assets/img/66_English_novels_network.png" alt="" title="example image"/>
</div>
<div class="col three caption">
    Fig. 2. Bootstrap consensus network of 66 English novels. Calculations performed by R and ‘Stylo’, network visualization prepared using Gephi, labels added with Adobe Illustrator.
</div>


<div>
    <img class="col three left" src="{{ site.baseurl }}/assets/img/124_Greek_texts.png" alt="" title="example image"/>
</div>
<div class="col three caption">
    Fig. 3. Bootstrap consensus network of 124 ancient Greek texts (prose, poetry, drama).
</div>



## References

**Eder, M.** (2013). [Computational stylistics and Biblical translation: how reliable can a dendrogram be?](http://www.wsf.edu.pl/upload_module/wysiwyg/Wydawnictwo%20WSF/The%20Translator%20and%20the%20Computer_Piotrowski_Grabowski.pdf) In: T. Piotrowski and Ł. Grabowski (eds.) _The translator and the computer_. Wrocław: WSF Press, pp. 155–170.

**Eder, M.** (2017a). [Visualization in stylometry: cluster analysis using networks](http://dsh.oxfordjournals.org/content/early/2015/12/02/llc.fqv061). _Digital Scholarship in the Humanities_, **32**(1), 50-64, [pre-print].

**Rybicki, J., Eder, M. and Hoover, D.** (2016). Computational stylistics and text analysis. In: C. Crompton, R. L. Lane and R. Siemens (eds.), _Doing Digital Humanities_, London and New York: Routledge, pp. 123-144.

**Eder, M.** (2016b). A bird’s eye view of early modern Latin: distant reading, network analysis and style variation. In: M. Ullyot, D. Jakacki, and L. Estill (eds.), _Early Modern Studies and the Digital Turn_. Toronto and Tempe: Iter and ACMRS, pp. 63-89 (New Technologies in Medieval and Renaissance Studies, vol. 6), [http://ems.itercommunity.org](http://ems.itercommunity.org), [pre-print].

**Eder, M.** (2014c). Stylometry, network analysis and Latin literature. In: _Digital Humanities 2014: Book of Abstracts_, EPFL-UNIL, Lausanne, pp. 457-58, [http://dharchive.org/paper/DH2014/Poster-324.xml](http://dharchive.org/paper/DH2014/Poster-324.xml), [the original poster].

**Eder, M.** (2014b). Large-scale stylometry using network analysis. In: _Qualico 2014: Book of Abstracts_, Olomouc: Palacky University, pp. 38-39, [pre-print].

**Eder, M.** (2014a). Metody ścisłe w literaturoznawstwie i pułapki pozornego obiektywizmu - przykład stylometrii. _Teksty Drugie_, **2**: 90-105.

