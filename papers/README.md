# Litterature review

The following papers might be used for the project paper:

1. [Multi-components System for Automatic Arabic Diacritization](https://www.semanticscholar.org/paper/Multi-components-System-for-Automatic-Arabic-Abbad-Xiong/c24d9c392878bffd8ee4c7992af967c524786cdb) Probably relevant for basaa too: The automatic diacritization problem is an essential topic due to the high
ambiguity of the undiacritized text and the free word order nature of the grammar. Their results fro two samples are CER1 = 4.00%, WER1 = 12.08%, CER2 = 2.80% and WER2 = 6.22%.
2. [An automatic diacritization algorithm for undiacritized Arabic text](http://etd.uum.edu.my/6822/2/s815357_02.pdf) Only a part of a thesis, but the approaches and levels come from here.
4. [Open Vocabulary Arabic Diacritics Restoration](https://www.semanticscholar.org/paper/Open-Vocabulary-Arabic-Diacritics-Restoration-Hifny/df672bbd9a4e88bffb3487ad28b5afb99d52d858) They apply BPE, sequences of characters not single character or word. Helps to track morphemes.
5. [Higher Order n-gram Language Models for Arabic Diacritics Restoration]()
6. [Diacritizing Arabic Text Using a Single Hidden Markov Model](https://www.researchgate.net/publication/326163674_Diacritizing_Arabic_Text_Using_a_Single_Hidden_Markov_Model)
7. [A Survey of Approaches to Diacritic Restoration](https://www.researchgate.net/publication/328419851_A_Survey_of_Approaches_to_Diacritic_Restoration)
8. [Automatic Diacritics Restoration for Tunisian Dialect](https://www.researchgate.net/publication/334438695_Automatic_Diacritics_Restoration_for_Tunisian_Dialect)
9. [Automatic Diacritics Restoration for Hungarian](https://www.researchgate.net/publication/301445993_Automatic_Diacritics_Restoration_for_Hungarian)
10. [A Cascaded Approach for Social Media Text Normalization of Turkish](https://www.researchgate.net/publication/281239696_A_Cascaded_Approach_for_Social_Media_Text_Normalization_of_Turkish)
11. [Morphological, Syntactic and Diacritics Rules for Automatic Diacritization of Arabic Sentences](https://www.researchgate.net/publication/305111497_Morphological_Syntactic_and_Diacritics_Rules_for_Automatic_Diacritization_of_Arabic_Sentences)
12. [Knowledge and Rule-Based Diacritic Restoration in Serbian](https://www.researchgate.net/publication/328416358_Knowledge_and_Rule-Based_Diacritic_Restoration_in_Serbian)
"The procedure [used in this paper] relies on the comprehensive lexical resources for Serbian: the morphological electronic dictionaries, the Corpus of Contemporary Serbian and local grammars. Dictionaries are used to identify possible candidates for the restoration, while the data obtained from SrpKor and local grammars assists in making a decision between several candidates in cases of ambiguity. The evaluation results reveal that, depending on the text, accuracy ranges from 95.03% to 99.36%, while the precision (average 98.93%) is always higher than the recall (average 94.94%)." I don't think our corpus is large enough to use the approach in this paper. Their corpus includes all Serbian words that use diacritics (p. 43).

#### Statistical  machine  translation  (SMT) is applied in several of the papers. Check if applicable for a small corpus.

### Mainly, there are three approaches to diacritics restoration(text 2):
1. Rule-based approach

The used methods include cascading Weighted Finite-State Transducers[33], lexicon retrieval and rule-based morphological analysis [7]. One other particular work [9] used diacritized text borrowing from other sources to diacritize a highly cited text. [Article 1] To apply this, we have to spot out some rules (they probably exist, but still)

Rule-based corrections are linked to the input and output of the model to apply some changes to the output. These rules can select the appropriate diacritic for
some characters in some contexts, or exclude the wrong choices in other contexts by nullifying their probabilities. Different sets of rules are applied to the outputs to eliminate some impossible diacritizations according to Arabic rules [Article 1] 


2. Statistical approach

This type of approaches includes using Hidden Markov odels both on word level and on character level [8,18,21], N-grams models
on word level and on character level as well [10], Dynamic Programming methods [24–26], classical Machine learning models such as Maximum-entropy
classifier [46], and Deep Learning methods like the Deep Neural Networks, both the classical Multi-Layer Perceptron and the advanced Recurrent Neural Networks[6,14,32,36]. [Article 1] Ngrams on both word and character levels look the easiest for me'. They give an approach to vectorize a sentence, we may try, why not. 


3. Hybrid approach.

They use a deep learning model which is a multi-layer recurrent neural network with LSTM and Dense layers, a character-level rule-based corrector which applies deterministic operations to prevent some errors, and a word-level statistical corrector which uses the context and the distance information to fix some diacritization issues. [Article 1]

The output and the input of the previous phase are transformed and merged to generate a standard diacritized sentence. The sentence is segmented into spacedelimited words and augmented by unique starting and ending entities. Every word in the sentence is checked up to 4 times in the levels of correction using the saved training data. If any acceptable correction is found at any level, the word will be corrected. Otherwise, it will be forwarded to the next level. In the case where many corrections get the same score in a single level, the first correction is chosen. If no correction is found, the predicted diacritization of the previous component is not changed. [Article 1]


### Ways to solve:
1. Word-level
They use first use trigrams, then bigrams and then a Minimum Edit Distance Correction [Article 1]

There are rule based [4], [7] as well as statistical methods for diacritics restoration. Statistical methods based on Hidden Markov Models (HMMs) were introduced in [8]. The hidden states are the diacritized word and the observations are the undiacritized words. The transition and emission probabilities can be estimated from a large training corpus [9]. The most likely diacritized word sequence can be found using the Viterbi [Article 3]

2. Morphemes-level

Arabic is a morphologically rich language and has a high OOV rate [28]. One way to solve this problem is to use character level [29] or n-gram character level [30] diacritization systems. In this letter, we use a novel approach to support open vocabulary diacritics restoration based on the Byte Pair Encoding (BPE)
method [31], [32]. The BPE method segments the words into variable length sub-word units and allows open vocabulary from fixed sub-word units dictionary. We test this approach within the language model scoring framework and report improved performance. [Article 3]

The BPE method segments the words into variable length sub-word units and allows open vocabulary from fixed sub-word units dictionary. The results on the Tashkeela diacritization task show that the proposed method outperforms the character based methods commonly used to support open vocabulary diacritics restoration within the language model scoring framework. [Article 3]

3. Letter-level
The input is mapped to a set of 38 numeric labels representing all the Arabic characters in addition to 0 and the white space. It is transformed into a 2D
one-hot encoded array, where the size of the first dimension equals the length of the sentence, and the size of the second equals the number of the labels.  After that, this array is extended to 3 dimensions by inserting the time steps dimension as the second dimension and moving the dimension of the label into the third position. The time steps are generated by a sliding window of size 1 on the first dimension. The number of time steps is fixed to 10 because this number is large enough to cover most of the Arabic words, along with a part of their previous words. The output of the primary diacritics is also transformed from a vector of labels to a 2D one-hot array. [Artice 1] MIght a way to vectorize each sentence.


### an approach to try [Article 3]

A large diacritized training corpus is segmented into tokens.  This tokenized corpus is used to estimate the n-gram language model.  The unique diacritized tokens in the training set is extracted to construct the mapping dictionary. This dictionary (keys are the undiacritized tokens and values are the diacritized tokens) is used during the test phase to generate the possible diacritized tokens from the input undiacritized token sequence.  For an input undiacritized token sequence, generate all the
possible diacritized hypotheses using the unique tokens dictionary.  Score all the hypotheses and select the hypothesis (diacritized tokens) with the highest score.  Map the tokens into the actual diacritized words.


References
1. Adali, K., & Eryiğit, G. (2014, April). Vowel and diacritic restoration for social media texts. In Proceedings of the 5th Workshop on Language Analysis for Social Media (LASM) (pp. 53-61).
2. De Pauw, G., Wagacha, P. W., & De Schryver, G. M. (2007, September). Automatic diacritic restoration for resource-scarce languages. In International Conference on Text, Speech and Dialogue (pp. 170-179). Springer, Berlin, Heidelberg.
3. Ezeani, I., Hepple, M., & Onyenwe, I. (2016, September). Automatic restoration of diacritics for Igbo language. In International Conference on Text, Speech, and Dialogue (pp. 198-205). Springer, Cham.
5. Ezeani, I., Hepple, M. R., & Onyenwe, I. (2017, April). Lexical disambiguation of Igbo using diacritic restoration. In Proceedings of the 1st Workshop on Sense, Concept and Entity Representations and their Applications (pp. 53-60). Association for Computational Linguistics.
6. Francom, J., & Hulden, M. (2013). Diacritic error detection and restoration via part-of-speech tags. In Proceedings of the 6th Language and Technology Conference.
Luu, T. A., & Yamamoto, K. (2012, November). A pointwise approach for Vietnamese diacritics restoration. In 2012 International Conference on Asian Language Processing (pp. 189-192). IEEE.
7. Zitouni, I., & Sarikaya, R. (2009). Arabic diacritic restoration approach based on maximum entropy models. Computer Speech & Language, 23(3), 257-276.

#### Adali, K., & Eryiğit, G. (2014, April). Vowel and diacritic restoration for social media texts. In Proceedings of the 5th Workshop on Language Analysis for Social Media (LASM) (pp. 53-61).
We propose a hybrid model consisting both a discriminative sequence classifier and a language validator in order to select one of the morphologically valid outputs of the first stage. The proposed model is language independent and has no need for manual annotation of the training data. We measured the performance both on synthetic data specifically produced for these two problems and on real social media data.

To be honest, I found this paper pretty hard to understand. It uses a system that treats diacritization  (adding diacritics) and vowelization (replacing vowels that have been deleted from Twitter posts). We would only need to use the diacritization part. What worked best in this paper was ±2ch + sformcurr + sform0010. So this means it looks at the 2 characters to the right and to the left  (±2ch), uses surface form of the current token (sformcurr), and/or the first n characters of the current token firstnchcurr as lemma feature. They said this was the best model in the literature for Turkish at the time of writing. I am a little unsure of what else to say about it. It seems like maybe it would work for us but, again, I feel like I only have a surface understanding. 

#### De Pauw, G., Wagacha, P. W., & De Schryver, G. M. (2007, September). Automatic diacritic restoration for resource-scarce languages. In International Conference on Text, Speech and Dialogue (pp. 170-179). Springer, Berlin, Heidelberg.
This paper describes experiments with a machine learning approach that is able to automatically restore diacritics on the basis of local graphemic context.We apply the method to the African languages of Cilub`a, G˜ık˜uy˜u, K˜ıkamba, Maa, Sesotho sa Leboa, Tshivenda and Yoruba and contrast it with experiments on Czech, Dutch, French, German and Romanian, as well as Vietnamese and Chinese Pinyin. One issue with the approach used for our purpose is that "...while the method is able to predict diacritics for phonemic variants of the same Latin character with a high degree of accuracy, there are considerable issues when dealing with languages that mark tonality in the orthography” (p. 8).  

#### Ezeani, I., Hepple, M., & Onyenwe, I. (2016, September). Automatic restoration of diacritics for Igbo language. In International Conference on Text, Speech, and Dialogue (pp. 198-205). Springer, Cham.
"In this paper, we experiment using an Igbo bible corpus, which is extensively marked for vowel distinctions, and partially for tonal distinctions, and attempt the task of reinstating these diacritics when they have been deleted. We investigate a number of word-level diacritic restoration methods, based on n-grams, under a closed-world assumption, achieving an accuracy of 98.83% with our most effective method."

“The ‘three key’ trigram model with the Add 1 and backward replacement [was] the most effective method with a performance accuracy of 98.83%” (p. 7). A backward replacement technique tells the program to “step back and correct” anything assumed to be an error. The authors give the example that “if the most probable [trigram] suggest a different diacritic form for the preceding word, then it will be replaced with the current word” (p. 6). 

The stored dictionary used was a copy of the Bible translated into Igbo. Bible verses were used as the unit of entry instead of sentences. The entire corpus contained “1,070,429 tokens (including punctuations and numbers) with 14,422 unique word types out of which 5580 are unambiguous (i.e. appeared only in one diacritic form) in the text. The lexical diffusion on the text is 1.0398. 

#### Ezeani, I., Hepple, M. R., & Onyenwe, I. (2017, April). Lexical disambiguation of Igbo using diacritic restoration. In Proceedings of the 1st Workshop on Sense, Concept and Entity Representations and their Applications (pp. 53-60). Association for Computational Linguistics.
In our previous work, we built some n−gram models with simple smoothing techniques based on a closed world assumption. However, as a classification task, diacritic restoration is well suited for and will be more generalizable with machine learning. This paper, therefore, presents a more standard approach to dealing with the task which involves the application of machine learning algorithms.

Like Basaa, Igbo is a low resource tonal language in need of diacritic restoration. In this study, a decision tree machine-learning algorithm was found to be the most effective (average accuracy of 88.64%) followed by a K Nearest Neighbors algorithm. The article doesn’t say this, but I believe these are grapheme-based approaches (based on the lit review and their previous work). *Out of the papers I read, the methods used in this paper feel like the most applicable to our project.* 

#### Francom, J., & Hulden, M. (2013). Diacritic error detection and restoration via part-of-speech tags. In Proceedings of the 6th Language and Technology Conference.
In this paper we address the problem of diacritic error detection and restoration—the task of identifying and correcting missing accents in text. In particular, we evaluate the performance of a simple part-of-speech tagger-based technique comparing it to other well-established methods for error detection/restoration: unigram frequency, decision lists and grapheme-based approaches. In languages such as Spanish, the current focus, diacritics play a key role in disambiguation and results show that a straightforward modification to an n-gram tagger can be used to achieve good performance in diacritic error identification without resorting to any specialized machinery.

Luu, T. A., & Yamamoto, K. (2012, November). A pointwise approach for Vietnamese diacritics restoration. In 2012 International Conference on Asian Language Processing (pp. 189-192). IEEE.
This paper proposes a pointwise approach for automatically recovering missing diacritics, using three features for classification: n-grams of syllables, n-grams of syllable types, and dictionary word features.


Zitouni, I., & Sarikaya, R. (2009). Arabic diacritic restoration approach based on maximum entropy models. Computer Speech & Language, 23(3), 257-276.
In this paper we present a maximum entropy approach for restoring short vowels and other diacritics in an Arabic document. The approach can easily integrate and make effective use of diverse types of information; the model we propose integrates a wide array of lexical, segment-based and part-of-speech tag features. The combination of these feature types leads to a high-performance diacritic restoration model. 
