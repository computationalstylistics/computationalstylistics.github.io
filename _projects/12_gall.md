---
layout: page
title: Gallus Anonymous
description: Who wrote ‘The Polish Chronicle’?
permalink: /projects/gallus-anonymous
img: /assets/img/gallus.png
---


<div>
    <img class="col three left" src="{{ site.baseurl }}/assets/img/gallus_fragm.png" alt="" title="The Polish Chronicle by Gallus Anonymous"/>
</div>
<div class="col three caption">
    Fig. 1. The first folio of <i>The Polish Chronicle</i> by Gallus Anonymous (Codex Zamoyscianus held at the National Library of Poland, Ms. BOZ cim. 28). Photo retrieved from <a href="https://polona.pl/item/chronicae-et-annales-poloniae,ODI3MDgz/8/#item">Polona</a>.
</div>



The 13<sup>th</sup>-century work entitled _Gesta principium Polonorum_ (_The Deeds of the Princes of the Poles_), also known as _Chronica Polonorum_ (_The Polish Chronicle_), is one of the earliest written documents on the history of Poland. It is also regarded to commence the Polish literary tradition, even if the text itself is in Latin. However, despite the importance of the chronicle, very little is known about its author. Traditionally called “Gallus” (a person from Gaul, or France) and probably a non-Pole, he seems to have been a benedictine monk. A few hypotheses about the author’s origin have been formulated, with the claim about him being a “Gallus” surfaced as early as in the 16<sup>th</sup> century. Then came the Hungarian hypothesis in the 19<sup>th</sup> century, followed by the Venetian hypothesis as formulated in the 1960s by Danuta Borawska (Borawska, 1965), and recently extended by Tomasz Jasiński. The Venetian theory is based on some textual similarities observed between _Translatio Sancti Nicolai_ by an author referred to as the “Monk of Lido” (Monachus Littorensis) and the _Chronicle_. 

In his original study, Jasiński tested rhythmical patterns of Gallus’ sentence endings and found striking similarities with those of Monk of Lido (Jasiński, 2005). The findings were then extended by some extra-textual evindence, in later studies (Jasiński, 2006; 2008; 2009). A motivation to undertake the present study, was the fact that the simple stylometric method proposed by Jasiński was carried out in isolation from the existing state-of-the-art attribution methodology. 

The outcomes of the experiments have been published in the following paper:

