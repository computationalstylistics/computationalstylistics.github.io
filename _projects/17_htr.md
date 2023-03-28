---
layout: page
title: HTR
description: and lexicographic sources
permalink: /projects/htr/
img: /assets/img/slowniki_karoteka.jpg
---


<div>
    <img class="col three left" src="{{ site.baseurl }}/assets/img/apelowac_head.jpg" alt="" title="A sample index card with its header detected"/>
</div>
<div class="col three caption">
    Fig. 1. A sample index card with its header detected: the outlined words will next be subject to recognition in next steps of the procedure. The card comes from the <i>Dictionary of the 17th- and 18th-century Polish</i>.
</div>



The project aims to decipher large collections of handwritten index cards of historical dictionaries. We provide a working solution that reads the cards, and links their lemmas to a searchable list of dictionary entries, for a large historical dictionary entitled the _Dictionary of the 17^th^- and 18^th^-century Polish_, which comprizes 2.8 million index cards. We apply a tailored handwritten text recognition (HTR) solution that involves (1) an optimized detection model; (2) a recognition model to decipher the handwritten content, designed as a spatial transformer network (STN) followed by convolutional neural network (RCNN) with a connectionist temporal classification layer (CTC), trained using a synthetic set of 500,000 generated Polish words of different length; (3) a post-processing step using constrained Word Beam Search (WBC): the predictions were matched against a list of dictionary entries known in advance. Our model achieved the accuracy of 0.881 on the word level, which outperforms the base RCNN model. Within this study we produced a set of 20,000 manually annotated index cards that can be used for future benchmarks and transfer learning HTR applications.


## Demo application

You can try how it works! Check out the following link: [http://149.156.30.114:8503/](http://149.156.30.114:8503/)


## References

**Idziak, J., Šeļa, A., Woźniak, M., Leśniak, A., Byszuk, J. and Eder, M.** (2021). Scalable handwritten text recognition system for lexicographic sources of under-resourced languages and alphabets. _Computational Science – ICCS 2021_, vol. 1. (LNCS 12742). Springer, pp. 137–50, [[pre-print](https://arxiv.org/)].


