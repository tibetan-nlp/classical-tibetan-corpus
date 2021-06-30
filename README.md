# Classical Tibetan Corpus
This repository contains a small number of Classical Tibetan texts that were linguistically analyzed and annotated by human beings:

1. མཛངས་བླུན་ཞེས་བྱ་བའི་མདོ། (_mdzangs blun_)
1. མར་པ་ལོ་ཙཱའི་རྣམ་ཐར། (_mar pa lo cA'i rnam thar_)
1. བུ་སྟོན་ཆོས་འབྱུང་། (_bu ston chos 'byung_)
1. མི་ལའི་རྣམ་ཐར། (_mi la'i rnam thar_)
1. ཏཱ་ར་ནཱ་ཐ (_tA ra nA tha_)

With the exception of ཏཱ་ར་ནཱ་ཐ, which was machine-tagged between 2017-2020, the above texts were part-of-speech tagged by human beings as part of the [TIDC (Tibetan in Digital Communication) project](https://www.soas.ac.uk/cia/tibetanstudies/tibetan-in-digital-communications/) (2012-2015).

The tagset was then simplified in approximate conformance with the [Universal POS tags](https://universaldependencies.org/u/pos/all.html) scheme. No information was lost in this process, since many tagging details were encoded as [Universal features](https://universaldependencies.org/u/feat/index.html). For details on this process, see the cg3 grammar ```tidc2upos``` in the `tibcg3` repository.

The texts were then converted into [BRAT standoff format](https://brat.nlplab.org/) so that they could be further analyzed using the _brat rapid annotation tool_. Between 2017-2020, the work focused on annotating the argument structure of Tibetan verbs, using a modified version of the [Universal Dependencies](https://universaldependencies.org/u/dep/all.html) scheme.

At the conclusion of annotation, the BRAT files were exported to [CoNLL-U format](https://universaldependencies.org/format.html), for broader dissemination and use. Please note that although the final BRAT configuration and data files are made available here, they are only provided for completeness. Moving forward, only the CoNNL-U files will be maintained.

English translations of the texts མཛངས་བླུན་ཞེས་བྱ་བའི་མདོ།, མར་པ་ལོ་ཙཱའི་རྣམ་ཐར།, and བུ་སྟོན་ཆོས་འབྱུང་། were obtained, and these translations were aligned at sentence or page-level to the Tibetan texts. In the case of མཛངས་བླུན་ཞེས་བྱ་བའི་མདོ། and མར་པ་ལོ་ཙཱའི་རྣམ་ཐར།, there are two CoNLL-U files each: those with the _-translated_ suffix are translation-aligned at the page-level (making CoNLL-U sentences very long), and untranslated pages are excluded. For these two texts, the files without the _-translated_ suffix lack translation alignments and use _shunits_, i.e. _shad_-delimited units, as CoNLL-U sentences.

You may cite this work by referencing the repository and its authors: Edward Garrett, Nathan Hill, Samyo Rode, Nikolai Solmsdorf, and Sonam Wangyal. We thank the AHRC for its funding of the projects _Tibetan in Digital Communication_ (2012-2015, PI Ulrich Pagel) and _Lexicography in Motion_ (2017-2020, PI Ulrich Pagel).

Here is some metadata about the collection.

| Key | Value |
| ------------- | ------------- |
| Text ID | mdzangs_blun |
| Title (eng) | Sutra of the Wise and the Foolish |
| Title (bod) | མཛངས་བླུན་ཞེས་བྱ་བའི་མདོ་ |
| Source (eng) | Frye, Stanley (1981). The Sutra of the Wise and the Foolish, Library of Tibetan Works and Archives. |
| Source (bod) | (?) |
| Date | (?) |
| Author | Unknown |
| Translation | Stanley Frye |
| Tagging | Edward Garrett & Nathan Hill (?) |
| Annotation | Samyo Rode & Nikolai Solmsdorf |
| Alignment | Sonam Wangyal |
| Genre | Religion |
| Region | Tibet |
| Language | Tibetan, Classical |
| Normalization | No |
| Licensing | Creative Commons Attribution 4.0 International License (CC-BY) |
| Annotator's notes | •	Translated from Chinese into Tibetan ca. 9./10. cent.
•	Canonical text (sDe dge bka’ ’gyur, mDo sde, Vol. 74,fols. 129a–298a)
•	Collection of tales of previous births of the Buddha (skt. jātaka)
•	Reflects structure of translated language (Non-Tibetan origin)
•	Formulaic, repetitive narrative structure
•	Regular grammatical structure, uniform verb frames |

| Key | Value |
| ------------- | ------------- |
| Text ID | mila |
| Title (eng) | The life of Milarepa |
| Title (bod) | མི་ལའི་རྣམ་ཐར་ |
| Source (eng) | Quintman, Andrew (2010). The Life of Milarepa, Penguin Books. |
| Source (bod) | (?) |
| Date | (?) |
| Author | Gtsang smyon Heruka (1452–1507) |
| Translation | Quintman, Andrew |
| Tagging | Edward Garrett & Nathan Hill (?) |
| Annotation | Samyo Rode & Nikolai Solmsdorf |
| Alignment | Sonam Wangyal |
| Genre | Biography |
| Region | Tibet |
| Language | Tibetan, Classical |
| Normalization | No |
| Licensing | Creative Commons Attribution 4.0 International License (CC-BY) |
| Annotator's notes | •	Completed in 1488
•	Vivid language, resembling Colloquial Tibetan in parts
•	Prose interspersed with songs and poems
•	Rich vocabulary
•	Diverse verb structures, e.g. light verbs, auxiliary verbs |

| Key | Value |
| ------------- | ------------- |
| Text ID | marpa |
| Title (eng) | The life of Marpa the Translator |
| Title (bod) | མར་པ་ལོ་ཙཱ་བ་རྣམ་ཐར་ |
| Source (eng) | Trungpa, Chögyam (1982). The Life of Marpa the Translator, Prajna Press. |
| Source (bod) | (?) |
| Date | (?) |
| Author | Gtsang smyon Heruka (1452–1507) |
| Translation | Nalanda Translation Committee under the direction of Chögyam Trungpa |
| Tagging | Edward Garrett & Nathan Hill (?) |
| Annotation | Samyo Rode & Nikolai Solmsdorf |
| Alignment | Sonam Wangyal |
| Genre | Biography |
| Region | Tibet |
| Language | Tibetan, Classical |
| Normalization | No |
| Licensing | Creative Commons Attribution 4.0 International License (CC-BY) |
| Annotator's notes | •	Composed in 1505
•	Large percentage of text is songs and poems
•	Vivid language, resembling Colloquial Tibetan in parts
•	Prose interspersed with songs and poems
•	Rich vocabulary
•	Diverse verb structures, e.g. light verbs, auxiliary verbs |

| Key | Value |
| ------------- | ------------- |
| Text ID | taranatha |
| Title (eng) | History of Buddhism in India |
| Title (bod) | ཙཱ་ར་ནཱ་ཐའི་རྒྱ་གར་ཆོས་འབྱུང་ |
| Source (eng) | Alaka, Chattopadhaya, Alaka and Chattopadhyaya, Debiprasad (1990). Taranatha's History of Buddhism In India, Motilal Banarsidass. |
| Source (bod) | (?) |
| Date | (?) |
| Author | Tāranātha Kun dga’ snying po (1575–1634) |
| Translation | Lama Chimpa Chattopadhaya Alaka |
| Tagging | Marieke Meelen |
| Annotation | Samyo Rode & Nikolai Solmsdorf |
| Alignment | No |
| Genre | History |
| Region | Tibet |
| Language | Tibetan, Classical |
| Normalization | No |
| Licensing | Creative Commons Attribution 4.0 International License (CC-BY) |
| Annotator's notes | •	Composed in 1608
•	History of Buddhism in India and Tibet
•	Mostly prose
•	Limited vocabulary: Lacking diversified verb structures |
