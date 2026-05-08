---
Title: N-Gram Language Models
Date Created: 29-January-2026
Last Updated: 28-April-2026
Tags:
  - CS4218
  - AI/NLP/N-Grams
---

# Language Models
---
Language models are fundamental for many NLP task:
- Speech recognition
- Spelling correction
- Gramma correction
- Machine translation

>[!question] So given 2 sentences output which makes more sense?
>1) "The role was played by an across famous for her comedic timing"
>2) "The role was played by an actress famous for her comedic timing"

We naturally feel that sentence 2 makes more sense. So in language models we are trying to <b><span style='color: #FFD700'>assign higher probability to a sentence, phrase or word that closely matches what we humans feel is more logical</span></b>.

So in our question above, $P(S_{1}) < P(S_{2})$ & thus our model will output sentence 2.
## Sentence Probabilities

Or in other words  the probability for a sequence of words.

>[!note] Whether it is words or sub words it does not change the meaning they are both fundamentally the same

In the concept of language models there are **2 basic notions of probability**:
1) Probability of a <b><span style='color: #FFD700'>sequence of words</span></b>, $P(W) = P(w_{1}, w_{2}, \dots, w_{n}) \leftarrow$ Joint probability
2) Probability of <b><span style='color: #FFD700'>an upcoming word</span></b> ($w_{n}$), $P(w_{n} | w_{1}, w_{2}, \dots, w_{n - 1}) \leftarrow$ Conditional probability 

>[!important] All language models just boils down to finding this probability

To solve these probabilities we can use the [[Year 3/Sem 1/CS3263 - Foundations of Artificial Intelligence/Probabilistic Graphical Modeling.md#Conditional Probability|chain rule]] which can <b><span style='color: #FFD700'>convert a join probability distribution into conditional probabilities</span></b>.

The **chain rule** goes as such:
$$
P(w_{1}, w_{2}, \dots w_{n}) = P(w_{n} \vert w_{1}, w_{1}, \dots, w_{n - 1}) \times P(w_{1}, w_{2}, \dots, w_{n - 1})
$$
We can repletely apply chain rule on the 2nd term:
$$
P(w_{1}, w_{2}, \dots w_{n}) = P(w_{n} \vert w_{1}, w_{1}, \dots, w_{n - 1}) \times P(w_{n - 1} \vert w_{1}, w_{1}, \dots, w_{n - 2}) \times P(w_{1}, w_{2}, \dots, w_{n - 2})
$$
Do this until we are left with:
$$
P(w_{1}, w_{2}, \dots w_{n}) = P(w_{n}\vert w_{1}, w_{1}, \dots, w_{n - 1}) \times \dots \times P(w_{2} \vert w_{1}) \times P(w_{1})
$$

>[!info] This can also be applied to conditional probability as well
>>[!example] Example of applying chain rule on a conditional probability
>>$$
> P(w_{5}, w_{4}, w_{3} \vert w_{2}, w_{2}) = P(w_{5} \vert w_{4}, w_{3}, w_{2}, w_{1}) \times P( w_{4} \vert w_{3}, w_{2}, w_{1}) \times P(w_{3} \vert w_{2}, w_{1})
> >$$

**Simplifying** the chain rule formula it will become:
$$
P(w_{1}, \dots, w_{n}) = \prod^{N}_{i = 1} P(w_{i} \vert w_{1 : i - 1})
$$
Where:
- $w_{1 : i - 1}$ means from the first word to the $i^{th} - 1$ word
## Evaluating Language Models

A **good model** will assign <b><span style='color: #FFD700'>high probabilities to frequently occurring sentences</span></b> while assigning rare ones a lower probability.

There are **2 basic approaches to compare 2 language models**:
1) Extrinsic evaluation
2) Intrinsic evaluation
### Extrinsic Evaluation

This methods involves some sort of <b><span style='color: #FFD700'>downstream task</span></b> (*spell checker, speech recognition*).

Then we run each language model to <b><span style='color: #FFD700'>execute this downstream task & compare the results</span></b>.

