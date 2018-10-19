---
layout: post
title: "Using ‘Stylo’ with languages other than English"
author: Joanna Byszuk
date: 2018-09-19 12:47:00
#description: Using ‘Stylo’ with languages other than English
---




## Can I conduct a ‘Stylo’metric analysis with any language in the world?

In theory – yes. In practice, there are a few things you should consider
first, from examining problems specific to the language (e.g. some
languages, like Japanese, work better with character ngrams rather then
words) to building a big enough, well-balanced and formatted corpus.

## Corpus

While it is a general good practice to use UTF-8 encoding, this is
especially important if the language of your corpus uses Latin
characters with diacritics, e.g. “ó”, “ö”, “ñ”, “ň”, or characters of
entirely different systems, e.g. Chinese or Japanese. If you’re getting
errors despite setting UTF-8 parameter in the GUI, check if all the
files in your corpus are encoded as UTF-8. Various text editors offer
various options, but you can usually check this while saving the file or
in its format settings.

## Languages in ‘Stylo’ gui:

As of 0.6.8 ‘Stylo’ gui allows selection between following languages:  
English, Latin (also a variant treating u/v as u), Polish, Hungarian,
French, Italian, Spanish, Dutch, German, CJK (Chinese, Japanese, Korean)
and Other.

The Other option should work for all languages supported by ‘Stylo’, and
usually there is no need to narrow it down to a specific language group.
Various languages offered in the gui allow for the use of extra features
such as pronoun deletion (feature available in the Features section, not
recommended for most experiments).

If you want to conduct a stylometric analysis on the texts in a language
we haven’t included so far you can add proper codepoints in the
`txt.to.words()`
function:

``` r
txt.to.words(input.text, splitting.rule = "[^PLACE_YOUR_CODEPOINTS_HERE]+", 
             preserve.case = FALSE)   
```

The `^` character in the class defined by the `[ ]` brackets means that
you indicate the characters that you *don’t* want to delete. In other
words, all characters that were not explicitly listed in the brackets
will be used as word delimiters. You can also use `splitting.rule`
parameter for other purposes, e.g. when you want to use other separator
than space (‘Stylo’ default).

Frankly, in a vast majority of applications you don’t even have to know
about the existence of the above `txt.to.words()` function. You simply
pass your codepoints directly to the function `stylo()`:

``` r
stylo(splitting.rule = "[^PLACE_YOUR_CODEPOINTS_HERE]+")   
```

## Language codepoints implemented in ‘Stylo’ ver. 0.6.8

  - Latin supplement (Western): `\U00C0-\U00FF`
  - Latin supplement (Eastern): `\U0100-\U01BF`
  - Latin extended (phonetic): `\U01C4-\U02AF`
  - modern Greek: `\U0386\U0388-\U03FF`
  - Cyrillic: `\U0400-\U0481\U048A-\U0527`  
  - Hebrew: `\U05D0-\U05EA\U05F0-\U05F4`
  - Arabic/Farsi: `\U0620-\U065F\U066E-\U06D3\U06D5\U06DC`
  - extended Latin: `\U1E00-\U1EFF`
  - ancient Greek:
    `\U1F00-\U1FBC\U1FC2-\U1FCC\U1FD0-\U1FDB\U1FE0-\U1FEC\U1FF2-\U1FFC`
  - Coptic: `\U03E2-\U03EF\U2C80-\U2CF3`
  - Georgian: `\U10A0-\U10FF`
  - Japanese (Hiragana): `\U3040-\U309F`  
  - Japanese (Katagana): `\U30A0-\U30FF`
  - Japanese repetition symbols: `\U3005\U3031-\U3035`  
  - CJK Unified Ideographs: `\U4E00-\U9FFF`
  - CJK Unified Ideographs Extension A: `\U3400-\U4DBF`  
  - Hangul (Korean script): `\UAC00-\UD7AF`

## What are the best settings for my language?

Frequent questions include:

  - are words or characters better features for language X?  
  - how many most frequent words are good for tests in language X?  
  - how big should the character *n*-grams be?

Feature selection is a complicated problem on its own, and so far few
studies compared the settings in a cross-lingual perspective. If
possible, a) try to look into literature dealing with your language of
choice, b) start with testing the settings that are considered general
gold standards. You will find some publications on the matter below.

## Bibliography

### Cross-lingual comparisons

**Eder, M.** (2011). [Style-markers in authorship attribution: a
cross-language study of authorial
fingerprint](http://www.ejournals.eu/SPL/2011/SPL-vol-6-2011/art/1171/).
*Studies in Polish Linguistics*, **6**, 99-114,
[pre-print](https://github.com/computationalstylistics/preprints/blob/master/Eder_Style-markers_SLP.pdf).

**Rybicki, J. and Eder, M.** (2011). [Deeper Delta across genres and
languages: do we really need the most frequent
words?](https://academic.oup.com/dsh/article/26/3/315/1149353) *Literary
and Linguistic Computing*, 26(3): 315-21,
[pre-print](https://github.com/computationalstylistics/preprints/blob/master/Rybicki%20Eder%20Deeper%20Delta%20LLC%20corrected%20and%20submitted.pdf).

### Non-Latin scripts

**Du, K.** (2016). [Testing delta on Chinese
texts](http://dh2016.adho.org/abstracts/15). In *Digital Humanities
2016: Conference Abstracts*. Jagiellonian University & Pedagogical
University, Kraków, pp. 781-783.

### Sample size standards

**Eder, M.**(2017c). [Short samples in authorship attribution: A new
approach](https://dh2017.adho.org/abstracts/341/341.pdf). *Digital
Humanities 2017: Conference Abstracts*. Montreal: McGill University,
pp. 221–24.

**Eder, M.** (2010). Does size matter? Authorship attribution, short
samples, big problem. *Digital Humanities 2010: Conference Abstracts*.
King’s College London, pp. 132-35,
[pre-print](https://github.com/computationalstylistics/preprints/blob/master/Eder_Does_Size_Matter_DigHum2010.pdf).

### Feature selection

**Kestemont, M.** (2014). Function words in authorship attribution. From
black magic to theory? In *Third Computational Linguistics for
Literature Workshop*, 59–66. Gothenburg, Sweden: European Chapter of the
Association for Computational Linguistics.

**Sapkota, U., Bethard, S., Montes, M., and Solorio, T.** (2015). Not
all character n-grams are created equal: a study in authorship
attribution. In *Proceedings of the 2015 Conference of the North
American Chapter of the Association for Computational Linguistics: Human
Language Technologies*, 93–102. Denver, Colorado: Association for
Computational Linguistics.

**Stamatatos, E.** (2013). On the robustness of authorship attribution
based on character n-gram features. *Journal of Law and Policy*, 21:
421–39.

You can find studies including many other languages that we’ve conducted
in the [Stylometry
Bibliography](https://www.zotero.org/groups/643516/Stylometry_bibliography).
