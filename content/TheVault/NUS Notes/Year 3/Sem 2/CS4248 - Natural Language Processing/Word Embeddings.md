---
Title: Word Embeddings
Date Created: 10-March-2026
Last Updated: 28-April-2026
Tags:
  - CS4248
---
# What's Wrong With Our Document Representation?
---
So if you recall we mentioned we can [[Year 3/Sem 2/CS4248 - Natural Language Processing/Text Classification.md#Representing Documents With Matrixes|represent a document as a vector]]:
- One hot encoding
- BoW
- TF-IDF

The main issue is that these methods we <b><span style='color: var(--mk-color-red)'>do not consider word order</span></b> (*some tasks requires word order some does not need it*).

>[!question] Why is this the case?
>Lets take one hot encoding for example and we have words, cat, dog, lion, bear and so on
>
>Our encoding will look like this:
>
>|      | w1  | w2  | w3  | w4  | ... |
| :--: | :-: | :-: | :-: | :-: | :-: |
| dog  |  1  |  0  |  0  |  0  | ... |
| cat  |  0  |  1  |  0  |  0  | ... |
| lion |  0  |  0  |  1  |  0  | ... |
| bear |  0  |  0  |  0  |  1  | ... |
| ...  | ... | ... | ... | ... | ... |
>
> So in the first dimension it represents the word dog, but a puppy will be in another dimension. So <b><span style='color: #FFD700'>there is no notion of similarity since words are in different dimensions</span></b>.

In general <b><span style='color: #FFD700'>word order matters</span></b>, so now we need to **represent words as vectors** and not like an individual cell. These are called <b><span style='color: #87CEEB'>word vectors / embeddings</span></b>.

>[!goal] We want to form a vector to encode the characteristics of the word so that 2 similar words have almost identical vectors
>For instance dog and puppy the vectors are not identical but the <b><span style='color: #FFD700'>values in the dimensions should be close enough</span></b>.
>
>In summary we want to <b><span style='color: #FFD700'>capture the context of a word</span></b> (*we do not use words individually but with others that gives us context on what word to use next*)

And similar to our document representation, it must be:
- **A fixed size**
- **Numerical**
# Word Embeddings
---
>[!info] Word embeddings are typically trained without a bias term

>[!info] A word embedding can be trained using a non annotated dataset
>Just text is enough.
## Sparse Word Embeddings

>[!failure] Technically TF-IDF, BoW etc can be your word embeddings
>But they are <b><span style='color: var(--mk-color-red)'>bad ones because word similarity is dependent on document appearence</span></b>.

The main idea is to not look at words independently but <b><span style='color: #FFD700'>look at set of words in a specific context of another word</span></b>.

>[!tldr] Context
>A context of a word is a <b><span style='color: #FFD700'>small window</span></b> ($w$) that <b><span style='color: #FFD700'>surrounds this word</span></b> (*the words before & after it*).
### Co-Occurrence Vectors

Also known as <b><span style='color: #87CEEB'>term-context matrix</span></b>, here:
- Our **row** denotes the word
- Our **column** denotes the words within the context of this particular word for that row

So a cell $c_{i, j}$ refers to the <b><span style='color: #FFD700'>number of times</span></b> the word $j$ <b><span style='color: #FFD700'>appears in the context</span></b> of word $i$.

>[!example] Example of a co-occurrence vector
>
>|                     | $w_{1}$ | $\dots$ | $w_{\vert V \vert}$ |
| :-----------------: | :-----: | :-----: | :-----------------: |
|       $w_{1}$       |    1    |   ...   |          2          |
|      $\vdots$       |   ...   |  ....   |         ...         |
| $w_{\vert V \vert}$ |    2    |   ...   |          0          |
>
>So this means that word $w_{\vert V \vert}$ appears in the context of word $w_{1}$ 2 times for **all occurrences of word** $w_{1}$.

So then we can take our <b><span style='color: #FFD700'>row as our word vector</span></b>.

>[!question] Won't it be bad because we are using the small window
>Actually this is alright, we are doing this over all words that appear in the document so overall we can have a good representation of the context of the word based on its surrounding words.

>[!failure] The problem with our current approach is that raw counting is skewed
>It is what [[Year 3/Sem 2/CS4248 - Natural Language Processing/Text Classification.md#Term Frequency - Inverse Document Frequency|TF-IDF]] is trying to solve, because certain <b><span style='color: var(--mk-color-red)'>non discriminative words</span></b> (*"the"*) <b><span style='color: var(--mk-color-red)'>appear very frequently</span></b>. This causes all words context to contain a high count of these words.

A **better way to count** is by using <b><span style='color: #87CEEB'>pointwise mutual information</span></b> (*PMI*). It asks <b><span style='color: #FFD700'>does 2 words co-occur more than if they were independent</span></b>.

$$
PMI(w_{i}, w_{j}) = \log \frac{P(w_{i}, w_{j})}{P(w_{i}) P(w_{j})}
$$
Where:
- $P(w_{i}, w_{j})$ is the number of times these 2 tokens (*words*) appear in the **same context**
- $P(w_{i})$ is the number of times we see this token in the document (*just the count of this word*)

>[!warning] Sadly PMI can be less than 0 but there is no good intuition for negative values
>So typically we will use <b><span style='color: #87CEEB'>positive pointwise mutual information</span></b> (*PPMI*), which just takes the max between PMI and 0. 
>
>$$
> PPMI(w_{i}, w_{j}) = max \left(\log \frac{P(w_{i}, w_{j})}{P(w_{i}) P(w_{j})}, 0 \right)
>$$

>[!tldr] Mutual Information (MI)
>$$
>I(X, Y) = H(X) - H(X \vert Y)
>$$
>
>So this entire formula is actually [[Year 2/Sem 1/CS2109S - Introduction to AI & Machine Learning/Introduction to Machine Learning & Decision Trees.md#Evaluating an Attribute|entropy]]. It means that what is the reduction in uncertainty for when the word $X$ is alone compared to when it has seen $Y$.
>
>So the greater the reduction the more context $Y$ gives to $X$.
>
>But for this we are computing for all possible outcomes of $X$ and $Y$ 

There is still 1 thing to address and that is **rare words**. We can use previous techniques discussed by <b><span style='color: #FFD700'>raising the context probabilities</span></b> using [[Year 3/Sem 2/CS4248 - Natural Language Processing/N-Gram Language Models.md#Smoothing|smoothing]].

>[!fail] However we still have a sparse vector
>This co-occurrence vector is still a $\vert V \vert \times \vert V \vert$ in size and typically PPMI word vectors most of the entries are 0 (*unless you did smoothing*).
## Dense Word Embeddings

You can think of it as compacting a sparse word embeddings by <b><span style='color: #FFD700'>utilising the dimensions better</span></b>.

The idea is to <b><span style='color: #FFD700'>find the right "context"</span></b> (*some property*) to be used as our dimensions.

>[!success] Practical benefits of dense vectors
>- More convenient features as there are <b><span style='color: #98FB98'>less weights to tune, less risk of overfitting</span></b>
>- <b><span style='color: #98FB98'>Generalize better</span></b> than features derived from counts
>- <b><span style='color: #98FB98'>Better capture synonymy</span></b> than sparse vectors

Typically a dense vector is:
- Around 100 to 1000 entries
- Most to all vector elements are non-zero

>[!fail] The only downside is that it is not easily interpretable

There are many popular techniques to compress this vector:
- Singular value decomposition
- Brown clustering
- Neural network-based methods (*Word2Vec*)
### Word2Vec

<b><span style='color: #87CEEB'>Word2Vec</span></b>, interestingly <b><span style='color: #FFD700'>learns embeddings as part of the process of word prediction</span></b> (*by product of word prediction*).

>[!info] Another word embedding model similar to Word2Vec is GloVe

It uses 1 of the **2 algorithms**:
1) **Continuous bag of words** (*CBOW*)

So here <b><span style='color: #FFD700'>given the context</span></b> (*not the middle word*) <b><span style='color: #FFD700'>predict the center word</span></b>. And typically our context window size is around 5.

It is a <b><span style='color: #98FB98'>faster method to train a word embedding</span></b> (*because there are very little training samples*).

2) **Skip-gram**

It is the opposite of CBOW where now <b><span style='color: #FFD700'>given the center word, can you predict the context</span></b> (*does not matter if the word is to the left or right*). And typically our context window size is around 10.

It is <b><span style='color: var(--mk-color-red)'>slower</span></b> but it is <b><span style='color: #98FB98'>better if there are infrequent words</span></b>.

>[!note] CBOW & Skip-gram is not used for actual word prediction or text generation

There are some things which will not be covered but it is good to know:
- **Training**
	- Hierarchical SoftMax: better for infrequent words
	- Negative sampling: better for frequent words, better with low dimensional vectors
- **Sub-sampling of frequent words**
	- Can improve both accuracy and speed for large data sets (useful values are in range 1e-3 to 1e-5)
- **Dimensionality of the word vectors**
	- Usually more is better, but not always
#### Basic Setup

![[Word2Vec Basic Setup.png|center]]

Ok it might seem a lot but lets break down part by part:
- The **left most** vector is your **word input**, it is <b><span style='color: #FFD700'>one-hot vector</span></b> with all 0s except for that word itself (*which is 1*)
- The **blue vector** is known as the <b><span style='color: #87CEEB'>input embedding</span></b> ($V \in R^{\vert V \vert \times d}$), *this just means matrix V of some size*) which is just a <b><span style='color: #FFD700'>representation of a specific word</span></b>
- The **green vector** is known as the <b><span style='color: #87CEEB'>output embedding</span></b> ($U \in R^{d \times \vert V \vert}$), it is a <b><span style='color: #FFD700'>matrix representation of the words context</span></b> (*the context of every word*).

>[!important] The input and output embedding is learnt by the neural network
>Therefore there are <b><span style='color: #FFD700'>double the number of training parameters</span></b> because there are 2 embeddings.
>
>All the values inside $U$ and $V$ are all <b><span style='color: #FFD700'>hyperparameters</span></b>.

Now going through the steps:
1) **Multiply the one-hot vector with the input embedding**

>[!info] This is the lookup phase
>We are just looking up the word vector in our input embedding.

So what it means is that if our input, at row $i$ the value is 0 or 1, just <b><span style='color: #FFD700'>multiply the entire</span></b> $\color{#FFD700}{i}$ <b><span style='color: #FFD700'>row in the input embedding by this value</span></b>.

Then we just <b><span style='color: #FFD700'>take the non-zero row as our output</span></b> and this is our vector representation of the word.

2) **Multiply the word vector with the output embedding**

>[!info] This is the prediction phase

So now for **each row** $i$ in our word vector we <b><span style='color: #FFD700'>multiply it with the</span></b> $\color{#FFD700}{i}$ <b><span style='color: #FFD700'>row in column</span></b> 1. Then we <b><span style='color: #FFD700'>take the sum</span></b>.

Repeat this for each column in the output embedding.

3) **Apply a SoftMax on all values on the output vector & set the highest probability as 1 the rest is 0**

So now with the final output vector, we just <b><span style='color: #FFD700'>apply SoftMax on the entire vector</span></b> to convert it to a list of probabilities.

Then we do the following transformation:
- If the probability is the **largest**, set the its value to 1
- Else set it to 0

Then our resulting <b><span style='color: #FFD700'>output is another one-hot vector with the size of our vocabulary</span></b>.
#### Tuning The Embedding Vectors

Regardless on which algorithm you want to use to train (*you never use both at the same time*) the word embedding, you are doing the same thing:
- First initialise the input & output embedding to random numbers
- Then do CBOW or Skip gram to get an output
- Compute the **loss function**
- Do **backward propagation** to minimise loss and update our 2 embedding vectors

>[!note] After minimising the loss our resulting $U$ and $V$ are our word embeddings
>We can use either:
>- $U$ only
>- $V$ only (*this is the most common*)
>- Or an average of $U$ and $V$
##### CBOW Loss Function

For **CBOW**, our loss function is as follows:
$$
L= - \log P(w_{c} \vert w_{c - m}, \dots, w_{c - 1}, w_{c + 1}, \dots, w_{c + m})
$$

If we follow our [[Word Embeddings#Basic Setup|setup]], $w_{c - m}$ to $w_{c + m}$ is just doing our <b><span style='color: #FFD700'>"lookup" and then summing them together</span></b> (*we can also average it*):

$$
w_{c - m}, \dots, w_{c - 1}, w_{c + 1}, \dots, w_{c + m} = \sum_{-m \le j \le m, j \neq 0} v_{c + j} = \tilde{v}
$$
Where:
- $v_{i}$ is the **row in our input embedding**

We can simplify the loss as:

$$
L = - \log P(u_{c} \vert \tilde{v})
$$
Now we just need to know how to **compute the probability** and we can us ethe <b><span style='color: #FFD700'>SoftMax function</span></b>:
$$
P(u_{c} \vert \tilde{v}) = \frac{e^{(u_{c}^{T}  \cdot \tilde{v})}}{\sum{_{j = 1}^{\vert V \vert} e^{(u_{j}^{T}  \cdot \tilde{v})}}}
$$
Where:
- $u_{j}^{T}$ or $u_{c}^{T}$ is just the column of our output embedding where $c$ is for our center word or for word $j$

It might look confusing but essentially this is our [[Word Embeddings#Basic Setup|step 2 and 3 in our setup]]. The **numerator** is the <b><span style='color: #FFD700'>value of our output vector for the center word</span></b>, the **denominator** is just the sum of the output vector.
##### Skip Gram Loss Function

For **skip grams** it is essentially the same just that now we are <b><span style='color: #FFD700'>adding up the log probabilities for the words in the context</span></b>.

$$
L= - \log P(w_{c - m}, \dots, w_{c - 1}, w_{c + 1}, \dots, w_{c + m} \vert w_{c})
$$
Then **simplifying it**:
$$
L = - \sum_{-m \le j \le m, j \neq 0} \log P(u_{c + j} \vert v_{c})
$$
Now we just need to know how to **compute the probability** and we can use the <b><span style='color: #FFD700'>SoftMax function</span></b>:
$$
P(u_{c + j} \vert \tilde{v}) = \frac{e^{(u_{c + j}^{T}  \cdot \tilde{v})}}{\sum{_{j = 1}^{\vert V \vert} e^{(u_{j}^{T}  \cdot v_{c})}}}
$$

So same thing the **numerator** is the <b><span style='color: #FFD700'>value of our output vector for the context word</span></b> ($u_{c+j}$), the **denominator** is just the sum of the output vector.

>[!tldr] Intuition for both of these loss functions
>Look at how we compute the probability, our goal is to make the <b><span style='color: #98FB98'>probability as high as possible</span></b> (*because log (1) = 0*).
>
>This means that our <b><span style='color: #FFD700'>dot product in the numerator has to be large</span></b>.
>
>And if they are large means that **both vectors** $u_{c + j}$ and $v_{c}$ (*for skip gram*) are <b><span style='color: #FFD700'>similar</span></b> (*same for CBOW if the combination of all the vectors is the same as the center vector*).
>
>And this leads back to what [[Year 3/Sem 2/CS4248 - Natural Language Processing/Text Classification.md#Cosine Similarity|cosine similarity]] does, **same vectors** (*maybe different in magnitude only*) will product the <b><span style='color: #FFD700'>maximum possible dot product</span></b>.

>[!info] So it does not matter if we use $V$ or $U$, 2 words which are similar in context will have similar embeddings
>Why lets say we use the **input vector**, then for **skip gram** lets take **apple & orange which are used in similar context** will need to <b><span style='color: #98FB98'>multiply with the output vectors to get high probabilities for the context for both</span></b> of them.
>
>If we used **CBOW**, lets say we have **context with the same words but differ by apple & orange** is used to compute the center word (*same center word*) must be somewhat <b><span style='color: #98FB98'>similar because it maximises the probability of the center word</span></b>.
>
>Same intuition if we used the output embedding.
#### Negative Sampling

The algorithm to <b><span style='color: var(--mk-color-red)'>train a word embedding is actually slow</span></b>. This is because of the SoftMax function where we need to <b><span style='color: #FFD700'>sum over the entire vocabulary</span></b> (*denominator*).

To **improve efficiency**, we do something called <b><span style='color: #87CEEB'>negative sampling</span></b>. So <b><span style='color: #FFD700'>instead of updating all the weights we take a smaller subsample</span></b>.

And we will <b><span style='color: #FFD700'>pick informative samples</span></b> (*rare words*) more often than uninformative ones (*common ones*). To <b><span style='color: #FFD700'>increase the probability of rare words</span></b>.

>[!question] Why not just check rare words?
>This requires some <b><span style='color: var(--mk-color-red)'>checking and it takes a long time</span></b>. Just doing a random sampling will be faster but we <b><span style='color: var(--mk-color-red)'>might sample wrong negative words</span></b>.

>[!goal] Convert our training from a word prediction task to a binary classification task

>[!note] Here we will talk about skip gram negative sampling
>For CBOW negative sampling is not the same but very similar.

Lets take some data samples as shown:

|        x         |  y  |
| :--------------: | :-: |
|  (movie, watch)  |  1  |
|  (movie, funny)  |  1  |
| (movie, netflix) |  1  |
|   (movie, nlp)   |  0  |
| (movie, nimble)  |  0  |
Here we set out context window to be $m = 2$ where:
- $y = 1$ meaning it is a <b><span style='color: #98FB98'>positive sample</span></b>, the 2 words **are of context** with one another (*within the window*)
- $y = 0$ meaning it is a <b><span style='color: var(--mk-color-red)'>negative sample</span></b>, the 2 words are **not of context** (*randomly sample from words that are out of the context*)

>[!note] The first token is the word, the second token is the context in our tuple

So **how do we choose these negative samples**:
$$
P_{\alpha}(w_{i}) = \frac{\text{Count}(w_{i})^{\alpha}}{\sum_{w \in V} \text{Count}(w_{i})^{\alpha}}
$$
Where:
- $P_{\alpha}(w_{i})$ is the probability that the word $w_{i}$ is selected as a negative sample
- $\alpha$ is known as a <b><span style='color: #87CEEB'>weighted unigram frequency</span></b> which is just some smoothing parameter, it typically $0 \lt \alpha \le 1$ (*ensures that the probability for common words gets reduced*)

>[!note] Typically for positive samples we will sample $2m$ while for negative samples it will be $2mk$ where $k$ is some parameter you can choose
>But **do not set k to be too large**, this is because the <b><span style='color: var(--mk-color-red)'>negative samples are more influential in the prediction task and thus the positive samples do not play a part</span></b> (*around 2 - 5 for large text and 5 - 20 for small text, why because smaller text we might not have the data or positive information*).
>
>So we need a balance between positive and negative guidance.

So after we sample to form some mini batch we can formulate a **loss function to say, negatives samples predict 0 else 1**:
$$
L = - \left[ \sum_{(c,m) \in B_{+}} \log P(+ \vert c, m) + \sum_{(c,m) \in B_{-}} \log (1 - P(+ \vert c, m)) \right]
$$
Where:
- $B_{+}$ is the samples that are in the positive class
- $B_{-}$ is the samples that are in the negative class

Then to **compute the probability**:
$$
P(+ \vert c, m) = \frac{1}{1 + e^{- u_{m}^{T} \cdot v_{c}}}
$$
Where:
- $v^{T}_{m}$ is the transpose matrix of the output embedding for word $m$
- $v_{c}$ is the input embedding for the word $c$

Then we can **simplify our loss function**:
$$
L = - \left[ \sum_{(c,m) \in B_{+}} \log \sigma(u^{T}_{m}v_{c}) + \sum_{(c,m) \in B_{-}} \log \sigma(- u^{T}_{m}v_{c})  \right]
$$
Where:
- $\sigma$ is the sigmoid function

We want $\log \sigma(u^{T}_{m}v_{c})$ to be <b><span style='color: #98FB98'>closest to 1 as possible</span></b> (*this is our positive class*) and for $\log \sigma(- u^{T}_{m}v_{c})$ to be <b><span style='color: #98FB98'>closest to 0</span></b> (*these are our negative classes*).

Then we can do <b><span style='color: #FFD700'>backward propagation on the selected words</span></b>. 
#### Practical Consideration & Limitations For Word2Vec

First when we are **preprocessing** the raw data, these choices matter:
- Choice of tokenizer
- Case folding (*case folding is not done*)
- Stemming / lemmatization (*stemming is usually not done*)
- Stopword removal (*stopword removal is not done*)
- Cross sentence contexts (*don't add cross-sentence contexts when you have insufficient data*)

The **parameters** as well (*typically in negative sampling*), we learnt that these matter:
- Number of negative samples ($k$)
- Window size (*m*)

>[!fail] Cannot represent phrases
>This is because we have <b><span style='color: var(--mk-color-red)'>not represent the ordering</span></b> of our text.

>[!fail] Cannot detect polarity of the word or its semantics
> And the reason is because the <b><span style='color: var(--mk-color-red)'>context that the word was used in is the same</span></b>. So words like "scarry" and "funny", though they are different, they can be similar if the context is the same.

>[!fail] Cannot handle polysemy
>Which is multiple meaning of the same word which in Word2Vec it just averages out.

>[!fail] Cannot handle part of speech
>Same words used as a noun, verb, etc.

>[!fail] The embedding is heavily reliant on the context of the dataset
>If we have a dataset that is about science and you want to use it for literature then the context will be different.
## Desired Properties

For our word embeddings we want some <b><span style='color: #87CEEB'>linear substructures</span></b>.

>[!tldr] Linear substructures
>Essentially our vector addition and multiplication can yield semantic relationships.

Some examples are:
- **Verb tense** (*walking, walked, swam, swimming*)
- **Adjective comparatives & superlatives** (*fast, faster, fastest*)

>[!note] If you want to get these semantic relationships, we cannot use stemming

>[!example] Example of such a semantic relationship
> ![[Word Embedding Semantic Relationships Example.png|center|250]]
> So here if we take the vector of king minus the man and then add a women we should get the vector for queen.