Alternatively we can do <b><span style='color: #FFD700'>user-driven comparisons</span></b> which is just letting people decide which is better just by using it.

>[!fail] Can be very expensive to do

>[!fail] Can be very time consuming to do
### Intrinsic Evaluation

Here we use some sort of <b><span style='color: #FFD700'>test corpus to evaluate the model</span></b>. This requires an intrinsic metric to compare the LMs, which is known as <b><span style='color: #87CEEB'>perplexity</span></b> (*& there are other metrics as well*).

There are **3 core steps**:
1) Train the language model on a **training corpus**
2) Tune the parameters using a **development corpus**
3) Then evaluate on the test corpus to compute the **evaluation metric**

>[!into] Typically a common corpus breakdown will be a 80/10/10 split

>[!success] Cheaper to test

>[!success] Faster to test
#### Perplexity

In a simpler term, perplexity is <b><span style='color: #FFD700'>how sure the model is in its answer</span></b>. So we are <b><span style='color: #98FB98'>trying to minimise perplexity</span></b> which results in maximising probability.

To **compute perplexity**, the formula is as follows:
$$
PP(W) = P(w_{1}, \dots, w_{n})^{-\frac{1}{n}} = \sqrt[N]{\frac{1}{P(w_{1}, \dots, w_{n})}}
$$
Where:
- The $- 1/ n$ or the root of $n$ is the normalisation

>[!info] We need normalisation due to long sentences such that their perplexity score is not inflated as compared to shorter sentences

>[!note] We can also apply the chain rule to the joint probability portion in the formula

There are **2 ways in which perplexity will be high**:
1) Many sequences are <b><span style='color: #FFD700'>frequent in the training corpus but rare in the test corpus</span></b>. This results in very few high probabilities over the test corpus
2) Many sequences are <b><span style='color: #FFD700'>rare in the training corpus but frequent in the test corpus</span></b>. This results in many low probabilities over the  test corpus

>[!warning] The joint probability can be very small & might risk arithmetic underflow
>In a large corpus $P(w_{1}, \dots, w_{n})$ can be very small <b><span style='color: var(--mk-color-red)'>due to many words</span></b>.
>
>So we can introduce <b><span style='color: #FFD700'>logarithms</span></b> to prevent this.
>
>So now the formula to **compute perplexity using logarithms** will be:
>$$
 PP(W) = e^{\ln PP(W)}
> $$
> 
> Then all we need is to compute $\ln PP(W)$
> 
> $$
  -\frac{1}{N} \ln P(w_{1}, .., w_{n}) = - \frac{1}{N} \ln \prod^{N}_{i = 1} P(w_{i} \vert w_{1 : i - 1}) = - \frac{1}{N} \sum^{N}_{n = 1}\ln P(w_{n} \vert w_{1}, .., w_{n - 1})
> $$
# N-Gram Language Models
---
The idea of n-grams is that instead of taking the whole sentence we <b><span style='color: #FFD700'>calculate probabilities using n-gram counts</span></b>.

>[!tldr] N-gram observations
>In general **larger n-grams** generally <b><span style='color: #98FB98'>generate better sentences</span></b>, are <b><span style='color: #98FB98'>more grammatical</span></b> but is <b><span style='color: var(--mk-color-red)'>often incoherent because long n-gram sequences are rare</span></b>.

>[!info] N-grams
>They are a <b><span style='color: #FFD700'>sequence of words of length n</span></b>.

To compute a **n-gram probability** we use a formula the <b><span style='color: #87CEEB'>maximum likelihood estimation</span></b> (*MLE*):
$$
P(w_{n} \vert w_{1 : n - 1}) = \frac{\text{Count}(w_{1:n-1},w_{n})}{\sum_{w} \text{Count}(w_{1:n-1},w)} = \frac{\text{Count}(w_{1:n})}{\text{Count}(w_{1:n-1})}
$$
Where:
- $\sum_{w} \text{Count}(w_{1:n-1},w)$ is essentially the count of a sequence of words $w_{1}$ to $w_{n - 1}$ & every single word $w$ that follows after it.
- $\text{Count}(w_{1 : n})$ is the count of sequences of words 1 to n.

