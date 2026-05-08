---
Title: Text Classification
Date Created: 10-February-2026
Last Updated: 28-April-2026
Tags:
  - CS4248
  - AI/ML/Classification
---
# Motivation Of Text Classification
---
A **very common task** in NLP is text classification. So essentially given a text document, <b><span style='color: #FFD700'>assign it a class</span></b>.

>[!tldr] Classes
>Essentially they are your <b><span style='color: #FFD700'>categories for a particular problem</span></b> (*spam or not spam, etc*).
>
>This set of <b><span style='color: #FFD700'>classes are fixed</span></b> (*finite*) & are <b><span style='color: #FFD700'>predefined</span></b> base set of possible outputs that the model can output.

Some tasks can be:
- Language detection
- Spam detection
- Authorship attribution
- Sentiment analysis

>[!danger] Not all tasks are ethical for instance like suicide detection or things which are sensitive to biases
## Formal Setup

Here we will go through some **definitions** to give a foundation of text classification.

So given a **dataset** with various text corpus & classes we can define the following:
- $X$ is the set of all documents, where $x \in X$ means that $x$ is a single document in our dataset
- $Y$ is the classes (*labels*) for all $x$ in the dataset, where $y \in Y$ means that this single class is in our dataset or the set of all possible classes

So a **classification task** we are <b><span style='color: #FFD700'>trying to find this unknown mapping to map the input space to the output space</span></b>. Mathematically we can denote this as, $h : X \rightarrow Y$ or $h(x) = y$.

>[!important] We always hypothesise that there is a "True" mapping
>If not then we will not be doing text classification.

>[!note] There is also such a thing as a multilabel classification where a document is assigned more than 1 class
# Approaches To Text Classification
---
So how do we find the best $\hat{h}(x)$ to **approximate the true mapping** $h(x)$, there are **2 main approaches**:
1) **Rule-based**
Uses things like <b><span style='color: #FFD700'>decision trees & manually defined rules</span></b> (*decision rules*) to classify text.

>[!fail] But this is tedious as someone will need to manually decide what are these decision rules

2) **Supervised learning**
Here we <b><span style='color: var(--mk-color-red)'>use a lot of data with the text & class pairings</span></b> to hopefully allow the model to automatically learn $\hat{h}(x)$ from the dataset (*these* $<x, y>$ *pairings*).

>[!info] We will mainly cover supervised learning methods
## Naive Bayes Classifier

Let's discuss about a simple naive <b><span style='color: #87CEEB'>probabilistic classifier</span></b> based on Bayes Rule. So given a document ($x$) <b><span style='color: #FFD700'>for each possible class</span></b> $(y_{i})$ <b><span style='color: #FFD700'>compute</span></b> $\color{#FFD700}{\boldsymbol{P(y_{i} \vert x)}}$.

