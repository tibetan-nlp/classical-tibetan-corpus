# Background

This repo makes available four texts that were part-of-speech
tagged as part of the
[TIDC (Tibetan in Digital Communication) project](https://www.soas.ac.uk/cia/tibetanstudies/tibetan-in-digital-communications/),
and are being further processed as part of the
[LIM (Lexicography in Motion) project](https://tibetan-nlp.github.io/lim-annodoc/).

1. མཛངས་བླུན་ཞེས་བྱ་བའི་མདོ། (volume-74)
2. མར་པ་ལོ་ཙཱའི་རྣམ་ཐར། (volume-444)
3. བུ་སྟོན་ཆོས་འབྱུང་། (volume-11842)
4. མི་ལའི་རྣམ་ཐར། (volume-11854)

It exploits a further processed version of Nathan Hill's
[Lexicon of Tibetan Verb Stems](https://github.com/tibetan-nlp/lexicon-of-tibetan-verb-stems).

# Formats

The corpus files are made available in various formats. This includes formats used by the
[TIDC](https://www.soas.ac.uk/cia/tibetanstudies/tibetan-in-digital-communications/),
such as vertical TXT files and VISL CG files. It also includes formats used by the
[LIM](https://tibetan-nlp.github.io/lim-annodoc/), which has mapped
[TIDC part-of-speech tags](http://larkpie.net/tibetancorpus/tags) to
universal part-of-speech tags and universal features following the guidelines of the
[Universal Dependency](http://universaldependencies.org/) project.

## Vertical TXT

The corpus is available as vertical TXT files (for example, `volume-11854.txt`),
with each word occupying its own line. A TAB separates the word form from its
part-of-speech. At this stage the corpus is not lemmatised, and so the
part-of-speech is always followed by a dash.

```
ང་	p.pers -
ཡིན་པ	n.v.cop -
ར་	case.term -
ཤེས་	v.past.v.pres -
ནས་	cv.ela -
ཧ་	n.count -
ལས་	v.invar -
ཏེ	cv.sem -
།	punc -

སྐམ་པ་	n.count -
གཡས་	n.count -
སུ་	case.term -
# page_id = 13a
བོར	v.past -
།	punc -

ཡོས་དཀྲུགས་	n.count -
གཡོན་	n.count -
དུ་	case.term -
བོར	v.past -
།	punc -
```

Vertical TXT files mark the beginning of a new page/side with interspersed comments of the
form `# page_id = X`. Breaks correspond to the original wood block paging,
with the following caveat: where the original source broke a page in the middle
of a word, our texts advance the page break to the end of the word, so that
breaks are only allowed between words.

## VISL CG

The vertical TXT files were then converted to
[VISL CG format](http://beta.visl.sdu.dk/cg3/single/#stream-vislcg) using a simple
script that is not provided here. The script transforms the input using two lemmatisation files,
`nonverbs-with-lemmas.txt` and `verbs-with-lemmas.txt`. The input text is lemmatised word by word using
the following procedure:

> Use the word + part-of-speech as the key. Then look the key up in `nonverbs-with-lemmas.txt`. If it's there,
> then retrieve the lemma and write it to the output. If it's not there, then look the key up in
> `verbs-with-lemmas.txt`. This time you may retrieve multiple lemmas, since the same word + part-of-speech
> could be listed several times. If the word is listed in this file, the write all of its possible lemmas
> to the output. Finally, if the word + part-of-speech isn't found in either file, then check to see whether
> or not it ends in a tsheg. If it does, then use the word itself as the lemma. If not, then add tsheg and
> use that variant as the lemma.

The VISL CG files take even further liberties with page breaking.
Where a vertical TXT file breaks between two words in the middle of a sentence
(as shown by the position of `# page_id = 13a` in the example above), the VISL CG
file advances the break forward until it immediately precedes the following sentence.

```
"<ང་>"
  "ང་√p" p.pers
"<ཡིན་པ>"
  "ཡིན་པ་" n.v.cop
"<ར་>"
  "དུ་√case" case.term
"<ཤེས་>"
  "ཤེས་" v.past.v.pres
"<ནས་>"
  "ནས་√cv" cv.ela
"<ཧ་>"
  "ཧ་" n.count
"<ལས་>"
  "ལས་" v.invar
"<ཏེ>"
  "ཏེ་√cv" cv.sem
"<།>"
  "།" punc
"<སྐམ་པ་>"
  "སྐམ་པ་" n.count
"<གཡས་>"
  "གཡས་" n.count
"<སུ་>"
  "དུ་√case" case.term
"<བོར>"
  "བོར་" v.past
  "འབོར་" v.past
"<།>"
  "།" punc
# page_id = 13a
"<ཡོས་དཀྲུགས་>"
  "ཡོས་དཀྲུགས་" n.count
"<གཡོན་>"
  "གཡོན་" n.count
"<དུ་>"
  "དུ་√case" case.term
"<བོར>"
  "བོར་" v.past
  "འབོར་" v.past
"<།>"
  "།" punc
```

Subsequent derived formats, including Niceline CG, also follow this practice,
which makes the texts easier for later tools to process.

## VISL CG with Universal Dependencies
The file `minimal-dependencies.txt` is a script that uses the
[Constraint Grammar](http://visl.sdu.dk/constraint_grammar.html) formalism to add
universal POS tags and universal features to our text corpus.
Note that CG3 does not directly implement feature-value tags,
so the universal features just come out as complex tags, for example
`NumType=Card|NumForm=Digit`.

In addition, the script adds minimal syntactic dependencies to the texts.
We add only those dependencies that can be inferred from the
POS tags. For example, if a case marker follows a count noun, then it depends on that count
noun. We know this because case markers are not free-standing words in Tibetan. (Complications may arise
in regards to nominal compounds but we ignore that now.)

For the output of this process, see `volume-11854-vislcg-UD.txt` and similarly named files.

To apply the grammar to the input yourself, first install VISL CG3 and then compile the grammar:

`cg-comp minimal-dependencies.txt minimal-dependencies.cg`

Then, apply the grammar to the input, specifying an output file:

`vislcg3 -g minimal-dependencies.cg -I volume-11854-vislcg.txt -O volume-11854-vislcg-UD.txt`

Alternatively, the output can be piped to a different format using the
[cg-conv](http://beta.visl.sdu.dk/cg3/chunked/cmdreference.html#cg-conv) tool.
This repository, for example, includes the output of the following command:

`vislcg3 -g minimal-dependencies.cg -I volume-11854-vislcg.txt | cg-conv -N > volume-11854-niceline-UD.txt`

The result is a file in [Niceline CG format](http://beta.visl.sdu.dk/cg3/chunked/streamformats.html#stream-niceline),
which can be easier to process than [VISL CG format](http://beta.visl.sdu.dk/cg3/chunked/streamformats.html#stream-vislcg).

## CoNNL-U

The [CoNNL-U](http://universaldependencies.org/format.html) format is used by the UD project to
represent annotated texts. We have also converted our texts to this format.

CoNNL-U format requires a sure analysis; therefore it is not possible to list multiple
candidate lemmas in the lemma column. Instead, in that case, we show the column as
unspecified using the underscore. The candidate lemmas are then copied into the MISC column.

Again, only sure dependency relations are included.