>[!info] We can simplify the summation into just a count from the first to the n - 1 word because we do not care what the last word can be
>The sum of the first to the n-1 word & all next possible words = sum of the first to the n-1 word.

>[!success] This solves the problem for long sequences
> In normal language models it takes in a <b><span style='color: var(--mk-color-red)'>long sequence of words but as it get longer the chances of it appearing is near 0</span></b>.
> 
> So when we want to [[Year 3/Sem 2/CS4248 - Natural Language Processing/N-Gram Language Models.md#Sentence Probabilities|compute sentence probability]] it will eventually be 0 or very close to it.
> 
> This is the <b><span style='color: #87CEEB'>Markov assumption</span></b> which n-grams is based on. It just <b><span style='color: #FFD700'>limits the look back of the number of words to n</span></b> as compared to starting from the 1st word.

>[!fail] But we are limited to the amount of information from the past to make good predictions
>So they are not very good in text generation.

In general there are:
- Unigrams (*1-gram*)
- Bigrams (*2-gram*)
- Trigram (*3-gram*)
- 3-gram ... 5 gram (*common models*), and more

To compute the MLE for any n-gram the formula is which is the same as what was shown above:
$$
P(w_{n} \vert w_{1}, \dots, w_{n - 1}) \approx P(w_{n} \vert w_{n - N + 1 : n - 1}) = \frac{\text{Count}(w_{n - N + 1 : n})}{\text{Count}(w_{n - N + 1 : n - 1})}
$$
>[!info] The lager the n the more data is required, to prevent seeing 0 counts

>[!important] If the corpus is already split into n-gram segments then do be wary of double counting
> Assuming we are given a bigram count as such:
> 
> |     Bigram     | Count |
| :------------: | :---: |
| alice accident |   5   |
| saw alice  |   5   |
| alice the  |  15   |
|   alice saw    |  20   |
|    saw the     |  25   |
|  accident saw  |   1   |
| accident alice |   2   |
>
>And we want to compute the $\text{Count}(alice)$. Then we cannot take counts of bigrams "saw alice", "accident alice" since we split into bigrams. So our sentence can be "saw alice the" when when split into segments of 2 words will cause double counting.
## Smoothing

An issue with languages is that it can be open or closed. **Close vocabulary** means that the number of words are fixed thus no unknown words.

The problem comes for **open vocabulary** (*more in line with languages*) where the <b><span style='color: var(--mk-color-red)'>words might not appear in the vocabulary</span></b> (*the training corpus*).

>[!fail] This means that potentially the word count might be 0
>Meaning computing the <b><span style='color: var(--mk-color-red)'>probability will just result to 0</span></b>.

There are ways to **handle OOV words**:
1) Special token for OOV words (*convert into a \<UNK\> token and use this to compute the probability*)
2) [[Year 3/Sem 2/CS4248 - Natural Language Processing/Strings & Words.md#Sub Word Based|Sub word tokenization]]
3) <b><span style='color: #87CEEB'>Smoothing</span></b>

The idea of smoothing is to <b><span style='color: #FFD700'>avoid assigning 0 probabilities to unseen n-grams</span></b>. To do this we can <b><span style='color: #FFD700'>"move" some probability mass from the frequent n-grams</span></b> to unseen ones.

>[!info] This is also called discounting
### Laplace Smoothing

A very basic way is to just <b><span style='color: #FFD700'>add 1 to all counts</span></b>. This is also known as <b><span style='color: #87CEEB'>add-1 smoothing</span></b>.

>[!question] Is this naive way good?
>Well it does <b><span style='color: #98FB98'>remove 0 probabilities</span></b> for OOV words but by adding 1, the <b><span style='color: var(--mk-color-red)'>probability of those that were non-zero will get changed a lot</span></b>. So too much probability has been moved.
>

A more generalised way is called the <b><span style='color: #87CEEB'>add-k smoothing</span></b> or <b><span style='color: #87CEEB'>generalised Laplace smoothing</span></b>.

Typically $k$ will be <b><span style='color: #FFD700'>greater than 0 but less than or equal to 1</span></b>. This is to ensure that the final probabilities do not change drastically.

With generalised Laplace smoothing the formula to **compute the probability** will be:
$$
P_{\text{add-k}}(w_{n} \vert w_{n - 1}) = \frac{\text{Count}(w_{n-1}, w_{n}) + k}{\text{Count}(w_{n-1}) + kV}
$$
Where:
- $V$ is the length of the vocabulary 

>[!important] OOV words are all considered as the same word, using the \<UNK\> token
>So our vocabulary will have all the seen words + an unknown word token.
### Backoff & Interpolation

#### Backoff

It is another method for smoothing, the intuition here is to <b><span style='color: #FFD700'>use less context if required</span></b>. In other words, lets say a trigram cannot be found in the dataset, then we can use he bigram probability.

>[!Example] Example of backoff
>As mentioned for example if $P(w_{n} \vert w_{n-2}, w_{n - 1})$ is not in the dataset we can use bigrams, $P(w_{n} \vert w_{n - 1})$ & if it is insufficient meaning a 0 probability again use a unigram probability $P(w_{n})$
#### Interpolation

For interpolation it is a bit similar to backoff where we compute the probabilities from n-gram down till bigrams. But we now <b><span style='color: #FFD700'>learn weights</span></b> ($\lambda_{i}$) from data for each of the probabilities.

>[!success] In practice it is better than backoff

The **formula for a simple interpolation** will be:
$$
P(w_{n} \vert w_{n - k}, w_{n - k + 1}, \dots,  w_{n - 1}) = \lambda_{1}P(w_{n}) + \lambda_{2}P(w_{n} \vert_{n - 1}) + \dots + \lambda_{k} P(w_{n} \vert w_{n - k}, w_{n - k + 1}, \dots,  w_{n - 1})
$$
Where:
- $k$ is just some arbitrary number of words that were already seen
- $\sum_{i} \lambda_{i} = 1$ 

We can also make $\lambda_{i}$ be **conditional on context** (*add normalisation*):
$$
P(w_{n} \vert w_{n - k}, w_{n - k + 1}, \dots,  w_{n - 1}) = \lambda_{1}(w_{n - k}, \dots,  w_{n - 1})P(w_{n}) + \lambda_{2}(w_{n - k}, \dots,  w_{n - 1})P(w_{n} \vert_{n - 1}) + \dots
$$
>[!note] All that needs to be done is to tune $\lambda$ till we maximise the probability of the sequence of words
### Kneser-Ney Smoothing

The idea is <b><span style='color: #87CEEB'>absolute discounting interpolation</span></b>. The **formula to compute the probability** using Kneser-ney smoothing is:
$$
P_{KN}(w_{n} \vert w_{n - 1}) = \frac{max[\text{Count}(w_{n - 1}, w_{n}) -d, 0]}{\text{Count}(w_{n - 1})} + \lambda(w_{n-1}) P_{continuation}(w_{n})
$$
Where:
- $\lambda(w_{n-1}) P_{KN}(w_{n})$ is the interpolation portion
- $d$ is some fixed variable usually $0 \lt d \lt 1$ to remove from all non-zero bigram counts

>[!note] Here we only show going from bigram to unigram
>But in **general**:
>$$
>P_{KN}(w_{n} \vert k) = \frac{max[\text{Count}(w_{n - k}, w_{n}) - d, 0]}{\text{Count}(k)} + \lambda(k) P_{continuation}(w_{n} | k - 1)
>$$
#### Absolute Discounting

So similarly to [[Year 3/Sem 2/CS4248 - Natural Language Processing/N-Gram Language Models.md#Laplace Smoothing|Laplace smoothing]] but instead of adding we <b><span style='color: #FFD700'>subtract by some value</span></b> $d$. You can think of this as removing some probability from existing ones for OOV n-grams.

The **intuition to subtract** is that:
- If $\text{Count}(w_{n - 1}, w_{n})$ is large then the count is hardly affected
- If $\text{Count}(w_{n - 1}, w_{n})$ is small than the count is not useful to begin with.

The `max` is in the formula to <b><span style='color: #FFD700'>avoid any negative probabilities</span></b>.

>[!info] A common value for $d = 0.75$
#### Interpolation in Kneser-Ney Smoothing

In [[Year 3/Sem 2/CS4248 - Natural Language Processing/N-Gram Language Models.md#Interpolation|basic interpolation]] we use the $P(w_{n})$ for the unigram probability. But here we use $P_{continuation}(w_{n})$ (*when we hit the unigram*), which calculates <b><span style='color: #FFD700'>how likely the word is to appear as a novel continuation</span></b> (*appear after a particular word*).

>[!question] Why do we not use $P(w_{n})$
>If we used the probability then we are just doing <b><span style='color: #87CEEB'>absolute discounting</span></b>, where we take the <b><span style='color: #FFD700'>counts of the low level n-grams</span></b>.
>
> Assume we have 2 words "glasses" & "Kong". Most of the time "Kong" is preceded by "Hong". Whereas glasses is preceded by many other words.
> 
> So if we have a corpus with a lot of words "Hong Kong" instead of glasses then the <b><span style='color: var(--mk-color-red)'>probability that "Kong" gets selected will be higher than "glasses" even though glasses is more commonly used</span></b>.
> 
> This can <b><span style='color: var(--mk-color-red)'>causes sentences formed to be wrong or incoherent</span></b>.

When:
- $P_{continuation}(w_{n})$ is **high** it means there are <b><span style='color: #FFD700'>many words</span></b> ($w'$) which form the existing bigram $w'w$
- $P_{continuation}(w_{n})$ is **low** it means there are <b><span style='color: #FFD700'>only few words</span></b> ($w'$) which form the existing bigram $w'w$

To **compute** $P_{KN}(w)$:
$$
P_{continuation}(w_{n} \vert k) = \frac{\vert\{w' : \text{Count} (w', k, w_{n}) \gt 0\} \vert}{\vert\{ (u, k, v) : \text{Count} (u, k, v) \gt 0\} \vert} + \lambda(k) P_{continuation}(w_{n} \vert k -1)
$$
Where:
- The numerator is the <b><span style='color: #FFD700'>number of words that form an existing n-gram</span></b> $w'k w$
- The denominator is the <b><span style='color: #FFD700'>total number of existing n-grams normalised</span></b>
- $u$ and $v$ are just any single word that comes before and after the range of words $k$

If we are dealing with bigrams $k$ will be empty so the denominator is all bigrams essentially.

>[!important] For the highest level n-gram we use the normal count, subsequently when we compute lower level n-grams we use the formula above

The last part is to compute $\lambda (k)$ or any of these <b><span style='color: #87CEEB'>normalising factors</span></b>. To **compute this** (*for the highest level n-gram*):
$$
\lambda(k) = \frac{d}{\text{Count}(k)} \times \vert\{ w' : \text{Count} (k, w') \gt 0 \} \vert
$$
Where:
- $d$ is the fixed value during [[Year 3/Sem 2/CS4248 - Natural Language Processing/N-Gram Language Models.md#Absolute Discounting|discounting]]
- $\text{Count}(w_{n} - 1)$ is the normalized discount

Subsequent **lower-level n-grams**:
$$
\lambda(k) = \frac{d}{\vert\{ (u, k, v) : \text{Count} (u, k, v) \gt 0 \} \vert} \times \vert\{ w' : \text{Count} (u, k, w') \gt 0 \} \vert
$$
Where:
- The denominator is the unique count of all possible pair of words where k is in the middle
- The multiplier is the unique count of all words