>[!question] How do we compute $P(y_{i} \vert x)$?
> We can use [[Year 1/Sem 1/CS1231S - Discrete Structures/Counting & Probability.md#Bayes Theorem|Bayes rule]], which allows to do the following:
> $$
> P(y_{i} \vert x) = \frac{P(x \vert y_{i}) P(y_{i})}{P(x)}
> $$

So if we have $n$ number of classes then we will have $\color{#FFD700}{\boldsymbol{n}}$ <b><span style='color: #FFD700'>number of probabilities</span></b>, which the model will <b><span style='color: #FFD700'>assign the class with the highest probability</span></b> as the text documents class. So mathematically:
$$
y_{i} = \text{argmax}_{y_{i} \in Y} P(y_{i} \vert x)
$$

All this relies on a simple representation where <b><span style='color: #FFD700'>a document is a bag of words</span></b> (*multiset of words*). By doing this we also <b><span style='color: #FFD700'>ignore word orders & other grammar</span></b>.

>[!note] The BoW representation does get affected by tokenization & normalization
>So <b><span style='color: #FFD700'>how we convert is based on the application & task</span></b> which changes the representation of the document.

>[!success] Naive Bayes Classifier is simple
>Easy to understand, implement, fast, not very data hungry, interpretable results all because of the independence assumption (*knowing previous words are not important*).

>[!fail] The assumption of conditional independence
> When [[Year 3/Sem 2/CS4248 - Natural Language Processing/Text Classification.md#Computing The Probability Of A Class|computing the probability]] later on you will notice that we make the assumption that words are independent, but this is <b><span style='color: var(--mk-color-red)'>typically not the case</span></b>.
> 
> But in practice for text classification it works well.

>[!fail] Handling negations
> Let's take the word <b><span style='color: #FFD700'>"not" which flips the semantics of a sentence</span></b>. When computing something like $P(pos \vert "not very funny")$ it will have a high probability because of "very funny".
> 
> >[!success] A solution is to add the negated word like "not" to every word between the negation word & the next punctuation
> >We essentially <b><span style='color: #98FB98'>pad our text with words from the negative class</span></b> to lower the probability of predicting the positive class.
## Computing The Probability Of A Class

>[!note] Before computing we can decide whether or not we want to normalise our documents

So given $x$ a document where $x = w_{1}, \dots w_{n}$ and some class label ($y$), we can form the following equation:
![[Naive Bayes Classifier Formula.png|center|500]]

>[!note] For prior what it means is the proportion of that class label in the dataset

So if we want to **compare** which is more likely between, $P(y_{i} \vert x)$ & $P(y_{j} \vert x)$ we <b><span style='color: #FFD700'>actually do not need to compute the marginal</span></b> (*it will be the same on both sides*).

So now we just need to **compute the numerator** so this is where the "naive" part comes in we assume that <b><span style='color: #FFD700'>all words are independent from each other</span></b>, so our numerator can become:
$$
P(y \vert w_{1} \dots w_{n}) = P(w_{1} \vert y)P(w_{2}\vert y)\dots P(w_{n} \vert y)P(y) = P(y) \prod_{i = 1}^{n}P(w_{i} \vert y) \text{ OR } \log P(y) + \sum_{i = 1}^{n} \log P(w_{i} \vert y)
$$

>[!important] When predicting we will use the above equation & if we did not see the word in our dataset then we exclude it from our computation or do smoothing
>>[!example] Lets say we want to predict $P(pos \vert funny, movie, cast)$
>>And the word funny is not seen in our dataset, then, $P(pos \vert funny, movie, cast) = P(pos)P(movie \vert pos)P(cast \vert pos)$ (*we do not bother with funny*).

So essentially we now compute the probability of a word given a single class. We can calculate the <b><span style='color: #98FB98'>log probability to prevent arithmetic underflow</span></b>.

>[!warning] This is not always the case, take the case "york" will always be paired with "new"

To **compute the prior** ($P(y)$):
$$
P(y) = \frac{N_{y}}{N}
$$
Where:
- $N$ is the number of documents
- $N_{y}$ is the number of documents of class $y$

Then to **compute the likelihood** ($P(w_{i} \vert y)$):
$$
P(w_{i} \vert y) = \frac{\text{Count}(w_{i}, y)}{\sum_{w \in V} \text{Count}(w, y)}
$$
It is exactly the same as how we compute the [[Year 3/Sem 2/CS4248 - Natural Language Processing/N-Gram Language Models.md#N-Gram Language Models|maximum likelihood estimation]], where:
- $\text{Count}(w_{i}, y)$ is the number of occurrences of $w_{i}$ in documents of class $y$
- $\sum_{w \in V} \text{Count}(w, y)$ is the number of every words in documents of class $y$

Then for OOV words or unrepresented classes (*no document that belongs to class y*) we can [[Year 3/Sem 2/CS4248 - Natural Language Processing/N-Gram Language Models.md#Smoothing|apply smoothing]].
- For **prior**, we add $k$ & $k \vert Y \vert$ for the numerator and denominator respectively
- For **likelihood**, we add $k$ & $k \vert V \vert$ for the numerator and denominator respectively
# Evaluating Classifiers
---
Looking at a **binary classification**, our model has 2 ways to get it right & wrong:

![[Images/CS4248 Images/Confusion Matrix.png|ceenter|500]]

>[!important] The orientation will differ depending on where the true & predicted labels are positioned (*top or at the left*)
## Binary Evaluation

With this we can compute various evaluation metrics:
$$
\text{Accuracy} = \frac{TP + TN}{TP + TN + FP + FN}
$$
We can extend the formula to a problem with **more than 2 classes** by just taking the <b><span style='color: #FFD700'>sum of all correctly predicated documents divide by the total number of documents</span></b>.

>[!success] The closer accuracy is to 1 the better the classification model

>[!fail] It is not useful for imbalanced datasets
>This is because our <b><span style='color: var(--mk-color-red)'>model will be too good at predicting the majority class</span></b> because it has more data to learn from.

$$
\text{Recall} = \frac{TP}{TP + FN}
$$
For **recall** we are interested to see the predictions, <b><span style='color: #FFD700'>condition on the true label</span></b> (*correct category*) <b><span style='color: #FFD700'>being positive against all the predicted labels that are positive</span></b>.

>[!info] Recall is also known as sensitivity or true positive rate (TPR)

$$
\text{Precision} = \frac{TP}{TP + FP}
$$
For **precision** we are interested to see the predictions, <b><span style='color: #FFD700'>condition on the predicted label being positive</span></b> and see which of these are <b><span style='color: #FFD700'>predicted correctly</span></b>.

>[!info] Precision is also known as positive predicted value (PPV)

>[!abstract] Recall vs Precision, which to prioritise
> If it is bad if <b><span style='color: #FFD700'>the model did not predict someone who is actually in the positive class</span></b> (*like suicidal or defaulting*) then **prioritise recall over precision**. 
> 
> If it is bad if <b><span style='color: #FFD700'>the model predicts someone with a positive class but they are actually not</span></b> (*news categorisation*) then **prioritise precision over recall**. 

$$
\text{Specificity} = \frac{TN}{TN + FP}
$$

For **specificity** we are interested to see the predications <b><span style='color: #FFD700'>condition on the true label being negative against all the predicted labels that are negative</span></b>. 

>[!info] Precision is also known as the true negative rate (TNR)

$$
\text{F1 Score} = 2 \times \frac{\text{Precision} \times \text{Recall}}{\text{Precision} + \text{Recall}}
$$
>[!info] For F1 score to be 1 precision and recall must be close to 1

>[!question] Why do we use the harmonic mean instead of average?
> This is because we want to <b><span style='color: #FFD700'>emphasis that both precision & recall must be high for F1 score to be high</span></b>.
> 
> If we were to take the average then one can be high while the other is low can we can still get a decent F1 score.
## Multiclass Evaluation

So how do we handle multiclass problems then? We can still create the **confusion matrix** but instead of 2 by 2 we will have <b><span style='color: #FFD700'>y by y</span></b> where $y$ is the number of classes. Then do a tactic called <b><span style='color: #87CEEB'>one vs rest</span></b>.

>[!abstract] One vs Rest confusion matrix
>We can transform our y by y confusion matrix to create a 2 by 2 confusion matrix where we <b><span style='color: #FFD700'>predict one class vs the rest of the classes</span></b>:
>
>![[One vs Rest Confusion Matrix.png|center|300]]
>
>We do this for all $y$ classes.

We have **2 approaches**:
1) **Micro averaging**
Here we take all the one-vs-rest confusion matrix and <b><span style='color: #FFD700'>average over all the TP, FP, FN, TN</span></b>.

>[!example] Example of micro averaging
> ![[Micro Averaging Example.png|center|500]]

>[!fail] Biased towards bigger classes since we are averaging over all counts
>So it favours classes with the majority of the data.

2) **Macro averaging**
Here we use <b><span style='color: #FFD700'>each one-vs-rest confusion matrix and compute a metric</span></b>. Then we take the <b><span style='color: #FFD700'>average of all the matrices</span></b>.

>[!example] Example of macro averaging
>![[Macro Averaging Example.png|center|500]]

>[!success] Less bias than micro averaging since it treats all classes equally
>Since metrices are <b><span style='color: #98FB98'>normalised</span></b>.
# Vector Space Model
---
Most **algorithms** like logistic regression (*since we have talked about text classification*) <b><span style='color: var(--mk-color-red)'>does not work on raw text</span></b>. Typically these are some requirements in order to use these algorithms:
- Numerical input (*and these input values have some meaning*)
- Standardized / canonical input (*fixed size inputs unlike text which can vary*)

What we can do is to do **feature extraction** by <b><span style='color: #FFD700'>vectorization of text data</span></b>.
- Now each document is of a equal sized vector
- Vector elements are numerical values derived from text

We can do a **manual approach** by using <b><span style='color: #FFD700'>handcrafted features</span></b> such as:
- Text length
- Number of positive & negative words
- Emoticons
- etc ...

>[!fail] In practice this is time consuming & finding good features is tricky to do
## Representing Documents With Matrixes

A more **simpler approach** will be to construct a 2D matrix where:
- Each **column** represents <b><span style='color: #FFD700'>one document in our corpus</span></b> ($\vert D \vert$)
- Each **row** represents <b><span style='color: #FFD700'>a unique word from all of the documents</span></b> in the corpus ($\vert V \vert$)

So our resulting matrix will be a $\vert V \vert \times \vert D \vert$ size <b><span style='color: #87CEEB'>document-term matrix</span></b>, where the <b><span style='color: #87CEEB'>weight</span></b> are the <b><span style='color: #FFD700'>matrix value depends on representation</span></b> ($w_{t, d}$) (*t stands for term / word*).

>[!note] Before forming the matrix we can do some normalization steps
> - Removal of non-words
> - Removal of stopwords
> - Case-folding (lowercase)
> - Lemmatization

>[!success] We now have a numerical way of representing documents
>Thus we can:
>- [[Year 3/Sem 2/CS4248 - Natural Language Processing/Text Classification.md#Document Similarity|Compute similarities]] between documents
>- <b><span style='color: #98FB98'>Input into other models</span></b> which requires numerical values

>[!fail] Does not consider the sequential order of the words in the setence
>This can be captured using n-grams.

>[!fail] Using a matrix does not consider semantic similarities between words
>Things like cinema & theater are the same but are considered as 2 different words.

We can assign values to these weights in various ways:
- **Binary** weights (*one hot encoding*)
Here $w_{t, d} = 1$ just means that <b><span style='color: #FFD700'>this document contains this word</span></b> (*or term*).

>[!success] Suitable for filtering of documents
>Since the weight reflects the presence or absence of a particular word in a document (*we can use the [[Year 3/Sem 1/CS4225 - Big Data Systems for Data Science/Data Mining.md#Jaccard Similarity|Jaccard similarity]]*).

>[!fail] No differentiation between words of a document
>It does not tell you whether this word is important or very frequent.

- **Term frequencies**
Here $w_{t, d}$ or $tf_{t, d}$ is equals to the <b><span style='color: #FFD700'>number of occurrences of the word</span></b> (*or term*) in that document.

>[!question] The more frequent the terms in a document the more important it is?
>If document 1 has the word "NLP" 10x but document 2 has it 100x but is also way longer than document 1. Should it be more important?
### Term Frequency - Inverse Document Frequency

>[!info] We covered just 3 out of the many different weighting schemes available
>Binary, term frequency, inverse document frequency.

We <b><span style='color: var(--mk-color-red)'>do not want our importance to scale linearly with term frequency and they also appear a lot in other documents as well</span></b> (*like stopwords!*).

We need to <b><span style='color: #FFD700'>consider a terms relative importance</span></b>. A simple way is to use a <b><span style='color: #FFD700'>sublinear function to model the importance</span></b> (*and not just use the count*):
$$
w_{t, d} = \min
\begin{cases}
1 + \log tf_{t, d}  & \text{, if $tf_{t, d} \gt 0$} \\
0 & \text{, Otherwise}
\end{cases}
$$
>[!info] You can use any base it does not have to be base 10 as long as it is consistent

Another thing we need to consider is <b><span style='color: #FFD700'>cross-document importance</span></b>.

>[!question] If a word appears frequently in 1 document but also frequent in many of the other documents is it important?

The idea is that if a <b><span style='color: #FFD700'>word is frequent in a document & also in other documents then it is not special</span></b>. We can compute an additional factor called the <b><span style='color: #87CEEB'>inverse document frequency</span></b> ($idf_{t}$):
$$
idf_{t} = \log \frac{\vert D \vert}{df_{t}}
$$
Where:
- $\vert D \vert$ is the total number of documents
- $df_{t}$ is the number of documents that contains at least 1 instance of word $t$

>[!note] We use the logarithm to dampen the effect of the inverse document frequence

So **putting everything together**:
$$
w_{t, d} = (1 + \log tf_{t, d}) \times \log \frac{\vert D \vert}{df_{t}}
$$

>[!note] We do this for all unique words in the corpus and for all documents

>[!fail] Word ambiguity might cause TF-IDF to not work as well

>[!fail] Large weights for rare words
>If there is <b><span style='color: #FFD700'>1 rare word in just 1 document</span></b> then it will result in $w_{t, d}$ to be <b><span style='color: var(--mk-color-red)'>very large, but it is not important</span></b>.
>
>>[!success] To solve this we set a minimum threshold of the count of these words before considering assigning weights to them

>[!abstract] Scitkit-learn's TfdifVectorizer / TfdifTransformer
>It has default parameters & includes normalization:
>$$
> w_{t, d} = tf_{t, d} \times \left(\ln \frac{\vert D \vert + 1}{df_{t} + 1} + 1 \right)
>$$
>Where:
>- $tf_{t, d}$ can be just the count or $1 + \log tf_{t, d}$
>- $df_{t}$ is the number of documents that contains at least 1 instance of word $t$
>
>The final +1 is when we encounter $ln 1 = 0$
>  
>By adding one, we are <b><span style='color: #FFD700'>giving the corpus more words that it actually seen</span></b> (*ghost words*) which is essentially smoothing.
# Document Similarity
---
With our **document embedded into a vector space model**:
- Each word is an axis in the $\vert V \vert$ <b><span style='color: #FFD700'>dimensional vector space</span></b> (*it is typically very high dimensional*)
- So a <b><span style='color: #FFD700'>document is a point or a vector in this space</span></b>

>[!info] Typically document vectors are sparse vectors
>Sparse vectors just means that <b><span style='color: #FFD700'>majority of the elements in the vector are zero</span></b>.

So can we use this <b><span style='color: #FFD700'>vector space to compute the similarity</span></b> between text documents (*useful for some NLP tasks*).
## Approaches

### Dot Product

The **dot product between 2 documents** ($v, w$) is defined as:
$$
\text{dot}(v, w) = v \cdot  w = v_{1}w_{1} + v_{2}w_{2} + \dots + v_{n}w_{n} = \sum_{i = 1}^{n}v_{i}w_{i}
$$
Where:
- $n$ is the total number of unique words in all documents

Both documents will be **similar** if the <b><span style='color: #98FB98'>dot product is high</span></b> (*both documents have large values in the same dimensions*).

>[!fail] Dot product overly favours frequent words
> For example the word like "the" which is the most frequent word in any document will push up the dot product value.

>[!fail] Dot product favours long documents
>Longer documents will potentially have more term frequencies & also more words which will push up the dot product value.
>
### Cosine Similarity

Cosine similarity helps to solve some issues from the dot product by <b><span style='color: #FFD700'>not caring about the length of the document but more of the angle between 2 vectors</span></b>.

>[!note] We can also compute bias with cosine similarity
>Just check if words like "Engineer" & "Male" are similar. Same goes for words like "Nurse" & "Female".

The **formula** to compute cosine similarity is as such:
$$
\text{cosine}(v, w) = \frac{v \cdot w}{\Vert v \Vert \times \Vert w \Vert} = \frac{v \cdot w}{\sqrt{\sum^{n}_{i = 1} v^{2}_{i}} \times \sqrt{\sum^{n}_{i = 1} w^{2}_{i}}}
$$
Where:
- $v$ & $w$ are the individual word vectors of 2 documents
- $v_{i}$ or $w_{i}$ is the i-th (*or i-th word*) weight for that specific document

The value **output** can be:
- -1, meaning the vectors point in opposite directions (*our vector is all positive values so this can never happen*)
- 1, meaning vectors <b><span style='color: #98FB98'>point in the same direction</span></b>
- 0, meaning the vectors are <b><span style='color: var(--mk-color-red)'>orthogonal</span></b> (*90 degree angle*)

>[!info] Cosine similarity is symmetric so we just need to fill up half the 2D matrix

>[!warning] Cosine similarity only cares about the angle, sometimes the magnitude is important as well to determine similaritty

