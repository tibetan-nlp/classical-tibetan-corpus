# Classical Tibetan Corpus
This repository contains a small number of Classical Tibetan texts that were linguistically analyzed and annotated by human beings:

1. མཛངས་བླུན་ཞེས་བྱ་བའི་མདོ། (_mdzangs blun_)
1. མར་པ་ལོ་ཙཱའི་རྣམ་ཐར། (_mar pa lo cA'i rnam thar_)
1. བུ་སྟོན་ཆོས་འབྱུང་། (_bu ston chos 'byung_)
1. མི་ལའི་རྣམ་ཐར། (_mi la'i rnam thar_)
1. Taranatha

With the exception of Taranatha, which was machine-tagged between 2017-2020, the above texts were part-of-speech tagged by human beings as part of the [TIDC (Tibetan in Digital Communication) project](https://www.soas.ac.uk/cia/tibetanstudies/tibetan-in-digital-communications/) (2012-2015).

The tagset was then simplified in approximate conformance with the [Universal POS tags](https://universaldependencies.org/u/pos/all.html) scheme. No information was lost in this process, since many tagging details were encoded as [Universal features](https://universaldependencies.org/u/feat/index.html). For details on this process, see the cg3 grammar _tid2upos_.

The texts were then converted into [BRAT standoff format](https://brat.nlplab.org/) so that they could be further analyzed using the _brat rapid annotation tool_. Between 2017-2020, the work focused on annotating the argument structure of Tibetan verbs, using a modified version of the [Universal Dependencies](https://universaldependencies.org/u/dep/all.html) scheme.

At the conclusion of annotation, the BRAT files were exported to [CoNLL-U format](https://universaldependencies.org/format.html), for broader dissemination and use. Please note that although the final BRAT configuration and data files are made available here, they are only provided for completeness. Moving forward, only the CoNNL-U files will be maintained.

English translations of the texts མཛངས་བླུན་ཞེས་བྱ་བའི་མདོ།, མར་པ་ལོ་ཙཱའི་རྣམ་ཐར།, and བུ་སྟོན་ཆོས་འབྱུང་། were obtained, and these translations were aligned at sentence or page-level to the Tibetan texts. In the case of མཛངས་བླུན་ཞེས་བྱ་བའི་མདོ། and མར་པ་ལོ་ཙཱའི་རྣམ་ཐར།, there are two CoNLL-U files each: those with the _-translated_ suffix are translation-aligned at the page-level (making CoNLL-U sentences very long), and untranslated pages are excluded. For these two texts, the files without the _-translated_ suffix lack translation alignments and use _shunits_, i.e. _shad_-delimited units, as CoNLL-U sentences.

You may cite this work by referencing the repository and its authors: Edward Garrett, Nathan Hill, Samyo Rode, Nikolai Solmsdorf, and Sonam Wangyal. We thank the AHRC for its funding of the projects _Tibetan in Digital Communication_ (2012-2015, PI Ulrich Pagel) and _Lexicography in Motion_ (2017-2020, PI Ulrich Pagel).
