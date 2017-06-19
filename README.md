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

# VISL CG Conversion

The raw vertical texts downloaded from http://larkpie.net/tibetancorpus/ (for example `volume-74.txt`)
have been converted to [VISL CG format](http://beta.visl.sdu.dk/cg3/single/#stream-vislcg) using a simple
script that is not provided here. The script transforms the input using two lemmatisation files,
`nonverbs-with-lemmas.txt` and `verbs-with-lemmas.txt`. The input text is lemmatised word by word using
the following procedure.

Use the word + part-of-speech as the key. Then look the key up in `nonverbs-with-lemmas.txt`. If it's there,
then retrieve the lemma and write it to the output. If it's not there, then look the key up in
`verbs-with-lemmas.txt`. This time you may retrieve multiple lemmas, since the same word + part-of-speech
could be listed several times. If the word is listed in this file, the write all of its possible lemmas
to the output. Finally, if the word + part-of-speech isn't found in either file, then check to see whether
or not it ends in a tsheg. If it does, then use the word itself as the lemma. If not, then add tsheg and
use that variant as the lemma.

# Universal Dependencies

The new SOAS project Lexicography in Motion (LIM) has mapped the
[TIDC part-of-speech tags](http://larkpie.net/tibetancorpus/tags) to 
universal part-of-speech tags and universal features following the guidelines of the 
[Universal Dependency](http://universaldependencies.org/) project.

The file `minimal-dependencies.txt` is a script that uses the
[Constraint Grammar](http://visl.sdu.dk/constraint_grammar.html) formalism to add these
universal POS tags to our text corpus. CG3 does not directly implement feature-value tags, 
so we just leave the SOAS POS tags in the file, alongside the Universal POS tags,
rather than adding universal feature tags.

In addition, the script adds minimal syntactic dependencies to the texts. 
We add only those dependencies that can be inferred from the
POS tags. For example, if a case marker follows a count noun, then it depends on that count
noun. We know this because case markers are not free-standing words in Tibetan. (Complications may arise
in regards to nominal compounds but we ignore that now.)

For the output of this process, see `volume-74-vislcg-UD.txt` and similarly named files.

To apply the grammar to the input yourself, first install VISL CG3 and then compile the grammar:

`cg-comp minimal-dependencies.txt minimal-dependencies.cg`

Then, apply the grammar to the input, specifying an output file:

`vislcg3 -g minimal-dependencies.cg -I volume-74-vislcg-with-lemmas.txt -O output-74.txt`
