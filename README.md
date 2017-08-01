# Background

This repo further processes four texts that were part-of-speech
tagged as part of the project
[TIDC - Tibetan in Digital Communication](https://www.soas.ac.uk/cia/tibetanstudies/tibetan-in-digital-communications/).

1. མཛངས་བླུན་ཞེས་བྱ་བའི་མདོ། (volume-74)
2. མར་པ་ལོ་ཙཱའི་རྣམ་ཐར། (volume-444)
3. བུ་སྟོན་ཆོས་འབྱུང་། (volume-11842)
4. མི་ལའི་རྣམ་ཐར། (volume-11854)

It exploits a further processed version of Nathan Hill's
[Lexicon of Tibetan Verb Stems](https://github.com/tibetan-nlp/lexicon-of-tibetan-verb-stems).

# Formats

The corpus files are made available in various formats.

## Vertical TXT

The corpus is available as vertical TXT files (for example, `volume-74.txt`),
with each word occupying its own line. A TAB separates the word form from its
part-of-speech. At this stage the corpus is not lemmatised, and so the
part-of-speech is always followed by a dash.

```
ངེད་	p.pers -
རང་	p.refl -
གི་	case.gen -
ནོར་བཅོལ་	n.count -
རྣམས་	d.plural -
སྤྲོད་པ་	n.v.pres -
དང་	case.ass -
།	punc -

མཛེས་སེ་	n.prop -
ཡང་	cl.focus -
གནའ་མ	n.count -
# page_id = 11b
ར་	n.count -
བསུ་	v.pres -
ནས་	cv.ela -
ཡབ་	n.count -
ཀྱི་	case.gen -
ཞལ་ཆེམས་	n.count -
བཞིན་	n.rel -
ཕ་ཤུལ་	n.count -
བུ	n.count -
ས་	case.agn -
འཛིན་	v.pres -
དུ་	cv.term -
འཇུག་པ	n.v.pres -
ར་	case.term -
ཞུ་	v.fut.v.pres -
བྱས་པ	n.v.past -
ས	case.agn -
།	punc -
```

Vertical TXT files indicate page/side breaks with interspersed comments of the
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
Where a vertical TXT file breaks a page between two words in the middle of a sentence,
the VISL CG file advances the break forward to the end of the sentence. This makes it
easier for later tools to process the texts.

## VISL CG with Universal Dependencies

The SOAS project Lexicography in Motion (LIM) has mapped the
[TIDC part-of-speech tags](http://larkpie.net/tibetancorpus/tags) to
universal part-of-speech tags and universal features following the guidelines of the
[Universal Dependency](http://universaldependencies.org/) project.

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

For the output of this process, see `volume-74-vislcg-UD.txt` and similarly named files.

To apply the grammar to the input yourself, first install VISL CG3 and then compile the grammar:

`cg-comp minimal-dependencies.txt minimal-dependencies.cg`

Then, apply the grammar to the input, specifying an output file:

`vislcg3 -g minimal-dependencies.cg -I volume-74-vislcg.txt -O volume-74-vislcg-UD.txt`

Alternatively, the output can be piped to a different format using the
[cg-conv](http://beta.visl.sdu.dk/cg3/chunked/cmdreference.html#cg-conv) tool.
This repository, for example, includes the output of the following command:

`vislcg3 -g minimal-dependencies.cg -I volume-74-vislcg.txt | cg-conv -N > volume-74-niceline-UD.txt`

The result is a file in [Niceline CG format](http://beta.visl.sdu.dk/cg3/chunked/streamformats.html#stream-niceline),
which can be easier to process than [VISL CG format](http://beta.visl.sdu.dk/cg3/chunked/streamformats.html#stream-vislcg).

## CoNNL-U

The [CoNNL-U](http://universaldependencies.org/format.html) is used by the UD project to
represent annotated texts. We have also converted our texts to this format.

CoNNL-U format requires a sure analysis; therefore it is not possible to list multiple
candidate lemmas in the lemma column. Instead, in that case, we show the column as
unspecified using the underscore. The candidate lemmas are then copied into the MISC column.

Again, only sure dependency relations are included.
