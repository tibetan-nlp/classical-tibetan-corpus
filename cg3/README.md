# Background

This repo makes available four texts that were part-of-speech
tagged as part of the
[TIDC (Tibetan in Digital Communication) project](https://www.soas.ac.uk/cia/tibetanstudies/tibetan-in-digital-communications/),
and are being further processed as part of the
[LIM (Lexicography in Motion) project](https://tibetan-nlp.github.io/lim-annodoc/).

1. མཛངས་བླུན་ཞེས་བྱ་བའི་མདོ། (_mdzangs blun_)
2. མར་པ་ལོ་ཙཱའི་རྣམ་ཐར། (_mar pa lo cA'i rnam thar_)
3. བུ་སྟོན་ཆོས་འབྱུང་། (_bu ston chos 'byung_)
4. མི་ལའི་རྣམ་ཐར། (_mi la'i rnam thar_)

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

The corpus is available as vertical TXT files (for example, `mila.txt`),
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

## Niceline CG with Universal POS tags
The file `tidc2upos.txt` is a script that uses the
[Constraint Grammar](http://visl.sdu.dk/constraint_grammar.html) formalism to add
universal POS tags and universal features to our text corpus.
Note that CG3 does not directly implement feature-value tags,
so the universal features just come out as complex tags, for example
`NumType=Card|NumForm=Digit`.

In addition, the script adds self-referential dependency tags for each word.
This makes it easier to convert the resulting Niceline file to CoNNL-U format.

For the output of this process, see `mila-vislcg-UD.txt` and similarly named files.

To apply the grammar to the input yourself, first install VISL CG3 and then compile the grammar:

`cg-comp tidc2upos.txt tidc2upos.cg`

Then, apply the grammar to the input, specifying an output file:

`vislcg3 -g tidc2upos.cg -I mila-vislcg.txt -O mila-vislcg-UD.txt`

Alternatively, the output can be piped to a different format using the
[cg-conv](http://beta.visl.sdu.dk/cg3/chunked/cmdreference.html#cg-conv) tool.
This repository, for example, includes the output of the following command:

`vislcg3 -g tidc2upos.cg -I mila-vislcg.txt | cg-conv -N > mila-niceline-UD.txt`

The resulting file - in [Niceline CG format](http://beta.visl.sdu.dk/cg3/chunked/streamformats.html#stream-niceline) -
is compact and easily converted to other formats.

```
ང་	[ང་√p] p.pers PRON PronType=Prs #1->1
ཡིན་པ	[ཡིན་པ་] n.v.cop AUX VerbForm=Vnoun #2->2
ར་	[དུ་√case] case.term ADP #3->3
ཤེས་	[ཤེས་] v.past.v.pres VERB Tense=Past,Pres #4->4
ནས་	[ནས་√cv] cv.ela SCONJ #5->4 @mark
ཧ་	[ཧ་] n.count NOUN Number=Sing #6->6
ལས་	[ལས་] v.invar VERB #7->7
ཏེ	[ཏེ་√cv] cv.sem SCONJ Case=Sem #8->7 @mark
།	[།] punc PUNCT #9->7 @punct
སྐམ་པ་	[སྐམ་པ་] n.count NOUN Number=Sing #1->1
གཡས་	[གཡས་] n.count NOUN Number=Sing #2->2
སུ་	[དུ་√case] case.term ADP #3->2 @case
བོར	[བོར་] v.past VERB Tense=Past #4->4	[འབོར་] v.past VERB Tense=Past #4->4
།	[།] punc PUNCT #5->4 @punct
# page_id = 13a
ཡོས་དཀྲུགས་	[ཡོས་དཀྲུགས་] n.count NOUN Number=Sing #1->1
གཡོན་	[གཡོན་] n.count NOUN Number=Sing #2->2
དུ་	[དུ་√case] case.term ADP #3->2 @case
བོར	[བོར་] v.past VERB Tense=Past #4->4	[འབོར་] v.past VERB Tense=Past #4->4
།	[།] punc PUNCT #5->4 @punct
```
## CoNNL-U

[CoNNL-U](http://universaldependencies.org/format.html) is a format used by the
UD project to represent annotated texts. We have also converted our texts to this format.

CoNNL-U format requires a sure analysis; therefore it is not possible to list multiple
candidate lemmas in the lemma column. Instead, in that case, we show the column as
unspecified using the underscore. The candidate lemmas are then copied into the MISC column.
By the same token, only sure dependency relations are included.

The fragment repeated above is represented as follows in CoNNL-U:

```
1	ང་	ང་√p	PRON	p.pers	PronType=Prs	1	 
2	ཡིན་པ	ཡིན་པ་	AUX	n.v.cop	VerbForm=Vnoun	2	 
3	ར་	དུ་√case	ADP	case.term		3	 
4	ཤེས་	ཤེས་	VERB	v.past.v.pres	Tense=Past,Pres	4	 
5	ནས་	ནས་√cv	SCONJ	@mark		4	 
6	ཧ་	ཧ་	NOUN	n.count	Number=Sing	6	 
7	ལས་	ལས་	VERB	v.invar		7	 
8	ཏེ	ཏེ་√cv	SCONJ	@mark	Case=Sem	7	 
9	།	།	PUNCT	@punct		7	 

1	སྐམ་པ་	སྐམ་པ་	NOUN	n.count	Number=Sing	1	 
2	གཡས་	གཡས་	NOUN	n.count	Number=Sing	2	 
3	སུ་	དུ་√case	ADP	@case		2	 
4	བོར	_	VERB	v.past	Tense=Past	4	[བོར་][འབོར་]
5	།	།	PUNCT	@punct		4	 

# page_id = 13a
1	ཡོས་དཀྲུགས་	ཡོས་དཀྲུགས་	NOUN	n.count	Number=Sing	1	 
2	གཡོན་	གཡོན་	NOUN	n.count	Number=Sing	2	 
3	དུ་	དུ་√case	ADP	@case		2	 
4	བོར	_	VERB	v.past	Tense=Past	4	[བོར་][འབོར་]
5	།	།	PUNCT	@punct		4	 
```
