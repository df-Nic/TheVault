---
Title: Transformers
Date Created: 03-April-2026
Last Updated: 17-April-2026
Tags:
  - CS4248
  - AI/ML/NN/Transformers
---
# Transfer Learning
---
With our **language model** trained we were able to **capture knowledge** of our training corpus. But now we want it to do **more task dependent things**.

So we need to <b><span style='color: #FFD700'>build a question answer model</span></b> & this is where <b><span style='color: #87CEEB'>transfer learning</span></b> (*fine-tuning*) comes in.

![[Transfer Learning For NLP Models.png|center]]

Essentially we can just <b><span style='color: #FFD700'>take some off the shelf language model</span></b> & <b><span style='color: #FFD700'>train it on a more specific task using an annotated dataset</span></b>.

>[!abstract] Freezing Parameters
>You might have heard the term <b><span style='color: #87CEEB'>freezing</span></b> which is essentially <b><span style='color: #FFD700'>locking the pre-trained model's parameters so it does not get updated during fine-tuning</span></b>. Which in fine-tuning some people might do that.
## Contextualised Word Embeddings

Now the issue is that up <b><span style='color: var(--mk-color-red)'>till now our word embeddings are context-independent</span></b>. Meaning there is <b><span style='color: var(--mk-color-red)'>only 1 vector to represent the word</span></b>. So there is this <b><span style='color: var(--mk-color-red)'>problem of polysemy</span></b>.

>[!question] Why is this an issue?
>Take for instance this sentence "In the bright light, the feather was light".
>
>The word "light" means to different things. The first "light" refers to the thing that allows us to see while the second "light" refers to the weight.

So what we want is a **model** that <b><span style='color: #98FB98'>takes into context of the whole sentence & word order</span></b> and then <b><span style='color: #FFD700'>represent the word in varying embedding vectors depending on context</span></b>.

