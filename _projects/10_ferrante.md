---
layout: page
title: Elena Ferrante
description: Who’s behind that pseudonym?
permalink: /projects/elena-ferrante/
img: /assets/img/domenico_starnone.jpg
---



Elena Ferrante is an Italian writer who does not exist as a person, at least a person bearing that name. Still, someone obviously has been writing her novels. In 2016, an Italian investigative journalist followed the novels’ royalties and announced that they seem to be going to Anita Raja, the Italian translator from the German of Christa Wolf. Raja said this was not true, but things became quite heated also because her husband is Domenico Starnone, a Neapolitan writer (as “Ferrante” always seemed to be) – he has already been mentioned as another possible suspect.

To finally solve this riddle – a very major one in modern Italian literature – the University of Padova, represented by Profs Arjuna Tuzzi and Michele Cortelazzo, organized a workshop called “Drawing Elena Ferrante’s Profile”, which took place in September 2018; they also provided a 150-book electronic corpus of Ferrante and many other suspect Italian writers. Two members of CSG were invited to the workshop together with eight other stylometrists from several countries. Despite using different methods and approaches to authorship attribution, all fingers pointed to Domenico Starnone. Judge for yourselves: in a network analysis of the above-mention Italian corpus, only two authors clustered away from the rest, and these two clustered together: Ferrante and Starnone, in very strong support of the Starnone hypothesis. At the same time, it is worth noting that the translations by Raja are nowhere close to Ferrante.


<div>
    <img class="col three left" src="{{ site.baseurl }}/assets/img/150_Italian_novels.tif" alt="" title="Bootstrap consensus network of 150 Italian contemporary novels"/>
</div>
<div class="col three caption">
    Fig. 1. Bootstrap consensus network of 150 Italian contemporary novels.
</div>




Yet this creates a problem: what if Raja is not visible in this attribution because all we have to go by in establishing her stylometric thumbprint are her translations of another person’s work rather than her _real_ personal traits. This cannot be answered with any certainty. There is still another possibility: Starnone and Raja are in this together, so an attempt was made to look into individual texts by Ferrante to look for possible Raja/Starnone fragments. While the above caveat still remains – Raja’s “signal” can only be represented by her translations of Christa Wolf – the clearly uniform appearance of that of Starnone as the strongest stylometric component over the entire length of a novel by Ferrante (the diagram below shows this for _L’Amica geniale_) brings us perhaps a little closer to some certainty.

<div>
    <img class="col three left" src="{{ site.baseurl }}/assets/img/Raja-Starnone.tif" alt="" title="Rolling SVM for _L’Amica geniale_ against Starnone, Raja and Murgia"/>
</div>
<div class="col three caption">
    Fig. 2. Rolling SVM for <i>L’Amica geniale</i> against Starnone, Raja and Murgia.
</div>


The Padova workshop and its findings made quite a stir in Italy and abroad. [_La Repubblica_](https://napoli.repubblica.it/cronaca/2017/09/09/news/le_prove_sono_nella_letteratura_elena_ferrante_e_starnone_-174989746/?refresh_ce) reported at one and at length, and so did local Padovan news. TA NEA, a major Greek newspaper, went so far as to publish a [picture](http://www.patakis.gr/images/files/1167464.pdf) of some of the researchers involved (including both CSG members). Italian state TV, RAI Cultura, recorded [an interview](http://www.filosofia.rai.it/articoli/rybicki-la-text-analysis-e-le-radici-della-letteratura/40413/default.aspx); another appeared in the Dutch [_De Volkskrant_](https://www.volkskrant.nl/cultuur-media/hoe-een-poolse-wetenschapper-het-grootste-literaire-raadsel-binnen-vijf-minuten-oploste~b227f47b/); and Poland’s _Gazeta Wyborcza_ also ran a broader [story](http://biqdata.wyborcza.pl/biqdata/7,159116,22829674,jak-rozpracowano-elene-ferrante-slowo-po-slowie.html) on the recent Polish contributions in stylometry. Even later, [Treccani](www.treccani.it/magazine/lingua_italiana/articoli/percorsi/percorsi_162.html) reviewed the post-workshop (open-access!) volume edited by Arjuna and Michele (link below). Both Raja and Starnone continue to negate all responsibility. Starnone even said, “I. AM. NOT. ELENA. FERRANTE.” 

---

Now, what if we assume that Starnone is right, and HE. IS. NOT. FERRANTE? What if we assume that whenever Starnone writes under the pseudonym, he is not himself anymore, in the sense that he is able to mimic a distinct authorial signal? What if there are indeed two different personae, the actual Starnone and a virtual “Ferrante”? To further explore the above issue, an additional series of tests have been performed. Again, the Rolling Stylometry technique has been used; this time, however, the training set contained the works a few actual authors, and the works by Ferrante. Needless to say, the novels by Starnone and Ferrane were marked as two distinct classes. 

<div>
    <img class="col three left" src="{{ site.baseurl }}/assets/img/virtual_Ferrante.png" alt="" title=" Novels by Domenico Starnone assessed sequentially via the Rolling Classify technique"/>
</div>
<div class="col three caption">
    Fig. 3. Novels by Domenico Starnone assessed sequentially via the Rolling Classify technique: (a) <i>Il salto con le aste</i> (1989), (b) <i>Via Gemito</i> (2001), (c) <i>Prima esecuzione</i> (2007), <i>Autobiografia erotica di Aristide Gambìa</i> (2011).
</div>

The results are shown in Fig. 3a–d (four novels out of seven); the analyzed novels by Ferrante are ordered chronologically. Arguably, a clear pattern appears: while the early novels show little similarity with the assumed virtual “Ferrante”, the late works are assigned to this class with more and more confidence of the classifier. Almost all of the segments of _L’amore molesto_ (1992) are classified as “Starnone”. The voice of the virtual “Ferrante” is more noticeable in _I Giorni dell’abbandono_ (2002). In _La figlia oscura_ (2006) the share of segments by “Ferrante” is roughly equal to those of “Starnone”. In the novel _L’amica geniale. Infanzia, adolescenza_ (2011) the style of “Ferrante” becomes predominant, which is even more visible in _Storia del nuovo cognome_ (2012). This novel is a triumph of the virtual author: all of the segments have been attributed to the class “Ferrante”. Apparently, Domenico Starnone demonstrates, particularly in his late works, the ability to differentiate his own stylistic profile and the voice of his _alter ego_.


> **Rybicki, M.** (2018). Partners in life, partners in crime? In Tuzzi, A. and Cortelazzo, M. A. (eds), _Drawing Elena Ferrante’s Profile_. Padova: Padova University Press, pp. 111–122, [http://www.padovauniversitypress.it/publications/9788869381300](http://www.padovauniversitypress.it/publications/9788869381300).


> **Eder, M.** (2018). Elena Ferrante: a virtual author. In Tuzzi, A. and Cortelazzo, M. A. (eds), _Drawing Elena Ferrante’s Profile_. Padova: Padova University Press, pp. 31–45, [http://www.padovauniversitypress.it/publications/9788869381300](http://www.padovauniversitypress.it/publications/9788869381300).

---

Check also this [blog post](https://dls.hypotheses.org/73) by Jan Rybicki, featuring the workshop “Drawing Elena Ferrante’s Profile”, organized by Arjuna Tuzzi at the University of Padua, Italy, in September 2018.

The outcomes of the workshop were gathered in [a book published by Padova University Press](http://www.padovauniversitypress.it/publications/9788869381300).


