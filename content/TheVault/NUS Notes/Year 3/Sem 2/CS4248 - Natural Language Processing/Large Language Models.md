---
Title: Large Language Models
Date Created: 09-April-2026
Last Updated: 17-April-2026
Tags:
  - CS4248
  - AI/ML/NN/LLM
---
# Transformer based LLMs
---
## Encoder-Only

### BERT

Also known as <b><span style='color: #87CEEB'>bidirectional encoder representation from transformers</span></b>. And is self-supervised trained.

It is trained on **2 learning objectives**:
- **Masked language model** (*MLM*), where we <b><span style='color: #FFD700'>mask some words in the input</span></b> (*around 50%*), then train itself by predicting the masked words
- **Next sentence prediction** (*NSP*), here we are <b><span style='color: #FFD700'>predicting if sentence 2 follows sentence 1</span></b>

>[!info] In future works, they learnt that next sentence prediction is not that helpful so future models only use MLM

**How BERT was trained**:
![[BERT Training Overview.png|center|500]]

Essentially we will first pass in:
- Some <b><span style='color: #FFD700'>classifier token</span></b> (*CLS*), this is to tell BERT to output a classification label
- Followed by <b><span style='color: #FFD700'>sentence 1, a separator token then sentence 2</span></b>
- We will also <b><span style='color: #FFD700'>mask</span></b> some tokens (*during preprocessing*)

Then the model will predict the NSP classification and the masked words.

>[!note] The first token is typically a CLS token but we can use other tokens as well to do other tasks
>So after training BERT when it sees this token will know what task it needs to do.

For **supervised fine-tuning** it is the <b><span style='color: #FFD700'>same thing but we augment the input</span></b>. For example SQuAD we pass in a question & a paragraph which BERT will find where in this paragraph is the answer to the question.
### RoBERTa

