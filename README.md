# Machine Learning Final Project
**By: Nathan Gibson, Cody Hornberger, Taeho Kim**

### Paper Summary ###
The basic premise of the paper we are focusing on was that blind application of machine learning with respect to data about people could serve to amplify the biases that already exist within that data.  They specifically focused in on the fact that these biases apply to gender bias. The results of their initial study indicated that they were correct in this assessment, and spurred them on to attempt to develop an algorithm to assist in debiasing data about word embeddings as a first step toward rectifying this situation. Additionally, before developing their algorithm, the researchers conducted surveys in an attempt to obtain crowdsourced opinions and determine whether biases contained within the data were reflected in the opinions of the public at large.

Specifically, they looked at word vectors of length 300 that gave insight into the relationships between words, and worked toward creating a debiasing algorithm that would attempt transform word vectors to an equidistant position between gender pairs when those words are of the type that ought to be considered gender neutral, but leave words alone that are intrinsically gender leaning (such as he/she or father/mother). In their debiasing algorithm, their first step was to identify a subspace of word embedding that displays bias in gender neutral words. They then performed one of two operations on gender neutral words in the subspace: either what they called hard debiasing in which they equalized the distance between genders in the subspace if a word ought to be gender neutral, while maintaining as much similarity to the original embedding as possible, or performing what they called soft bias correction, in which they performed linear transformations on the gender neutral words such that pairwise inner products between word vectors would be mostly preserved but they would be closer to the midpoint between genders. The final few paragraphs of this paper went on to show that they'd found their methodology to be fairly successful, giving the example that before debiasing "he is to doctor as she is to X" would output X as nurse, whereas after their debiasing it would output X as physician.

### Reproduction Procedure ###
The researchers published a github repository with their Python code. We used the we.py and debias.py files to reproduce and extend the researchers’ work. The we.py file contains methods to manipulate a word embedding and get relevant analogy pairs given a seed set of pairs. We were able to reproduce and confirm the researchers' results easily using the same dataset. We used their code and attempted to extend it to another characteristic besides gender. Our original idea was to try race, but we found that the nature of finding analogy pairs as they did in the paper requires that the characteristic be strictly binary. We found the procedures used by the researchers are best applied to gender and cannot be easily extended to other characteristics.

The researchers shared a preliminary example of how to apply their code to analyze race in word embeddings. This work was not included in the paper but was shared in a tutorial of how to use their code. To address the binary limitations, they used popular white and black names in place of analogy pair seeds. This approach did not produce many noteworthy stereotypical pairs compared to the gender-based approach. We felt that this method for race analysis was very limited and could be improved since it is constrained by the names present in the dataset. We attempted to improve the method by adding additional names, but many were not present. It appeared that the researchers included the names in the word embedding dataset for the purpose of conducting this analysis. The embeddings were obtained from Google News articles and the researchers kept the most frequent words and filtered out many. Although findings may be more significant with more data and names, we felt that a better approach could be carried out.

We instead created three seed sets of analogy pairs related to nationality status, socioeconomic status, and age and attempted to analyze it in a similar manner to how gender was done. The most descriptive analogy pairs for each are international-national, rich-poor, and old-young, respectively. These were chosen because we could think of the most similar binary analogies for them to give as seed sets to the algorithm. The chosen analogy pairs are shown below.

**Nationality Status:** national-international, citizen-immigrant, citizenship-visa, native-alien, domestic-foreign

**Socioeconomic Status:** rich-poor, wealthy-impoverished, wealth-poverty

**Age:** old-young, parent-child, elderly-youth, past-future, old-new, death-birth

The seed pairs are used to determine an initial direction to distinguish between the two groups. The code uses linear algebra and Principal Component algorithms to find associations in the word embeddings and return additional analogy pairs. We inputted our seed pairs and ran the code for each of the three categories and analyzed the results.
The debias.py file includes code to conduct the debiasing. It also took analogy pairs as input and generated additional pairs based off the word embedding, but this time attempting to return more true, neutral words while avoiding returning pairs that may be stereotypical. We also ran this on each of our three categories and analyzed the results. The debias method takes the seed pairs as well as gender-specific words and equalize pairs as additional input. The researchers built these inputs from data collected from a questionnaire that asked survey-takers to rate the bias of different gender-related words. The documentation specifies that these inputs are not necessary, so we did not enter anything for them. Our results may have been more significant if we had collected similar survey data for our characteristics.

### Analysis ###

### References ###

-Man is to Computer Programmer as Woman is to Homemaker? Debiasing Word Embeddings. Bolukbasi et al. https://arxiv.org/abs/1607.06520?context=cs

-Distributed Representation of Words and Phrases and their Compositionality. Mikolo et al. https://papers.nips.cc/paper/5021-distributed-representations-of-words-and-phrases-and-their-compositionality.pdf

-On the Dimensionality of Word Embedding. Yin et al. https://papers.nips.cc/paper/7368-on-the-dimensionality-of-word-embedding.pdf
