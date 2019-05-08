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

Finally, we attempted to reproduce the procedure from the paper with a different embedding. We observed that the original word embedding was heavily filtered and we suspected that the given results might be specific to that dataset. We found a word embedding built from Wikipedia data that was in a compatible format. The Wikipedia word embedding was approximately 1 GB, compared to 80 MB from the original embedding. We were able to run the gender-related code with all the same inputs other than the embedding and analyzed the results.

### Code ###
Our code is contained in the additional_bias.ipynb notebook. The Wikipedia dataset is not included on the repo because its large size.

### Analysis ###

After reproducing the procedure from the paper with a different Wikipedia dataset, we found that the results were much less profound. Most of the generated analogy pairs did not make sense and many contained numbers and indiscernible words. We did, however, find a few stereotypical pairs similar to those found in the paper, such as physician-nurse, football-volleyball, and feminism-nationalism. The debiasing results were similarly uneventful. It may be the case that news articles contain more biased language than Wikipedia. It would be an interesting future study to look into this further. If we had more time, we would have liked to experiment with additional filtering of the different dataset and test more datasets. However, we concluded from our initial efforts that the procedure outlined in the paper may be sensitive to the dataset used and the profound findings may not be as prevelant in other embeddings.

For socioeconomic status, before debiasing, the analogies produced had few appropriate and stereotypical analogies. Few examples being “advantage-disadvantage”, “luxuries-necessities”, “limo-bus”, “ample-insufficient”, “mansion-townhouse”, and more. Although these analogies seem to demonstrate similar direction as “rich-poor”, most of the analogies produced by the program does not seem to follow the same direction and does not show obvious reasoning. It is also plausible that these analogies are simple antonyms rather than complex analogy based on socioeconomic direction we provided. As shown in the additional bias notebook, there is a significant disparity in number of valid (definitional and stereotypical) analogies produced with socioeconomic status and binary gender. 

After debiasing the word embeddings of socioeconomic status, the number of both definitional and stereotypical analogies decreased further. Of the 500 analogies produced, less than five were valid. Most analogies produced were synonyms most likely since the pairs are closely related. Even the definitional pairs used as input to the debiasing functions could not be found in the output analogies. Although debiasing the word embedding of gender based biases resulted in decreased in number of analogies as shown in the original paper, the word embeddings still retained most of the valid analogies. 

Nationality status and age had similar outcomes. Directions based on these classifications had even less valid analogies than socioeconomic status. Of 500 analogies produced, less than ten analogies were either definitional and stereotypical for both classifications. After debiasing, the word embeddings were only able to produce less than five valid analogies for both classifications. 

We suspect that such huge disparity between gender based bias in word embeddings and biases based on other classifications is largely due to how everyday language works. Gender is more ingrained into our language, English,  as nouns and pronouns, whereas socioeconomic status, race, nationality, and age are not. Words that are related to gender or hold meaning based on gender are used even when the conversation isn't about gender. However, words that convey or mean socioeconomic status, nationality status, or age are often only used when talking about those subjects. Therefore, we believe that biases based on our chosen classifications are less prevalent in word embeddings. If words related to these classification are used less often, then it would be much more difficult to find biases in word embeddings.

#### Table: Number of Valid (definitional and stereotypical) Analogies ####
| | Socioeconomic Status | Nationality Status | Age
| --- | --- | --- | ---|
| Before | 21 | 9 | 15 |
| After | 8 | 3 | 8 |

All analogies produced and mentioned in this section can be found in additional_bias.ipynb notebook.

### References ###

-Man is to Computer Programmer as Woman is to Homemaker? Debiasing Word Embeddings. Bolukbasi et al. https://arxiv.org/abs/1607.06520?context=cs

-Distributed Representation of Words and Phrases and their Compositionality. Mikolo et al. https://papers.nips.cc/paper/5021-distributed-representations-of-words-and-phrases-and-their-compositionality.pdf

-On the Dimensionality of Word Embedding. Yin et al. https://papers.nips.cc/paper/7368-on-the-dimensionality-of-word-embedding.pdf
