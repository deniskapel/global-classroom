
# Tone prediction and orthographic conversion for Basaa

Basaa (*Ɓàsàa*; ISO-639-3: `bas`) is a Bantu language spoken in Cameroon. It is a tonal language. The language has several orthographies, two are "missionary" orthographies and another is [an orthography](https://en.wikipedia.org/wiki/General_Alphabet_of_Cameroon_Languages) supported by the Academy of Languages of Cameroon.

| Academy | Missionary (Protestant) | Missionary (Catholic) |
|---------|-------------------------|-----------------------|
| Mɛ̀ yè lɛ mɛ̀ ɓɔl nyɔɔ̄ nı̀ màkòò. | Me yé le me bol nyoo ni makôô. | Mè ye lè mè bòl nyòò ni makoo. |

As you can see from the example, the Academy orthography writes the tones, where the two missionary orthographies do not. 

## Task

The purpose of this task is to create a system that will, given input in the missionary orthography convert it to the academy orthography. 

## Data

In the `data/` subdirectory you will find a training set and a development set. The files are tab-separated, in the first column is the Academy orthography and in the second column is the protestant missionary orthography.

| File | Sentences | Tokens |
|------|-----------|--------|
| `train.tsv` | 10000 | 113628 |
| `dev.tsv`   | 1000 |11254 |

The test data will be provided towards the end of the course.

### Sample

```
Ti me bot yem.	Ti mɛ̀ ɓɔ̀t yɛ̂m.
Mimañ mi bôdaa mi ñañna ni jomol.	Mı̀maŋ mi ɓodàa mi ŋâŋnā ni jɔ̀mɔ̂l.
Me bibagla ni bôt bem, me bibagla bôt bem.	Mɛ̀ biɓāgla ni ɓòt ɓɛ̂m, mɛ̀ biɓāgla ɓôt ɓɛ̂m.
Me galo ga ha, ni tehe.	Mɛ̀ galɔ̀ ga hâ, ni tɛhɛ.
A mbéhha me kwade.	À m̂ɓehha mɛ kwādɛ.
Me ñwabal koo i e.	Mɛ̀ ŋ́wàbal kɔɔ i ɛ̄.
A nlem hala.	À ǹlɛm halà.
Ñem u mbôô me matjél.	Ŋɛm u mɓoo mɛ màcèl.
Kôp i ñkek bon.	Kop ı̀ ŋ̀kɛk ɓɔn.
```

### Encoding

Tones in the Academy orthography are encoded by combining characters in Unicode. Note that 
you should avoid using precomposed characters in your output. For example,

| Character | Encoding | Precomposed | Encoding |
|-----------|----------|-------------|----------|
| ô         | `U+006F U+0302` | ô    | `U+00F4` |
| ɔ̀         | `U+0254 U+0300` | -- | -- | 

Also bear in mind that in Python, combining characters are by default treated as two separate 
characters:

```python
>>> len('ɔ̀')
2
```

Your program should support input in both composed and precomposed characters. 

A useful program for working with Unicode data is [Unidump](https://github.com/Codepoints/unidump),

```bash
$ echo "Ti mɛ̀ ɓɔ̀t yɛ̂m." | unidump -n 8
      0    0054 0069 0020 006D 025B 0300 0020 0253    Ti.mɛ̀.ɓ
     11    0254 0300 0074 0020 0079 025B 0302 006D    ɔ̀t.yɛ̂m
     23    002E 000A                                  ..
```

## Baseline

The [baseline system](baseline/) is a simple word-by-word replacement algorithm which takes the most frequent replacement
in the training data.

## Evaluation

Systems will be evaluated by Word Error Rate (WER) and Character Error Rate (CER). You can run the evaluation
using the script `evaluate.py`:

# Probably the best result ever recieved

```bash
$ python3 evaluate.py data/test.tsv output.tsv 
CER: 4.456824512534819
WER: 18.916666666666664
```

# Our experiments

This is the result with a unigram model

```
      CER: 16.54687852515551
      WER: 40.88336922205728
```

This is the result if you only replace words with with frequency = 1.0

```
      CER: 31.07938247332968
      WER: 71.55824609018337
```

This is the result if you only replace words with pairs with frequency >= .75

```
      CER: 24.86543977825765
      WER: 53.64671032464463
```

This is the result if you only replace words with pairs with frequency > .5

```
      CER: 19.860121829374418
      WER: 44.13193799706697
```