> Eder, M. (2015). In search of the author of “Chronica Polonorum” ascribed to Gallus Anonymous: A stylometric reconnaissance. _Acta Poloniae Historica_, 112: 5-23, [[pre-print](https://github.com/computationalstylistics/preprints/blob/master/Eder_Author_of_Chronica_Polonorum.pdf)].

A slightly extended version in Polish is also available (Eder, 2017). Below you will find a few key findings (or, an appetizer).

<div>
    <img class="col two left" src="{{ site.baseurl }}/assets/img/gallus_PCA.png" alt="" title="Gallus’ Chronicle vs. Monachus’s Translatio"/>
</div>
<div class="col two caption">
    Fig. 2. Gallus’ <i>Chronicle</i> vs. Monachus’s <i>Translatio</i>: Principal Components Analysis based on 100 most frequent words.
</div>

Fig. 2 shows a direct comparison of the _Translatio_ and the _Chronica_ against each other, with no reference (yet) to the comparative corpus. Both texts have been divided into sections of 10,000 words each. As a result, _Translatio_ is represented by three samples, and the _Chronicle_ by eight samples: the first three almost exactly coinciding with Book I, samples 5, 6 and a part of 7 belonging to Book II, whereas a lion’s share of sample 7 and the whole of 8 forming Book III. The concentrated distribution of the _Translatio_ samples is quite striking. Most interestingly, however, observable here is an evolution – from the earliest to the latest fragments of the work, with a fairly clear division into Book I (samples 1–3, drifting in the upper area), Book II (the three samples at the centre) and Book III (the less clearly separated samples 7 and 8). This might obviously bring about new findings with regard to the time when the respective sections of the _Chronicle_ were written.

Next comes a comparison of the _Chronicle_ against a number of texts that were written roughly at the same time. A sample dendrogram for 100 most frequent words, the Delta distance measure and Ward’s linkage algorithm is shown in Fig. 3.

<div>
    <img class="col two left" src="{{ site.baseurl }}/assets/img/gallus_clustering.png" alt="" title="Cluster analysis of 9 chronologically close texts"/>
</div>
<div class="col two caption">
    Fig. 3. Cluster analysis of 9 chronologically close texts; Ward linkage, Classic Delta distance measure, and 100 most frequent words.
</div>

The above dendrogram shows rather clearly that a discrete branch hosts three treatises by Bernard de Silvestris – properly recognised as written by the same author – whereas on another branch, the _Chronicle_’s closest neighbor is Monachus’s _Translatio_. This is a considerable, though not decisive, argument in support of the supposed stylistic uniformity of Gallus and Monachus.

Since cluster analysis might be very sensitive to input parameters of the model, it is usually better to use a more sophisticated technique, e.g. [Bootstrap Consensus Networks]({{ site.baseurl }}/projects/bootstrap-networks/). In Fig. 4, a network of 159 Latin texts, including both Gallus and Monachus, has been shown. The right side of the network exhibits mostly historical works – those by Julius Caesar, Tacitus, Sallust, Florus, and others. In terms of the authorship of the _Chronicle_, fundamental are the works which are directly connected to the Gallus’ work, be it a stronger or weaker link. All such similarities are marked in colour, and the relevant nodes labelled. These include, starting from the most distant relationships: Sallust’s _Caligula_ and _Res Gestae Divi Augusti_, Ambrose’s _Letters_ (these being very strongly connected with a number of other nodes), Dante’s _Monarchia_, St. Bernard of Clairvaux's _Life of St. Malachy of Armagh_, Albert of Aachen _Historia Ierosolimitana_, and Augustin Tünger’s _Facetiæ_. 


<div>
    <img class="col three left" src="{{ site.baseurl }}/assets/img/gallus_network.png" alt="" title="Bootstrap consensus network of 159 Latin texts"/>
</div>
<div class="col three caption">
    Fig. 4. Bootstrap consensus network of 159 Latin texts from various epochs (prose works only). The colour is used to mark the texts showing similarities to Gallus’ <i>Chronicle</i>.
</div>


Gallus’ _Chronicle_ demonstrates some stylometric affinity with these works, yet none of them appears to be its closest neighbor. Such close neighbors include: _Chronicon Coenobii Sancti Michaelis de Clusa_ (11<sup>th</sup> century), _The Alexander Romance_ by Pseudo-Callisthenes, _The Ecclesiastical History of the English People_ by Beda Venerabilis, Alexander of Telese’s _The Deeds Done by King Roger of Sicily_ and, lastly, the _Translatio_ by Monachus Littorensis, which is associated with the Gallus’ work due to an extremely strong stylistic similarity: in the other sections of the plot, similarly strong connections are those between the works written by the same author (e.g. the instances of Cicero, Vitruvius, or Varro).

An obvious conclusion comes to mind: the similarity between Gallus and Monachus is so evident that no accidental concurrence can be the case. As long as no better prospective author is proposed, the Venetian background hypothesis will be difficult to undermine.



## References

**Borawska, D.** (1965). Gallus Anonim czy Italus Anonim. _Przegląd Historyczny_, **61**: 111–20.

**Eder, M.** (2015). In search of the author of “Chronica Polonorum” ascribed to Gallus Anonymous: A stylometric reconnaissance. _Acta Poloniae Historica_, **112**: 5-23, [[pre-print](https://github.com/computationalstylistics/preprints/blob/master/Eder_Author_of_Chronica_Polonorum.pdf)].

**Eder, M.** (2017). Autorstwo „Kroniki” Anonima zwanego Gallem w świetle badań stylometrycznych: rekonesans. In Dąbrówka, A., Skibiński, E. and Wojtowicz, W. (eds), _Nobis Operique Favete. Studia nad Gallem Anonimem_. Warszawa: IBL PAN, pp. 59–74.

**Jasiński, T.** (2005). Czy Gall Anonim to Monachus Littorensis? _Kwartalnik Historyczny_, **92**(3): 69–89.

**Jasiński, T.** (2006). Rozwój średniowiecznej prozy rytmicznej a pochodzenie i wykształcenie Galla Anonima. In Sikorski, D. A. and Wyrwa, A. M. (eds.), _Cognitioni gestorum. Studia z dziejów średniowiecza dedykowane Profesorowi Jerzemu Strzelczykowi_. Poznań and Warszawa, pp. 185–93.

**Jasiński, T.** (2008). _O pochodzeniu Galla Anonima_. Kraków: Avalon.

**Jasiński, T.** (2009). Die Poetik in der Chronik des Gallus Anonymus. _Frühmittelalterliche Studien. Jahrbuch des Instituts für Frühmittelalterforschung der Universität Münster_, **43**: 373–91.