>[!warning] In [[Word Embeddings#Word2Vec|Word2Vec]] we did consider a window size but sometimes context requires the whole sentence 
### ELMo

It stands for <b><span style='color: #87CEEB'>embeddings from language model</span></b>. But instead of our vanilla RNN it uses:
- An <b><span style='color: #FFD700'>LSTM</span></b>
- It is a <b><span style='color: #87CEEB'>bidirectional-LSTM</span></b> (*Bi-LSTM*)
- Then we use <b><span style='color: #FFD700'>2 of these Bi-LSTM</span></b> (*the output of the 1st Bi-LSTM will be the input for the 2nd*)

>[!info] You can use more than 2 layers but ELMo stopped at 2 because of heavy computation

**Example of ELMo**:
![[High Level Overview of ELMo.png|center|500]]

>[!tldr] Bidirectional-LSTM
>In our RNN you call the structure is that we start at the first input then we go to the next and so on.
>
>Bidirectional-LSTM now <b><span style='color: #FFD700'>introduces backward dependencies</span></b>, so it <b><span style='color: #FFD700'>start from the last word and goes backwards</span></b>. But everything else still remains the same its just the direction.

If we look at the sample image we can see that for a particular output we **have 3 embeddings**
- The <b><span style='color: #FFD700'>uncontextualized embedding</span></b> (*the green box*) which is just the word embedding
- The <b><span style='color: #FFD700'>2 embeddings from the LSTM output</span></b>

>[!note] That the LSTM output will be just a concatenation of the forward and backward embeddings

The **simplest case will be to use the top layer** (*embedding from the 2nd layer*) but a more <b><span style='color: #FFD700'>generalised method is to use a weighed sum</span></b>:
$$
\text{embedding}_{t} = \gamma \sum^{2}_{i = 0} s_{i}h_{t}^{i}
$$
Where:
- $\gamma$ is some scaling factor
- $s_{i}$ is the normalised weights which when **sum together will be equal to 1**

>[!success] It might seem complex but its very simple to compute because everything is done through pre-training

>[!success] It has a good improvements to downstream NLP tasks
>Because now we use the context of the whole sentence.
# Transformers
---
So the **main issue with RNN** is that for <b><span style='color: var(--mk-color-red)'>very long sequences it might face vanishing or exploding gradients</span></b>.

>[!warning] LSTM does not completely solve it but it can be mitigated with a memory line

Which we solved it using [[Year 3/Sem 2/CS4248 - Natural Language Processing/Encoder & Decoder.md#Attention|attention]]. But now the next issue is that <b><span style='color: var(--mk-color-red)'>RNN are sequential</span></b>. We want to <b><span style='color: #FFD700'>process in parallel</span></b> which is what the <b><span style='color: #87CEEB'>transformer</span></b> does.

In addition **transformers uses 2  important concepts**:
1) [[Year 3/Sem 2/CS4248 - Natural Language Processing/Transformers.md#Positional Embeddings|Positional embeddings]]
2) [[Year 3/Sem 2/CS4248 - Natural Language Processing/Transformers.md#Masking|Masking]]

>[!warning] But in general transformers are hard to train
>- Complex architecture (*a lot of parameters to train*)
>- Needs large and curated datasets (*prevent overfitting*)
>- Typically require large computing infrastructure
>  
>  >[!success] So commonly we just use a pretrained encoder or transformer based LLM (*BERT, RoBERTa*) and then we can tune them if we want to
## Attention For Transformers
### Computing Attention

![[Computing Attention for Transformers.png|center|150]]

[[Year 3/Sem 2/CS4248 - Natural Language Processing/Encoder & Decoder.md#Attention|Recall]] that to **compute attention** we follow this formula:
$$
\text{Attention}(Q, K, V) = \text{SoftMax}\left(\frac{QK^{T}}{\sqrt{d_{k}}}\right)V
$$
So computing the attention for a transformer is no different just some tweaks. So there are **2 core steps**:
- <b><span style='color: #FFD700'>Compute alignment</span></b> / similarity between <b><span style='color: #FFD700'>all pairs</span></b> of input word embeddings
- <b><span style='color: #FFD700'>Adjust the word embeddings based on embedding similarities</span></b>

There are **2 types** of attention:
1) **Self**-attention (*it is the dot product on the same sequence, applied in both encoder &decoder*)
2) **Cross**-attention (*it is the dot product on a different sequence, applied to the decoder*)
#### Pre-Processing Our Matrices

**Before even computing the alignment scores**, we need to do the following:
- <b><span style='color: #FFD700'>Add the positional embedding</span></b> to the word vector (*just simply add the 2 matrices*)
- Then <b><span style='color: #FFD700'>transform this word embedding into query, key, value matrices</span></b> using their respective weight metrices.

>[!tldr] Query, key, value weights
>These are <b><span style='color: #FFD700'>tunable parameters</span></b> which can transform the word embedding into a vector which represents that word as a key, value or query (*in a high level sense*).
>
>For <b><span style='color: #FFD700'>the embedding size we do not always need to output a vector size similar to our embedding</span></b> (*it can be smaller or bigger but all must output the same size*).
#### Computing The Alignment

With that done we can finally start, looking at the image we <b><span style='color: #FFD700'>do a matrix multiplication first</span></b>, & that is our $QK^{T}$ (*size N by N where N is the number of words in the sequence*). This <b><span style='color: #FFD700'>gives us which words are relevant to which other words</span></b>.

>[!info] So what is happening in $QK^{T}$
>**Q and K** are just a <b><span style='color: #FFD700'>list of the matrix representation of query's or keys for all words</span></b>.
>
>So when doing a matrix multiplication we are going to do a <b><span style='color: #FFD700'>dot product for all pairs of words</span></b> (*more specifically between all pairs of query and key*). 

Then at the same time we also do <b><span style='color: #FFD700'>scaling</span></b> which is when we divide by $\sqrt{d_{k}}$ where $d_{k}$ is the <b><span style='color: #FFD700'>dimension of our query/key embedding</span></b>. Then we can do [[Year 3/Sem 2/CS4248 - Natural Language Processing/Transformers.md#Masking|masking]] (*just change some values to be negative infinity*).

Then we <b><span style='color: #FFD700'>apply the SoftMax function on the rows</span></b> to give us a weighted sum (*total 1 for each row*) & also to scale the values between 0 and 1.

>[!note] This final alignment is also called the scaled dot-product attention
#### Updating Our Word Embedding

**Lastly**, we do a <b><span style='color: #FFD700'>matrix multiplication on the scaled dot-product attention to the values</span></b>. And as a reminder $V$ is a list of value matrices for each word.

Recall that our alignment matrix contains scalar values and $V$ contains matrices. So when we do a matrix multiplication we will essentially be <b><span style='color: #FFD700'>doing a weighted multiplication on the value matrix</span></b>.

The result will be a matrix of matrices, which we will then <b><span style='color: #FFD700'>sum the matrices for each row</span></b>. To get our "<b><span style='color: #87CEEB'>update vector</span></b>".

Then we use this update vector and <b><span style='color: #FFD700'>add it to to the original word's embedding</span></b> (*for the row*) to <b><span style='color: #98FB98'>get a contextualised word embedding</span></b>.
### Sparse Attention

So one issues is that if we have a <b><span style='color: var(--mk-color-red)'>long sequence then we will need to compute a lot of alignment score for each pair</span></b>. So instead of computing all attention we <b><span style='color: #FFD700'>compute some of the attention</span></b>. 

>[!goal] The goal is to make the operations to be $O(N)$

Some examples to **do sparse attention** are:
- <b><span style='color: #FFD700'>Random</span></b> attention (*each word compute the attention for a fixed number of random pairs*), this is <b><span style='color: #FFD700'>like dropout & masking</span></b>
- <b><span style='color: #FFD700'>Window</span></b> attention (*compute the attention based on the context window*), like Word2Vec where the <b><span style='color: #FFD700'>words nearby are important</span></b>
- <b><span style='color: #FFD700'>Global</span></b> attention (*only compute attention for the first x number of words*), is to let the word <b><span style='color: #FFD700'>remember the earliest words</span></b>
- <b><span style='color: #FFD700'>BigBird</span></b> attention (*combine all of the 3 methods above*)

>[!abstract] There are also strategies than just sparse attention
>There is:
>- <b><span style='color: #FFD700'>Linear</span></b> attention (*approximates attention with lower-rank representation or PCA*)
>- <b><span style='color: #FFD700'>Hierarchical</span></b> attention
>- <b><span style='color: #FFD700'>Flash</span></b> attention (*Avoid redundant computations*)
>- <b><span style='color: #FFD700'>Selective routing</span></b> (*only compute over the most relevant tokens*)
## Core Concepts Of Transformers
### Positional Embeddings

Because in **transformers we process all words at once**, we now <b><span style='color: var(--mk-color-red)'>lose the word ordering</span></b> (*because we process all words at once*) and we want to preserve word order in the sequence.

So when we talk about adding word order for transformers we will <b><span style='color: #FFD700'>take the word embedding and just add some position embedding</span></b> ($p$).

This positional embedding:
- It must be <b><span style='color: #FFD700'>continuous</span></b>
- It must be <b><span style='color: #FFD700'>unique regardless of the sentence length</span></b>

So lets take the **naive approach** by just <b><span style='color: #FFD700'>using the index of the word in the sentence</span></b> (*so the nth word's positional embedding is just a matrix of the value n*).

>[!fail] This is bad because our positional encodings of later words can dominate word embeddings because it depends on the length of the sequence

Ok then lets **normalise it against the number of words** so, $\text{pos} / N$. The <b><span style='color: #FFD700'>values now will be between 0 & 1</span></b>.

>[!fail] The positional encoding still depends on the sequence length
>Between sentences of different lengths, the <b><span style='color: var(--mk-color-red)'>encoding for the same position will be different</span></b>.

The <b><span style='color: #FFD700'>proposed solution is to use our trigonometry functions</span></b>, given a size of the positional embedding to be $I$:
- For all **even** index cells in the embedding
$$
PE_{(pos, 2i)} = \sin(\frac{pos}{10000^{2i / d_{model}}})
$$
- For all **odd** index cells in the embedding
$$
PE_{(pos, 2i + 1)} = \cos(\frac{pos}{10000^{2i / d_{model}}})
$$
Where:
- $d_{model}$ is the word embedding size which is the same as our positional embedding size
- $i$ is some value which we need to find so for even index solve $2i = x$ for odd indexes solve $2i + 1 = x$.
- $pos$ is the position of the word in the sequence starting from 0

>[!important] This type of positional encodings are absolute
>Meaning it <b><span style='color: #FFD700'>encodes the position of the word</span></b> & that <b><span style='color: #FFD700'>distances between words are implicit</span></b> (*not stated but can be derived*).

>[!note] Using sin and cos ensures that all the values are between -1 and 1

>[!success] Unique encoding for each position & is independent from the length of the sequence
>This also means we can compute all of this once at the start & it will not change.

We can **visualise this**:
![[Visualising Positional Embedding Results.png|center|500]]

The the rows denote the positional embedding, and the columns are the embedding values.
### Multiple Head Attention

![[Attention Head Example.png|center|200]]

So the whole process of [[Year 3/Sem 2/CS4248 - Natural Language Processing/Transformers.md#Computing Attention|computing attention]] is all wrapped in something called a <b><span style='color: #87CEEB'>attention head</span></b>. But there is a problem with this, <b><span style='color: var(--mk-color-red)'>not only is it slow</span></b>, it also <b><span style='color: var(--mk-color-red)'>considers only 1 instance of a relationship between pairs of words</span></b>.

So this is where the <b><span style='color: #87CEEB'>multi-attention head</span></b> comes in. **Each attention head** will have its <b><span style='color: #FFD700'>own KQV weight metrices</span></b> & will convert the input word embedding into the corresponding (*typically of size* $d_{model} / h$ *but it does not have to be*) 

You <b><span style='color: #FFD700'>can also stack multiple MHAs</span></b>, so the output from the MHA will be passed into the next layer and so on (*for this we use the parameter $n_{layers}$*).

>[!success] So this makes computation faster as we are doing smaller computation it in parallel

>[!success] Each attention head can then pay attention to a small aspect of word relationship

>[!example] If after transforming we have a embedding size of 512 and we have 8 attention heads we just convert the matrix into blocks of 64 elements

Then the output of each head will be <b><span style='color: #FFD700'>concatenated back together</span></b> to form the original "update embedding" then we use a **linear layer** to ensure that the <b><span style='color: #FFD700'>final embedding is of the original word embedding size</span></b> so that we can update the original word embedding.

>[!tldr] Feed forward layer
> In papers it **did not explain what this layer does**, but essentially when we <b><span style='color: #98FB98'>stack neural networks we get more capability or expressiveness</span></b> which is what is happening here in general.
### Masking

When we do masking we are address the issue that <b><span style='color: #FFD700'>not all alignments matters</span></b> (*not all word pairs matter*) so this can be:
- <b><span style='color: #FFD700'>Padding sequences</span></b> of different lengths to ensure the same context window
- <b><span style='color: #FFD700'>Hide words</span></b> in models for language modeling (*mask then ask them to predict*)
- <b><span style='color: #FFD700'>Hide future words</span></b> to ignore for text generation (*it would be cheating if it can see future words*)

So typically **masked words** will be represented as a matrix called the <b><span style='color: #87CEEB'>masking matrix</span></b>, where the <b><span style='color: #FFD700'>values is negative infinity if the word is mask else its 0</span></b>. 

So before taking the SoftMax we will <b><span style='color: #FFD700'>add this matrix</span></b> to it. Then after the SoftMax, they will become 0, meaning the <b><span style='color: var(--mk-color-red)'>alignment between that word and the masked word can't be used</span></b>.

>[!tldr] Masking for language modeling
>Like what BERT does, so everything is the same actually, when we <b><span style='color: #FFD700'>compute the alignment for all pairs, the pairs containing the mask words will be negative infinity</span></b> due to the masking matrix. 

>[!tldr] Masking for text generation
>The problem with he transformer is that it look at all words (*past & future*). So when training text generation the **input is the sentence** the **output is the same sentence just shifted left by 1**.
>
>Now the **problem** is when predicting the next word the transformer can <b><span style='color: var(--mk-color-red)'>"cheat" by looking into the future</span></b>. So this is where <b><span style='color: #87CEEB'>causal masking</span></b> comes in. In causal masking we <b><span style='color: #FFD700'>just mask the top triangular half of the alignment table</span></b>.
>
>This is <b><span style='color: #FFD700'>mainly used in a decoder-only LLM</span></b> (*cause the decoder you get to see the output as well*).
## Transformer Architecture

It is still an [[Year 3/Sem 2/CS4248 - Natural Language Processing/Encoder & Decoder.md#Encoder & Decoder|encoder & decoder]] but it <b><span style='color: #FFD700'>does not have recurrences</span></b>, meaning it does not depend on the previous states & does all its computation in a few steps.

![[Transformer Architecture .png|center|300]]

Here the **input & output** <b><span style='color: #FFD700'>is the entire sentence</span></b> and not just 1 word.

>[!success] No long-range dependencies then no bottleneck
>Which prevents vanishing & exploding gradients.

>[!success] Learns better representation of the words

>[!success] No sequential processing thus we can parallelize it
>But this does not mean it is easier or faster to train

>[!fail] The number of operations can be a lot if we want to operate attention
>It is around $N^{2}$ number of operations where $N$ is the sequence length.

>[!important] The core concept of transformers is still attention
>And they compute attention <b><span style='color: #FFD700'>calculating the alignment scores between all word pairs all at once</span></b>.
### Encoder Layer For The Transformer

So what we have seen is so far is the **encoder of the transformer**:
- Take a input at some time stamp $t$
- Add the [[Year 3/Sem 2/CS4248 - Natural Language Processing/Transformers.md#Positional Embeddings|positional embedding]]
- Then pass it through the [[Year 3/Sem 2/CS4248 - Natural Language Processing/Transformers.md#Multiple Head Attention|multi-head attention]] to compute the [[Year 3/Sem 2/CS4248 - Natural Language Processing/Transformers.md#Attention For Transformers|attention]]
- Then we pass it through the feed forward layer

There are also **3 additional concepts** deployed as well:
1) <b><span style='color: #87CEEB'>Residual connections</span></b>, there the <b><span style='color: #FFD700'>input skips the multi-head attention layer</span></b> and the <b><span style='color: #FFD700'>multi-head input skips the feed forward layer</span></b>. All this is to <b><span style='color: #98FB98'>mitigate the vanishing gradient</span></b> problem
2) <b><span style='color: #87CEEB'>Dropout</span></b>, which is done after MHA and FF block which is just setting some weights to be 0. A <b><span style='color: #98FB98'>regularisation technique to prevent overfitting</span></b>
3) <b><span style='color: #87CEEB'>Layer normalisation</span></b>, which is done after the MHA and FF. This <b><span style='color: #FFD700'>normalise the input across features</span></b>, which <b><span style='color: #98FB98'>improves the  training stability & convergence</span></b>

>[!note] Typically we will have multiple encoder blocks
>This forms a <b><span style='color: #FFD700'>layered architecture</span></b>, So the output of 1 encoder block will be passed into the next encoder block and the cycle repeats.
### Decoder Layer For The Transformer

Here everything is the <b><span style='color: #FFD700'>same as the encoder</span></b> but we <b><span style='color: #FFD700'>use 1 more MHA block</span></b>:
1) 1 for the output being passed into the decoder
2) 1 is to <b><span style='color: #FFD700'>compute the cross attention from the output to the encoder's output</span></b>

For the 2nd MHA block, now our **query** is from the <b><span style='color: #FFD700'>output</span></b>, while the **key & value** are from the <b><span style='color: #FFD700'>encoder's output</span></b>.

>[!note] And same as the encoder we can have multiple decoder blocks
# Core Tasks For Transformers
---
## Classification

![[Classification Using Transformers.png|center|400]]

## Sequence Labeling

![[Sequence Labeling Using Transformers.png|center|250]]

## Text Generation

![[Text Generation Using Transformers.png|center|500]]