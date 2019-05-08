# Machine Learning Final Project
**By: Nathan Gibson, Cody Hornberger, Taeho Kim**

### Paper Summary ###
The basic premise of the paper we are focusing on was that blind application of machine learning with respect to data about people could serve to amplify the biases that already exist within that data.  They specifically focused in on the fact that these biases apply to gender bias. The results of their initial study indicated that they were correct in this assessment, and spurred them on to attempt to develop an algorithm to assist in debiasing data about word embeddings as a first step toward rectifying this situation. Additionally, before developing their algorithm, the researchers conducted surveys in an attempt to obtain crowdsourced opinions and determine whether biases contained within the data were reflected in the opinions of the public at large.

Specifically, they looked at word vectors of length 300 that gave insight into the relationships between words, and worked toward creating a debiasing algorithm that would attempt transform word vectors to an equidistant position between gender pairs when those words are of the type that ought to be considered gender neutral, but leave words alone that are intrinsically gender leaning (such as he/she or father/mother). In their debiasing algorithm, their first step was to identify a subspace of word embedding that displays bias in gender neutral words. They then performed one of two operations on gender neutral words in the subspace: either what they called hard debiasing in which they equalized the distance between genders in the subspace if a word ought to be gender neutral, while maintaining as much similarity to the original embedding as possible, or performing what they called soft bias correction, in which they performed linear transformations on the gender neutral words such that pairwise inner products between word vectors would be mostly preserved but they would be closer to the midpoint between genders. The final few paragraphs of this paper went on to show that they'd found their methodology to be fairly successful, giving the example that before debiasing "he is to doctor as she is to X" would output X as nurse, whereas after their debiasing it would output X as physician.

### Reproduction Procedure ###
The researchers published a github repository with their Python code. We used the we.py and debias.py files to reproduce and extend the reserchers' work. The we.py file contains methods to manipulate a word embedding and get relevant analogy pairs given a seed set of pairs. We were able to reproduce and confirm the researchers' results easily. We used their code and attempted to extend it to another characteristic besides gender. Our original idea was to try race, but we found that the nature of finding analogy pairs requires that the characteristic be strictly binary. The researchers shared a preliminary example of how to apply their code to analyze race in word embeddings. We instead created three seed sets of analogy pairs related to international status, socioeconomic status, and age. The most descriptive analogy pairs for each are international-national, rich-poor, and old-young, respectively. These were chosen because we could think of enough similar binary analogies for them to give as seed sets to the alogrithm.
The debias.py file includes code 

### Analysis ###

### References ###

-Man is to Computer Programmer as Woman is to Homemaker? Debiasing Word Embeddings. Bolukbasi et al. https://arxiv.org/abs/1607.06520?context=cs

-Distributed Representation of Words and Phrases and their Compositionality. Mikolo et al. https://papers.nips.cc/paper/5021-distributed-representations-of-words-and-phrases-and-their-compositionality.pdf

-On the Dimensionality of Word Embedding. Yin et al. https://papers.nips.cc/paper/7368-on-the-dimensionality-of-word-embedding.pdf
