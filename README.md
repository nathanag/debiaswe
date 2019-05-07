# Machine Learning Final Project
**By: Nathan Gibson, Cody Hornberger, Taeho Kim**

### Paper Summary ###

### Reproduction Procedure ###
The researchers published a github repository with their Python code. We used the we.py and debias.py files to reproduce and extend the reserchers' work. The we.py file contains methods to manipulate a word embedding and get relevant analogy pairs given a seed set of pairs. We were able to reproduce and confirm the researchers' results easily. We used their code and attempted to extend it to another characteristic besides gender. Our original idea was to try race, but we found that the nature of finding analogy pairs requires that the characteristic be strictly binary. The researchers shared a preliminary example of how to apply their code to analyze race in word embeddings. We instead created three seed sets of analogy pairs related to international status, socioeconomic status, and age. The most descriptive analogy pairs for each are international-national, rich-poor, and old-young, respectively. These were chosen because we could think of enough similar binary analogies for them to give as seed sets to the alogrithm.
The debias.py file includes code 

### Analysis ###

### References ###

-Man is to Computer Programmer as Woman is to Homemaker? Debiasing Word Embeddings. Bolukbasi et al. https://arxiv.org/abs/1607.06520?context=cs

-Distributed Representation of Words and Phrases and their Compositionality. Mikolo et al. https://papers.nips.cc/paper/5021-distributed-representations-of-words-and-phrases-and-their-compositionality.pdf

-On the Dimensionality of Word Embedding. Yin et al. https://papers.nips.cc/paper/7368-on-the-dimensionality-of-word-embedding.pdf
