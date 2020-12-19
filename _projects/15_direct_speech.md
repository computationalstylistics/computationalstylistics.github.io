---
layout: page
title: Direct Speech
description: direct speech detection
permalink: /projects/direct_speech/
img: /assets/img/direct_speech.png
---

# Direct speech detection using deep learning
## About the project
The project was born as part of [Deep learning in computational stylistics](https://computationalstylistics.github.io/projects/deep_learning/) collaboration between University of Antwerp and Institute of Polish Language PAS, funded by Research Foundation of Flanders (FWO) and the Polish Academy of Sciences (PAS), and in support of the COST Action [Distant Reading](https://www.distant-reading.net/) in which some of us participate.  

# The outline
Fictional prose can be broadly divided into narrative and discursive forms with direct speech being central to any discourse representation (alongside indirect reported speech and free indirect discourse). This distinction is crucial in digital literary studies and enables interesting forms of narratological or stylistic analysis. The difficulty of automatically detecting direct speech, however, is currently under-estimated. Rule-based systems that work reasonably well for modern languages struggle with (the lack of) typographical conventions in 19th-century literature. While machine learning approaches to sequence modeling can be applied to solve the task, they typically face a severed skewness in the availability of training material, especially for lesser resourced languages.  
In our project, we develop a multilingual approach to direct speech detection in a diverse corpus of 19th-century fiction in 9 European languages. The proposed method finetunes a transformer architecture with multilingual sentence embedder on a minimal amount of annotated training in each language, and improves performance across languages with ambiguous direct speech marking, in comparison to a carefully constructed regular expression baseline.

## Malaga workshop materials
[The presentation](https://docs.google.com/presentation/d/1jlENADuXeM9s5whAtJuC5LhC4kr4BqGIhZf-dz0eSxE/edit#slide=id.g6f1691de29_0_0)  
[Materials on binder](https://mybinder.org/v2/git/https%3A%2F%2Fgitlab.ijp.pan.pl%3A11431%2Fpublic-focs%2Fmalaga/2154c990d43b12d4e5d749cc7a4351c73ce44254)  
[The latest model - as of late February](https://gitlab.ijp.pan.pl:11431/public-focs/detecting-direct-speech)  

## Resources

**Byszuk, J., Woźniak, M., Kestemont, M., Leśniak, A., Łukasik, W., Šeļa, A. and Eder, M.** (2020). Detecting direct speech in multilingual collection of 19th century novels. In _LREC 2020_. [preprint](https://github.com/computationalstylistics/preprints/blob/master/byszuk-et-al_LT4HALA_final.pdf) [final version pp. 100-104](https://lrec2020.lrec-conf.org/media/proceedings/Workshops/Books/LT4HALAbook.pdf)