It is just a <b><span style='color: #FFD700'>scaled up version</span></b> of [[Year 3/Sem 2/CS4248 - Natural Language Processing/Large Language Models.md#BERT|BERT]]. Trained on more data and longer & it uses <b><span style='color: #FFD700'>MLM only</span></b>.

The **"Ro"** means **robustly optimised** and it <b><span style='color: #98FB98'>outperforms BERT</span></b>.

It also does **dynamic masking** where the <b><span style='color: #FFD700'>masking is done during training time & the words to mask changes</span></b>.

There are also **other BERT variants**:
- DistilBERT (*smaller than BERT so it runs faster*)
- ALBERT
## Encoder-Decoder

### T5

![[T5 Highlevel Overview.png|center|400]]

Also known as <b><span style='color: #87CEEB'>text-to-text transformer</span></b>. It is you standard [[Year 3/Sem 2/CS4248 - Natural Language Processing/Transformers.md#Transformers|encoder decoder transformer]]. But T5 is known for its <b><span style='color: #FFD700'>multi-task learning</span></b>, where the model is <b><span style='color: #FFD700'>trained on multiple tasked simultaneously</span></b>.

We can just give it plenty of <b><span style='color: #FFD700'>input prompt and a sample output during training</span></b> (*all text*). And because of this it can learn a lot of natural language task.

>[!abstract] Scaling law
>This law states that as a <b><span style='color: #FFD700'>model sees more input the better its performance</span></b> will be.
>
>So this is where T5 capitalises on this where if a model is only shown data for one task its performance will be at a certain level. But if we <b><span style='color: #FFD700'>give it data from multiple tasks it gets to see more data</span></b> and the <b><span style='color: #98FB98'>competency for all these tasks will increase</span></b>.
### BART

BART improves the concept of masking by <b><span style='color: #FFD700'>corrupting documents</span></b>:
- Token masking
- Sentence permutation
- Document rotation
- Token deletion
- Text infilling

Then all it does is to <b><span style='color: #FFD700'>optimise the reconstruction loss</span></b> and this is called <b><span style='color: #87CEEB'>denoising</span></b> (*cross-entropy between decoder output & original document*).

>[!info] BART is essentially BERT + [[Year 3/Sem 2/CS4248 - Natural Language Processing/Large Language Models.md#GPT|GPT]]
>So BERT doss the masking, then <b><span style='color: #FFD700'>GPT is to auto-regressively do word prediction</span></b>

## Decoder-Only

These types of LLMs <b><span style='color: #FFD700'>largely dominates</span></b> in the type of LLMs that are currently created.

>[!question] Why do they dominate?
>It is because there are a lot of advantages to this:
>- <b><span style='color: #98FB98'>Simple architecture & setup</span></b>
>- More <b><span style='color: #98FB98'>cheap to train</span></b> (*relatively*)
>- More <b><span style='color: #98FB98'>suitable for text generation</span></b>
>- <b><span style='color: #98FB98'>Good zero-shot generalization</span></b>
### GPT

Also known as <b><span style='color: #87CEEB'>generative pretrained transformer</span></b>. And is self-supervised trained.

Recall that in our decoder we have a <b><span style='color: #FFD700'>multi-head attention layer for the encoder output, which now we do not have</span></b> (*so it goes directly to the feed forward layer after the masked multi-head attention*).

And **during training** we need to do [[Year 3/Sem 2/CS4248 - Natural Language Processing/Transformers.md#Masking|causal masking]]. Because during <b><span style='color: var(--mk-color-red)'>training when computing attention we can see all the future words</span></b> which we do not want.

>[!important] We also need to do causal masking during inference (*during testing or during actual predictions*)
>Because when we <b><span style='color: #FFD700'>give a prompt it processes all the words at once & it can still cheat</span></b> by taking word 1 and computing the alignment for all the future words in the input. So we still need to mask.
>
>Unless we didn't give anything then no need for masking!!

As GPT models improve, so does the number of parameters which leads to more layers, number of heads, dimension of the word embeddings and attention head dimension.
#### Reinforcement Learning From Human Feedback (RLHF)

A **very important step** is to do <b><span style='color: #87CEEB'>alignment with human feedback</span></b>.

So in RLHF there are **2 common setups**:
1) Take our trained model and for the **same query** (*or similar queries*) <b><span style='color: #FFD700'>generate multiple responses & ask a human to rank</span></b> them which will then be used for fine-tuning
2) We can also just <b><span style='color: #FFD700'>use human-generated responses</span></b> & do fine-tuning

Like in GPT they will ask you which response is better A or B. This is what RLHF is doing it asks a bunch of people which reference its preferred (*this generates* $2^{n}$ *training samples due to this transitivity property* ). Then <b><span style='color: #FFD700'>all this will be used with a reinforcement learning algorithm</span></b>.

>[!tldr] Reinforcement learning from AI feedback (RLAIF)
>Is the exact same thing, but now we <b><span style='color: #FFD700'>use an highly capable AI</span></b> with a strict set of evaluation criteria and automatically scores responses which will then be used to fine-tune a model.
### LLaMA

Very similar to [[Year 3/Sem 2/CS4248 - Natural Language Processing/Large Language Models.md#GPT|GPT]] but with some **slight tweaks**.

>[!success] LLaMA models are trained on publicly available data
>Meaning that LLaMA models are open LLM and anyone can re-create it.
#### Pre-Normalisation

This is one of the tweaks that LLaMA models does. Recall that in our [[Year 3/Sem 2/CS4248 - Natural Language Processing/Transformers.md#Transformer Architecture|transformer architecture]] **after each block we will do an addition and then a normalisation**. But now the <b><span style='color: #FFD700'>normalisation layer is done before the block or inside the block</span></b>.

>[!note] Normalisation is to convert a set of numbers to be within a particular range

>[!success] More well-behaved gradients at initialisation
>And during training as well.

>[!success] Helps with vanishing & exploding gradients

>[!success] Significantly faster training
#### SwiGLU

It is **similar to ReLU** (`max(0, x)`), but the issue with ReLU is that <b><span style='color: var(--mk-color-red)'>at 0 there is a discontinuity, thus we cannot really continuously differentiable</span></b>.

>[!info] Dead neuron / unit
>If your neurons uses the ReLU activation & they all **zero out**, meaning that <b><span style='color: #FFD700'>no information is being passed through</span></b>, effectively making the neuron dead.

In additional <b><span style='color: #98FB98'>sometimes negatives are useful</span></b>.

<b><span style='color: #87CEEB'>SwiGLU</span></b> is made up of 2 parts:
1) <b><span style='color: #FFD700'>Gated linear unit</span></b>

$$
GLU(x) = (xW + b) \otimes \sigma(xV + x)
$$
Where:
- $\otimes$ means element wise multiplication
- $V$ & $W$ are trainable weights (*this V is not the value matrix*)
- $b$ is a bias vector
- $x$ is one row after computing the attention matrix QKV

2) <b><span style='color: #FFD700'>Swish</span></b>

$$
Swish(x) = x \otimes \sigma(\beta x)
$$
- $\beta$ is just some parameter to control the steepness or shape of the activation curve

So with this SwiGLU is just:
$$
SwiGLU(x) = (xW + b) \otimes Swish_{\beta}(xV + c) 
$$

So this **block is typically placed after the MHA**.
#### Rotary Positional Embeddings

Also known as <b><span style='color: #87CEEB'>RoPE</span></b>. It is the same idea as our [[Year 3/Sem 2/CS4248 - Natural Language Processing/Transformers.md#Positional Embeddings|positional encodings]] but here we are <b><span style='color: #FFD700'>also computing the relative positions</span></b>.

So here we **either** do RoPE or the **[[Year 3/Sem 2/CS4248 - Natural Language Processing/Transformers.md#Positional Embeddings|positional encodings]]**.

>[!tldr] Relative positions
>They are essentially the <b><span style='color: #FFD700'>distances between one word & another</span></b>.
>
>So if it is a negative value then its some word in the past and if its positive it is some word in the future.

We **still want to use our sinusoidal functions** but <b><span style='color: #FFD700'>words that are far apart can be differentiated</span></b> & how can we do this, is through the <b><span style='color: #FFD700'>angle between the 2 vectors</span></b>.

The idea is to rotate the vector using a <b><span style='color: #87CEEB'>rotation matrix</span></b> ($R^{d}_{\Theta, m}$):
![[Rotation Matrix for Any Dimension Size.png|center|450]]

For a **2D matrix** it the rotation matrix will be:
$$
R_{\theta, m} = 
\begin{bmatrix}
\cos(m\theta) & -\sin(m\theta) \\
\sin(m\theta) & \cos(m\theta)
\end{bmatrix}
$$
And you can see we repeat this as we go down the diagonal where:
- $m$ is the actual index position of the word in the sentence
- Each $\theta$ which is **in radian** are individual coefficients to rotate the vector

So typically to **select theta**, we will follow this formula:
$$
\Theta = \{ \theta_{i} = B^{-2(i - 1)/d}, i \in [1, 2, \dots, d/2] \}
$$
Where:
- $B$ is some base frequency where we can set it to any value

>[!note] This will cause lower dimensions to correspond to higher frequencies and vice versa

But this is more of a **guide**, we can actually <b><span style='color: #FFD700'>choose whatever values we want</span></b>.

>[!warning] When selecting theta, try and not use values that are the same or are multiples of some number
>This will <b><span style='color: #FFD700'>ensures the vector does not rotate more than 360 degrees</span></b> (*thus no 2 different positions will be rotated to the same angle*).

With this a <b><span style='color: #98FB98'>dot product will be the same regardless of the absolute position as long as the relative position stays the same</span></b>.

>[!important] This only works if our dimensions are even

Here is the how RoPE **computes the positionings**:
![[The Full Rotation Formula.png|center|450]]

Here, $x$ is the **embedding of 1 word**. So we only <b><span style='color: #FFD700'>do this rotation for the query & key vectors</span></b> (*because it affects the computation of weights*) but <b><span style='color: var(--mk-color-red)'>not the value vectors</span></b> as we do not want to interfere with the computation of the weighted sum.

>[!success] Encodes relative positions which are often more useful than absolute positions
>But we are not removing absolute positions.

>[!success] Fixed computation that can extrapolate the positions not seen during training

>[!failure] Fixed computation meaning less flexible than learnable encoding strategies

>[!failure] Generally harder to interpret than absolute positional encodings

>[!failure] Not (directly) compatible with all attention variants
>For example: Multi-head Latent Attention in DeepSeek.

>[!failure] Assumes vectors to be of even sizes
>Will not work with odd vector size.
# Training & Working With LLMs
---
## Data Collection & Preprocessing

We have **a lot of training data**, anything with text can be our training data and <b><span style='color: #FFD700'>most of it is on the web</span></b>.

Typically we can <b><span style='color: #FFD700'>crawl</span></b> the website which is just to <b><span style='color: #FFD700'>extract out the text</span></b> from the website (*and typically we need to adhere to the `robots.txt`*).

>[!warning] But not all of the data on the web is useful
>It contains a <b><span style='color: var(--mk-color-red)'>mixture of useful and irrelevant data</span></b> (*headers, footers, navigation, HTML markup*), so its of low quality (*we want high quality data*). This is called <b><span style='color: #87CEEB'>noisy data</span></b>.

And if our task is **something domain specific** we <b><span style='color: var(--mk-color-red)'>cannot crawl everything</span></b> we need to <b><span style='color: #FFD700'>curate a special dataset</span></b>.

>[!info] Instead of crawling we can also train on the output of other LLMs or use syntactic data
>Which we still need to clean & ensure it is of quality.
### Data Deduplication

A common occurrence when crawling is the <b><span style='color: var(--mk-color-red)'>retrieval of duplicate data</span></b>. Lets take news outlets, many of them will be **posting the same news articles**, this <b><span style='color: #FFD700'>does not mean that the article is important than others</span></b>, it just appears more frequently.

>[!fail] Typically it slows down training

>[!fail] Higher risk of memorization

And <b><span style='color: var(--mk-color-red)'>deduplication is not an easy problem to solve</span></b>:
- Sometimes it is <b><span style='color: #FFD700'>not obvious</span></b> what a duplicate is
- It is a <b><span style='color: var(--mk-color-red)'>very resource-intensive task</span></b>
### Data Decontamination

This is a **typical setup for training or fine-training a model**:
- <b><span style='color: #FFD700'>Hyperparameter tuning</span></b> with training & validation set
- <b><span style='color: #FFD700'>Evaluation</span></b> with a separate test data

<b><span style='color: #87CEEB'>Data decontamination</span></b> is mainly when evaluating a model, but it is <b><span style='color: #FFD700'>not clear which data non-public LLM's are trained on</span></b>. So there is <b><span style='color: var(--mk-color-red)'>no guarantee that test dataset was not part of the initial training data</span></b>.
### Toxicity & Biases

The model is not toxic or bias since it follows the math we set. This <b><span style='color: #FFD700'>comes from the data that we supply</span></b>.

This can be in the form of, racism, sexism, misinformation, biased reporting, hate speech, propaganda, etc.

>[!success] One way to mitigate this is to rely on content from trusted sources

>[!warning] Debiasing is actually quite complex because some biases can help with the semantic context of the word
>This will <b><span style='color: var(--mk-color-red)'>remove some semantic meaning</span></b> from words but it can also <b><span style='color: var(--mk-color-red)'>remove useful relationships</span></b> as well.

### PII Control

PII means <b><span style='color: #87CEEB'>personally identifiable information</span></b>. So the problem here is that our <b><span style='color: #FFD700'>training data might contain privacy-sensitive information</span></b>.

We need to exclude these information from the LLM so that it does not generate these PII's in their responses.
## Training An LLM

So <b><span style='color: #FFD700'>typically large numbers of data is required for a very good LLM</span></b> but a normal LLM can be generated using a few 100k data samples.

>[!success] Small datasets are easy to run even on a CPU
>But **consider using a GPU** is available as it <b><span style='color: #98FB98'>makes linear algebra faster</span></b>.

>[!success] Whole dataset fits into memory

>[!failure] Downside to using small amounts of data is that it is no rival to the bigger popular LLMs

When <b><span style='color: #FFD700'>training we need a stream of documents</span></b>, so with our training data we will just make a very long sentence, <b><span style='color: #FFD700'>concatenating each datapoint with a end of sentence token</span></b>.

So essentially we are:
- Looping over each datapoint (*sentence*)
- Tokenize our sentence
- Append the special separator
- Concatenate all our datapoints into a document stream

Recall that all we are **training is a next word prediction task**, so from our dataset we can do a <b><span style='color: #FFD700'>sliding window approach with overlap</span></b>.

So what happens here is that we <b><span style='color: #FFD700'>take some context window & ask it to predict the next word</span></b>. Now we **specify an overlap** which is to say we <b><span style='color: #FFD700'>take how many percent of the last few words of the current context in the next iteration</span></b>.

>[!example] Example of a sliding window of 4 & a overlap of 50%
>So given this sentence "Hello I am very interested in NLP"
>Epoch:
>1) "Hello I am very"
>2) "am very interested in"
>3) And so on...

>[!note] For larger datasets people do not use overlaps but for smaller datasets we should use a larger overlap for more training samples

So typically <b><span style='color: #DDA0DD'>PyTorch</span></b> is used & then we can use this to train our decoder:
- So we need the [[Year 3/Sem 2/CS4248 - Natural Language Processing/Transformers.md#Positional Embeddings|positional encoding]]
- An [[Year 3/Sem 2/CS4248 - Natural Language Processing/Transformers.md#Encoder Layer For The Transformer|encoder]] (*if we are doing a encoder-decoder*)
- [[Year 3/Sem 2/CS4248 - Natural Language Processing/Transformers.md#Masking|Causal masking]]
## Using Pretrained LLMs
### Cloud-Based APIs
Many of the pretrained LLMs are on the cloud (*cloud based APIs*) are <b><span style='color: #FFD700'>accessible through API</span></b> (*application programing interface*).

All we need is an <b><span style='color: #FFD700'>API key and a wrapper</span></b> (*sometimes*) to invoke the LLM.

>[!success] These LLMs are a [[Year 3/Sem 2/CS5224 - Cloud Computing/Cloud Concepts & Models.md#Software As a Service|software as a service]] and the LLM's are personalised for the user

>[!warning] However do keep in mind about billing, rate limitation

>[!success] Advantages of using cloud-based APIs
>- Immediate access to state-of-the-art models
>- Ease of use and integration
>- High performance and optimization (*no need for own high-end hardware, e.g., GPU clusters*)
>- Security, compliance, and reliability
>- Extensive ecosystem and tooling
>- Ethical and Policy Constraints
>- Lower barrier to entry

>[!failure] Challenges & limitations of using cloud-based APIs
>- Limited customization and control
>- Data privacy and security
>- Cost and Scalability
>- Network latency and rate limits
>- Dependence on service provider
>- Ethical and Policy Constraints
### Running LLMs Locally

To run a model locally you will need to <b><span style='color: #FFD700'>install their neural network and the weights</span></b> (*no need for an API key*).

These models can be found on LLaMA and hugging face with different sizes and capabilities. Then all you need to do now is implement it in your code.

>[!success] Advantages of running LLMs locally
>- Data privacy and security
>- Full control and customization
>- Predictable costs (*potentially lower in the long term*)
>- Low latency and offline capability
>- Integration and infrastructure flexibility

>[!failure] Challenges & limitations of running LLMs locally
>- High hardware and setup costs
>- Limited access to frontier models
>- Complex setup and maintenance
>- Performance and memory constraints
## Prompt Engineering

It is the practice of <b><span style='color: #FFD700'>designing / refining / structuring prompts</span></b> to <b><span style='color: #FFD700'>elicit specific responses</span></b> from an LLM (*garbage in, garbage out*).

>[!tldr] Prompt
> Natural language text <b><span style='color: #FFD700'>describing the task</span></b> that an AI (*model*) should perform.

>[!goal] Systematically design prompts to ensure or avoid certain behavior of LLM
>But typically we are trying to:
>- Enforce reasoning
>- Reduce hallucinations
>- Improve consistency & coherence
>- Self-reflection / self-monitoring

And a good thing is that it <b><span style='color: #98FB98'>does not affect the LLMs pre-trained weights</span></b>.

Here are some **best practices**:
- Use the latest model
- Put <b><span style='color: #FFD700'>instructions at the beginning</span></b> of the prompt and clearly separate instructions and prompt (*and at the end to remind the LLM*)
- Be specific, descriptive and as detailed as possible (*about the desired context, outcome, length, format, style, etc.*)
- Articulate the desired output format through examples
- Start with <b><span style='color: #FFD700'>zero-shot, then few-shot</span></b> (*if all fails: fine-tune*)
- Reduce “fluffy” and imprecise descriptions
- Instead of saying what "not" to do, <b><span style='color: #FFD700'>say what to do instead</span></b>
- Code Generation Specific – <b><span style='color: #FFD700'>use “leading words”</span></b> to nudge the model toward a particular pattern (*like in [[Year 3/Sem 2/CS4248 - Natural Language Processing/Large Language Models.md#BERT|BERT]] we add like a task token*)
### In-Context Learning

Typically when we <b><span style='color: #FFD700'>just ask a question</span></b> to an LLM, we are doing <b><span style='color: #87CEEB'>zero-shot prompting</span></b>. In x-shot prompting or <b><span style='color: #87CEEB'>in-context learning</span></b> (*ICL*) our <b><span style='color: #FFD700'>prompt will contains some number of task-specific examples and their answers</span></b>.

>[!note] For self-explanatory tasks 0 prompting is suffice but for more complex tasks giving more shots helps provides context & guide the LLM

>[!important] In in context learning we are not modifying any of the model's weights
>We are <b><span style='color: #FFD700'>just augmenting the hidden states in the transformers</span></b>.

>[!success] The LLM can do a task that it is not trained on

>[!success] It is inexpensive / cost effective

>[!question] Why does ICL this work?
>The intuition is that it <b><span style='color: #FFD700'>helps "locate" latent concepts acquired during pre-training</span></b> (*the weighs needed to do this task*).

Here are some **interesting observations** from a study on ICL:
1)  <b><span style='color: #FFD700'>Correctness</span></b> of the demonstration labels <b><span style='color: #FFD700'>does not really matter</span></b>

Demonstrations with incorrectness <b><span style='color: #98FB98'>perform just as well with actual ground-truth labels</span></b> & outperforms with no demonstrations.

2) More demonstrations help <b><span style='color: #FFD700'>except beyond some threshold</span></b>

More demonstrations help but <b><span style='color: var(--mk-color-red)'>after a certain threshold it gives diminishing returns</span></b>.

3) <b><span style='color: #FFD700'>Relevance</span></b> of the demonstration matters

By **giving random tasks** instead of the actual tasks <b><span style='color: var(--mk-color-red)'>decreases the models performance for the task</span></b> (*even with the correct outputs*).

4) The <b><span style='color: #FFD700'>label space</span></b> of the demonstration matters

Same thing by **giving random labels** instead of the actual ones <b><span style='color: var(--mk-color-red)'>decreases the models performance for the task</span></b> (*labels carry semantic information*).

5) <b><span style='color: #FFD700'>Order & distribution</span></b> of demonstration & labels matters

![[Example of how Distribution & Order Affects LLMs.png|center|500]]

From the image you can observer that there is some <b><span style='color: var(--mk-color-red)'>recency bias & majority label bias as well</span></b>, because there are a majority of the same label or the order of the labels.
# LLMs The Good The Bad The Ugly
---
Now language models are **very powerful**, this is due to:
- New architectures (*transformers*)
- More computing power
- More diverse data
- More resources (*millions spent and a lot of manpower*)

This <b><span style='color: #FFD700'>caused an explosion in the size & scale of the model</span></b>. So these models have crossed some tipping point which shows <b><span style='color: #FFD700'>emergent abilities</span></b>.

>[!tldr] Emergent abilities
><b><span style='color: #FFD700'>Abilities that were not explicitly programmed into the model</span></b> but emerge from the training process (*summarisation, translation, question answering, code generation*).
>
>And remember an LLM in the end is still just a next word prediction task.

>[!fail] And since the model is so large we do not really know why and how it works
>Some argues that there are reasoning capabilities but it is still a <b><span style='color: #FFD700'>black box model</span></b>.

>[!fail] It also causes a lot of disruptions
>In areas like, workplace or education
## Cost Of LLMs

We know that **training** an LLM we need:
- <b><span style='color: #FFD700'>Huge amounts of clean / good data</span></b>
- <b><span style='color: #FFD700'>Huge amounts of computing resources</span></b> (*infrastructure & energy consumption*)

>[!fail] This makes training LLMs from scratch accessable to large companies
>Might be too expensive for individuals or small teams.

And it is not just training it is also during **inference** (*test time/deployment*) as typically the full model is used.

So for each query it <b><span style='color: var(--mk-color-red)'>consumes a lot of power</span></b> (*150x more than google search*) which is mainly due to:
- Number of <b><span style='color: #FFD700'>tokens generated</span></b>
- <b><span style='color: #FFD700'>Model size & type</span></b>
## Model Alignment

So LLMs typically give responses that are correct, but the <b><span style='color: #FFD700'>style, form or tone of the response also matters</span></b>.

Typically **we want responses** to be:
- Aligned with <b><span style='color: #FFD700'>user preference</span></b> (*Accurate & coherent*)
- Aligned with <b><span style='color: #FFD700'>user's moral compass</span></b> (*Safe & ethical*)

So typically there are a lot of advancement to **improve LLMs in terms** of:
- <b><span style='color: #FFD700'>Accuracy &  hallucinations</span></b> (*prevent it from giving wrong or garbage outputs*)
- <b><span style='color: #FFD700'>Misinformation, disinformation & fake news</span></b> (*people can spread this freely*)
- <b><span style='color: #FFD700'>Jailbreaking</span></b> (*Bypass LLMs guardrails using prompts or by pretending*)

>[!tldr] Guardrails
>They are some sort of <b><span style='color: #FFD700'>rules that are imposed on the LLM</span></b> to ensure that the <b><span style='color: #98FB98'>content generated is moderated & will not provide harmful information</span></b>.