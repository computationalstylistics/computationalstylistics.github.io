---
layout: page
title: Bibliography style
description: for DH publications
permalink: /projects/htr/
img: /assets/img/slowniki_karoteka.jpg
---




While not a research endeavor in the strictest sense, this tiny project has its place in our hearts, without any doubt. It is a little plugin that helps to format bibliographic references according to the style required by the proceedings (aka books of abstracts) of the main annual Digital Humanities conference, but also used in our flagship journal _Digital Scholarship in the Humanities_.

Everyone who has ever published a research paper, knows quite well how tedious it is -- and often frustrating -- to deal with bibliographic references. Particularly, remembering about all the minor trivia, such as where to put a comma rather than a dot, where to switch to italics, and how to abbreviate page numbers, might feel intimidating if not challenging for most of us. 

It cannot be stressed enough how helpful bibliography managers are, e.g. [Zotero](https://www.zotero.org/), to deal with the said issue. If set up properly, they just take over all the formatting and styling. Unfortunately, the bibliographic style used by the DH community has not been supported "just like this". The current project was launched to come in rescue.

First introduced at the [DH2016 conference in Kraków](https://dh2016.adho.org/), and authored by Maciej, the following style definition was released: 

[https://github.com/computationalstylistics/DHAbstracts_biblio_style](https://github.com/computationalstylistics/DHAbstracts_biblio_style)

It's an open-source repository, so feel free to grab it and use it! The file `digital_humanities_abstracts.csl` should be downloaded and installed in Zotero. However, it can be used with other bibliography managers too (see below).

Those who use MS Word as their daily writer, should check out the functionalities of Zotero with a dedicated [MS Word plugin](https://www.zotero.org/support/word_processor_plugin_usage). Using bibliographic entries with such a combination of tools is extremely easy, and kind of awesome! LibreOffice users will find [a similar plugin](https://www.zotero.org/support/libreoffice_writer_plugin_usage), too, and the same applies to the combination of GoogleDocs and Zotero. 

More adventurous users (including all diehard geeks) might want to explore the art of writing scholarly articles directly in plain text, using Markdown codes for minimal styling, and BibTeX files to store the accompanying bibliography. Without any doubt, It's the pinnacle of scholarly reproducibility, since both the code and the actual paper are integrated, and can easily be put on any public repository. 

a lesson in Programming Historian:
https://programminghistorian.org/en/lessons/sustainable-authorship-in-plain-text-using-pandoc-and-markdown


R users might want to discover the package `Rmarkdown` to get to the next level
https://rmarkdown.rstudio.com/
What it does, it allows the users to combine the code and the narrative in one file. The code is then being evaluated (or compiled) and all the plots are being generated on the fly


quarto:
https://quarto.org

Create dynamic content with Python, R, Julia, and Observable.



``` txt
---
title: "Short samples in authorship attribution: a new approach"
author: Maciej Eder
date: 29.03.2020
output: 
  html_document:
    pandoc_args: [ --mathjax, -f, markdown+tex_math_double_backslash ]
    fig_width: 7
    fig_height: 5
bibliography: bibliography.bib
csl: digital_humanities_abstracts.csl
---
```








