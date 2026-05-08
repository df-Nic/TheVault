---
Title: Improving LLMs Efficiency
Date Created: 22-April-2026
Last Updated: 01-May-2026
Tags:
  - CS4248
  - AI/ML/NN/LLM/Efficiency
---
# Why Improve An LLMs Efficiency
---
LLMs are great and all but they have some major **issues** & that is <b><span style='color: var(--mk-color-red)'>power consumption & speed</span></b>.

During inference (*generating responses*), the <b><span style='color: #FFD700'>full model will be used</span></b> (*slow generation*). But the <b><span style='color: #FFD700'>main issue is the number of tokens generated</span></b>.

>[!warning] The more tokens it generates the more power it consumes
>In comparison google search is 150x cheaper than text generation using LLM.

And not only that but the <b><span style='color: #FFD700'>model's architecture</span></b> does play a part in this as well.

>[!goal] Increase efficiency of the LLM to decrease electricity cost

There are many ways to improve efficiency:
- Data efficiency
- Budget efficiency
- Inference efficiency (*focus is on this*)
- Architecture efficiency
- Training & tuning efficiency
## Model Complexity & Data Size

So far from many LLMs <b><span style='color: #FFD700'>more parameters, data, compute results in better models</span></b> this is known as the <b><span style='color: #87CEEB'>scaling law</span></b>. But this has its own **issues**:
- Increasing <b><span style='color: var(--mk-color-red)'>memory requirements</span></b>
- Increasing <b><span style='color: var(--mk-color-red)'>training & inference time</span></b>
- Increasing <b><span style='color: var(--mk-color-red)'>energy consumption</span></b>
- Increasing need for more <b><span style='color: var(--mk-color-red)'>training data</span></b>
- <b><span style='color: var(--mk-color-red)'>More compute</span></b> (*performance has a hardware or data limit*)

>[!important] Is not just parameters only, there is also the amount of data to consider as well
>We will get <b><span style='color: var(--mk-color-red)'>diminishing returns</span></b> if we have **insufficient data & a large model**.
# Quantization
---
Our **weights** typically <b><span style='color: #FFD700'>tuned to some levels of prevision</span></b> (*over-parameterized*) & typically for **normal use cases** we do not need 100% accuracy we just <b><span style='color: #FFD700'>need something that is close to the actual answer & still acceptable</span></b>.

>[!idea] We just reduce the numerical precision of weights and or activations
> Activations are the outputs from the neuron, and we also need to <b><span style='color: #FFD700'>preserve distribution during this mapping</span></b>.
>>[!example] Instead of using a 32 bit floating point integer we can use just a 8 bit integer, saving 24 bits

>[!success] Reduce memory requirement
>Sometimes we can fit large LLM's into a single GPU.

>[!success] Faster calculations
>As hardware is often optimised for lower prevision values.

>[!success] Works best for very large models
>Especially when they are over parameterized.

>[!fail] Risk of accuracy degradation
>The penalty for quantization is the loss of some information or the models expressiveness.

>[!fail] More tricky to implement & train
>And it is sometimes <b><span style='color: var(--mk-color-red)'>not suitable for all layers networks & hardware</span></b>.
>
>For instance, in backward propagation if we have values like 0.99 it will be reduced to just 0 leading to a <b><span style='color: var(--mk-color-red)'>0 gradient backward propagation</span></b>.
>
>Also some <b><span style='color: var(--mk-color-red)'>hardware may not support lower precision</span></b> which leads to them bring the same precision.

There are a few quantization **strategies**:
- Post training quantization (*PTQ*), like [[Year 3/Sem 2/CS4248 - Natural Language Processing/Improving LLMs Efficiency.md#Asymmetric Quantization|asymmetric quantization]]
- [[Year 3/Sem 2/CS4248 - Natural Language Processing/Improving LLMs Efficiency.md#Quantization Aware Training (QAT)|Quantization-aware training]] (*QAT*)
- Quantize training (*QT*)

>[!tldr] Quantize training
> Though not the focus here but in summary, we <b><span style='color: #FFD700'>look at the distribution</span></b> of the weights then we <b><span style='color: #FFD700'>use more integers to express denser or more common weight values</span></b>.
## Asymmetric Quantization

So this approach is very simple we just <b><span style='color: #FFD700'>compress the weights from some high prevision to something lower</span></b>.

So now its the **asymmetric part**, it means that we should <b><span style='color: #FFD700'>preserve the meaning of the weights</span></b>, so:
- The **largest** weight value will be <b><span style='color: #FFD700'>mapped to the maximum value</span></b> we are compressing into
- The **smallest** weight value will be <b><span style='color: #FFD700'>mapped to the minimum value</span></b> we are compressing into
- Any **0** weight values will be <b><span style='color: #FFD700'>mapped to a zero-point</span></b> (*just some offset in the lower precision space*), basically this number in the lower prevision represents 0.

>[!important] If we can compress we can always decompress back
>But this <b><span style='color: var(--mk-color-red)'>decompression will lead to some loss in precision or information</span></b>.

>[!note] Symmetric quantization
>Here we take the max absolute weight value and we will map this to the max and min. We will also center everything around 0 as well (*meaning map 0 to 0*).
>
>But the bad thing about this approach is that we <b><span style='color: var(--mk-color-red)'>might not be using the maximum range of values</span></b>.

So to **do asymmetric quantization we need 2 things**:
1) <b><span style='color: #87CEEB'>Scale factor</span></b>

$$
s = \frac{2^{b} - 1}{max(X) - min(X)}
$$
Where:
- $b$ is the number of bits for the target data type we are compressing into

2) <b><span style='color: #87CEEB'>Zero-point</span></b>

$$
z = - \text{round}(min(X) \times s) - 2^{b - 1}
$$
Then once we have these 2 values to **do quantization**:
$$
X_{quant} = X \cdot s + z
$$
Then for **dequantization**:
$$
X_{dequant} = (X_{quant} - z) / s
$$
>[!question] Now how doe we decide how many bits to compress into
>We can <b><span style='color: #FFD700'>compute an error matrix</span></b>.
>$$
> X_{error} = X_{original} - X_{dequant}
>$$
>If the error for each of the weights is **acceptable** then we can use that number of bits.
### Clipping

However there is **one major flaw** in our approach and that is <b><span style='color: var(--mk-color-red)'>outliers</span></b>.

This is because <b><span style='color: var(--mk-color-red)'>scale factor & zero point uses the max & min</span></b>. So if we have **1 value in 1 end of the spectrum while the rest are on the other** then all of the <b><span style='color: var(--mk-color-red)'>values will be compressed into a small range on 1 side</span></b> (*maybe even the same value*).
 
![[Problem with Outliers in Quantization.png|center|400]]
 
 Not only that but when we **decompress** them, the <b><span style='color: var(--mk-color-red)'>error will be high</span></b> since during compression the values are around the same causing the decompression to result to using the same few values.

We can **solve** this through <b><span style='color: #87CEEB'>clipping</span></b>, which is just the act of <b><span style='color: #FFD700'>cutting weights to a defined maximum & minimum range</span></b>.

Range derived from trained weights using the process of calibration (*mainly for activations*):
- **Static calibration**: find best ranges <b><span style='color: #FFD700'>before inference</span></b> using a calibration dataset (*we decide based on the data*)
- **Dynamic calibration**: after each layer, collect statistics of activations to find best ranges, this is <b><span style='color: #FFD700'>during inference</span></b>

>[!success] Decrease quantization errors of non-outliers

>[!fail] Increase quantization errors of outliers
>But this is alright because we assume that there are very few outliers so the overall effect is positive.
## Quantization Aware Training (QAT)

So here we introduce quantization directly into the pipeline meaning <b><span style='color: #FFD700'>simulated during training</span></b>.

>[!success] Mitigate the effects of post training quantization (PTQ)

So here we **add between layers** a <b><span style='color: #87CEEB'>fake quantization nodes</span></b>, where all it does is <b><span style='color: #FFD700'>quantize & immediately dequantize</span></b>.

>[!question] So what is going on?
> Essentially during 1 forward pass the <b><span style='color: #FFD700'>weights of 1 layer will be quantize & dequantize before outputting</span></b>.
> 
> This allows the model to <b><span style='color: #98FB98'>see the effects of quantization during training</span></b>.

But now the <b><span style='color: var(--mk-color-red)'>issue is backward propagation</span></b>, because quantization is just a <b><span style='color: #FFD700'>mapping so its a step function</span></b> (*in reality it has the `round` operation which is a step function*). So it <b><span style='color: var(--mk-color-red)'>does not differentiate</span></b> well (*not continuous & the gradient is mostly 0*).

So to **get around** this is to use a <b><span style='color: #87CEEB'>straight through estimator</span></b> which treats this <b><span style='color: #FFD700'>fake quantization layer as a identity function</span></b>. So if the <b><span style='color: #FFD700'>weight is between the range return 1 else return 0</span></b>.
# Mixed Precision Training
---
Typically for general usage we do not need such high precision so <b><span style='color: #FFD700'>when users use a model it can be of a lower precision</span></b> (*correct on an acceptable level*).

>[!important] We do not throw away the higher precision weights, we still keep a master copy at high precisions to do gradient updates

Generally this is what happens **during training**:
![[Idea of Mixed Precision Training.png|center|450]]

Here:
- FP32 uses 32 bits, has a high precision & range
- FP16 uses 16 bits
- There is also BF16, uses 16 bits, has a lower precision than FP32 but the same range as FP32

>[!question] Why do we need scaling?
> We scale the loss because our model is on a lower precision. During <b><span style='color: #FFD700'>backward propagation computation is in high prevision but updating will be done in the lower precision</span></b> so we might <b><span style='color: var(--mk-color-red)'>suffer from arithmetic underflow</span></b>. So we <b><span style='color: #98FB98'>scale to ensure that when we get the gradient it is not 0</span></b>.
> 
> Then we need to <b><span style='color: #FFD700'>scale it back because our gradients are based off the scaled loss</span></b> values.

>[!success] Less memory required

>[!success] Faster computation
# KV Caching
---
So when we **do autoregressive text generation** at each step we <b><span style='color: #FFD700'>take the previous input + the newly generated token as input into the decoder</span></b>.

So we can see at <b><span style='color: #FFD700'>each time stamp we have this static input</span></b> (*it does not change*). 

>[!warning] So at each iteration we compute the key & value vectors for the same words we saw in past iterations

So this is where <b><span style='color: #87CEEB'>KV caching</span></b> (*key-value caching*) comes in, we just <b><span style='color: #FFD700'>cache the key & value embeddings of previous words</span></b> (*because they do not change*).

![[KV-Caching Example.png|center|500]]

From here you can see we only need to <b><span style='color: #98FB98'>compute the attention of the new word to all other existing words</span></b> (*while retrieving the KV embeddings from our cache*).

There is <b><span style='color: #FFD700'>no need to cache the query</span></b> because in autoregressive generation after we generate the next word we <b><span style='color: #FFD700'>only pass this word in the next timestamp</span></b>.
## Memory Limitations

That is nice we <b><span style='color: #98FB98'>save a lot of compute</span></b> but where are we storing these intermediate KV embeddings? Yes they are <b><span style='color: #FFD700'>stored in memory typically GPU VRAM</span></b>. So we might <b><span style='color: var(--mk-color-red)'>require additional memory</span></b>.

So this **cache size depends on**:
1)  Sequence length ($t$), <b><span style='color: #FFD700'>size of the input</span></b>
2) Batch size ($b$),<b><span style='color: #FFD700'> how many queries</span></b> (*applicable in both training & inference*)
3) Number of layers in the decoder ($n$)
4) Number of heads in the multi head attention layer ($h$)
5) Embedding size ($d_{model} / h$)
6) Precision of weights ($p$) <b><span style='color: #FFD700'>typically in bytes</span></b>

>[!question] What is batch size?
>So a model can <b><span style='color: #FFD700'>handle multiple queries</span></b> at once so this is called a batch size. And one way to <b><span style='color: #FFD700'>prevent computing attention for between queries is to use masking</span></b>.

>[!info] Points 1 & 2 are run time parameters while the rest are model parameters which we can tune

Then we have to <b><span style='color: #FFD700'>times 2 of this</span></b> because we are storing both key and value. So the total VRAM needed is:
$$
VRAM = 2 \times p \times b \times n \times h \times d \times t 
$$
## Memory Optimisation

We can certainly **do some optimisation tweaks** to ensure our <b><span style='color: #FFD700'>cache does not get too large</span></b>.

So the **basic strategies** are to balance these:
- Model size so our $n$, $h$ & $d$
- Reduce precision (*our [[Year 3/Sem 2/CS4248 - Natural Language Processing/Improving LLMs Efficiency.md#Quantization|quantization]]*)
- Reduce the batch size (*but this comes with reduced efficiency*)

There are also some **advance techniques** (*attention variants*):
- Sliding window attention, where we <b><span style='color: #FFD700'>calculate attention only between the new word & the last k words</span></b>
- Multi-query attention (*MQA*)
- Grouped-query attention (*GQA*)
- Multi-head latent attention (*MLA*), which basically <b><span style='color: #FFD700'>reduce the dimension space of the embedding</span></b> $d$
### Multi-Query  &  Grouped-Query

In our **[[Year 3/Sem 2/CS4248 - Natural Language Processing/Transformers.md#Multiple Head Attention|multi head attention]]**, each head will have its own key & value weight matrix, meaning they <b><span style='color: #FFD700'>each have their own representation of a key and a value</span></b>.

>[!fail] This means we are using way more memory to cache our keys and values

So is there a way to <b><span style='color: var(--mk-color-red)'>lower expressivity to use less space</span></b> but <b><span style='color: #98FB98'>decrease storage</span></b>.

![[MQ & GQ Attention Visualisation.png|center|500]]

So for **grouped query**, we are essentially <b><span style='color: #FFD700'>heads that computes the keys & values similarly are grouped to use 1 value & key weight representation</span></b>.

For **multi query**, we are essentially <b><span style='color: #FFD700'>reducing the number of key and value weights to just have 1 representation</span></b>.

>[!important] Number of heads remain the same it does not change, it just uses the same keys and values

>[!question] Why can we share the key & value weights
>This is because the query will be different for each head so even if we merge heads into 1 we still can get something different.

Then we use <b><span style='color: #FFD700'>mean pooling on the query embeddings for backward propagation</span></b>.

>[!tldr] Mean pooling
>Here we just sum up the embeddings then divide it by the total number of embeddings.
### Multi-Head Latent Attention

Here we are taking the idea from **[[Year 3/Sem 2/CS4248 - Natural Language Processing/Augmenting LLMs.md#LoRA|LoRA]]**. Instead of reducing the number of value, key weight representations, we are just <b><span style='color: #FFD700'>turning them into low dimensions</span></b>.

![[Multi-Head Latent Attention Overview.png|center|450]]

So what is happening is that <b><span style='color: #FFD700'>each head will have its own key, value compression & decompression</span></b> (*as shown in the image*). But we only <b><span style='color: #FFD700'>store the lower dimension embedding</span></b>, then we can revert this whenever we need it.

>[!note] Typically there is 1 global downward projection weight matrix, then each head will have its own key & value upward projection weight matrix.
# Mixture Of Experts
---
You can think of this as <b><span style='color: #FFD700'>using multiple networks in 1 giant model</span></b>. This is an <b><span style='color: #FFD700'>ensemble method</span></b> where <b><span style='color: #FFD700'>each network is an expert</span></b>.

>[!info] This experts can be anything
>From RNN, CNN to transformers. But we prefer to **keep it as a neural network so we can do backward propagation**.

So these experts are good at some things (*like math, coding, semantics etc*). It uses a <b><span style='color: #87CEEB'>gate & a router</span></b> to <b><span style='color: #FFD700'>decide which experts gets which input</span></b> (*gating mechanism not attention*).

>[!tldr] Gate
>It essentially to tell <b><span style='color: #FFD700'>how much to trust</span></b> the model based on this query.
>
>So it basically <b><span style='color: #FFD700'>does a probability distribution</span></b> ($G(x)$) over all the experts (*SoftMax probabilities or logits*).
>
>Its **architecture can be anything**, but <b><span style='color: #FFD700'>typically it is a simple feed forward neural network</span></b> (*or any NN that can determine how much to trust for each experts*).
>
>So typically a gate will have the following function:
>$$
> G(x) = \text{SoftMax}(\text{TopK}(W_{gate}x, k))
>$$
>Where:
>- $W_{gate}x$ is just the matrix multiplication with the gate weight matrix to give us a probability

>[!tldr] Router
>It <b><span style='color: #FFD700'>moves the query</span></b> to the different experts.
>
>So generally we can **just take what the gate gives** but we can also include **additional criteria's** called <b><span style='color: #87CEEB'>routing strategies</span></b>.

So all the <b><span style='color: #FFD700'>experts & the gating mechanism gets done during training</span></b>.

>[!success] We are essentially improving model efficiency through utilising specialised subnetworks 
>Essentially we are using some of the networks not the whole model.

>[!fail] Adds complexity to implementation
>May also need additional tweaks to ensure stable training, load balancing & more. Also we are passing each token, maybe it is more efficient to pass the entire query.
## Routing Strategies
### Dense Mixture Of Experts

So since we are dealing with an **ensemble** method, our <b><span style='color: #FFD700'>output is a weighted sum</span></b>:
$$
y = \sum^{n}_{i = 1} G(x)_{i} E_{i}(x)
$$
Where:
- $G(x)_{i}$ is the weight for expert $i$
- $E_{i}(x)$ is the output from expert $i$

And as the name suggests being dense means that the <b><span style='color: #FFD700'>input is passed to all experts</span></b>.

>[!important] So $G(x)_{i}$ can never be $\le 0$

>[!success] Very easy to implement

>[!success] Often we get a better model accuracy

>[!fail] All network components & weights are involved
>So there is <b><span style='color: var(--mk-color-red)'>no improvement in efficiency</span></b>.
>
>But generally it is worse than a single expert since we are using multiple networks.
### Sparse Mixture Of Experts

So this is the opposite of dense MoE, where we <b><span style='color: #FFD700'>pass the inputs to experts with the highest probability</span></b> (*can be top-k or based on the gate some values are 0*)

So here is what is happening:
1) The **gate** will still give us a probability distribution but <b><span style='color: #FFD700'>gives us the top-k experts</span></b> (*the rest will just be negative infinity*)
2) Then we take these top-k probability & <b><span style='color: #FFD700'>apply SoftMax to ensure that the total distribution sums to 1</span></b> (*so the SoftMax result will be our $G(x)_{i}$* )
3) Then the router will route the inputs to the experts

Then the aggregation is the same as the dense variant.

>[!important] So $G(x)_{i}$ some of them can be  $= 0$

>[!success] Only certain parts of the network are active
>Thus we are <b><span style='color: #98FB98'>improving on efficiency</span></b>.

>[!fail] Naive implementation often shows undesired behaviour
>By choosing the top-k , the gate choose only the most prominent experts. This leads to <b><span style='color: var(--mk-color-red)'>overfitting as only these experts gets trained & increasing their selection chances</span></b>.
>
>So then we are wasting space as our <b><span style='color: var(--mk-color-red)'>model is underutilised</span></b>. This can also lead to <b><span style='color: var(--mk-color-red)'>degradation of the overall performance</span></b>.
>
>And we are also <b><span style='color: var(--mk-color-red)'>reducing diversity</span></b> in learning as we <b><span style='color: #FFD700'>limit the selection of other possible specialised experts</span></b>.

There are different mitigation strategies to solve sparse MoE issues:
- [[Year 3/Sem 2/CS4248 - Natural Language Processing/Improving LLMs Efficiency.md#Stochastic Routing|Stochastic routing]]
- [[Year 3/Sem 2/CS4248 - Natural Language Processing/Improving LLMs Efficiency.md#Load Balancing|Load balancing]]
- Entropy regularisation, where we encourage more diverse expert selection
- Soft routing, where we allow fractional routing decisions
#### Stochastic Routing

So the idea is to <b><span style='color: #FFD700'>add some noise</span></b> to the probability distribution in the gate. This <b><span style='color: #98FB98'>gives all experts a chance to be selected early in training</span></b> (*a more passive load balancer*).

>[!note] We do not need to make the noise static it can be a tunable operation by introduction additional learnable parameters

So now our **gate will look like this**:
$$
G(x) = \text{SoftMax}(\text{TopK}(H(x), k))
$$
$$
H(x) = W_{gate}x + \text{StandardNormal}() \cdot SoftPlus(W_{noise}x)
$$
Where:
- $\text{StandardNormal}() \cdot SoftPlus(W_{noise}x)$ is a tunable gaussian noise
- $\text{StandardNormal}()$ is essentially a random number generator using a bell curved distribution
- $SoftPlus(x) = \ln(1 + e^{x})$ this is a <b><span style='color: #98FB98'>smooth & differential approximation</span></b> of ReLU

>[!question] Why use SoftPlus?
>This is because it <b><span style='color: #FFD700'>always produces a small positive value</span></b>. This makes <b><span style='color: #98FB98'>optimisations more stable</span></b>.
>
>>[!success] Very useful when the activations need to be positive (*for variances or standard deviations*)
>>Can be used in a NN.
#### Load Balancing

So the core idea is that we want all our <b><span style='color: #FFD700'>experts to be equally utilised</span></b>. One strategy is to compute an <b><span style='color: #87CEEB'>auxiliary loss</span></b> to <b><span style='color: #FFD700'>penalize an imbalance utilization of experts</span></b>.

![[Auxiliary Loss for Load Balancing.png|center|400]]

Here are some **global terms**:
- $L_{aux}$ is the auxiliary loss
- $w_{aux}$ is our weight or a hyperparameter to control how strongly the model should care about load balancing
- $N$ the total number of experts (*or* $n$)
- $T$ is the total number of tokens in batch $B$
- $B$ is the called the batch

Now lets look at $\color{#FFD700}{f_{i}}$ which is the <b><span style='color: #FFD700'>fraction of samples routed to that expert</span></b> (*samples just means tokens*). So what does $1\{argmax P(x) = i\}$ mean, it just says if the <b><span style='color: #FFD700'>largest probability for the token is this expert the value is 1 otherwise 0</span></b>.

>[!note] This is the case where the gate only passes to 1 expert
>If we are doing a **top-k approach** then change $argmax$ to $TopK$ where $i \in TopK$.

Now lets look at $\color{#FFD700}{P_{i}}$ which is the <b><span style='color: #FFD700'>fraction of router probabilities allocated to the expert</span></b>. It does not matter if it was actually selected but this compute <b><span style='color: #FFD700'>how confident this expert is for the batch</span></b>.

>[!important] This is the raw probabilities before we select the top-k & apply SoftMax

Once we get these 2 values we will multiply & sum over all experts.
# Distillation
---
We have some large LLM which is costly & slow to run which for most specialised tasks its overkill (*a smaller model is actually good enough*).

So <b><span style='color: #87CEEB'>distillation</span></b> is the process of <b><span style='color: #FFD700'>transfering knowledge from a large model to a smaller one</span></b> (*[[Year 3/Sem 2/CS4248 - Natural Language Processing/Augmenting LLMs.md#Teacher-Generated Data|teacher to student]]*), this process is also known as **transfer learning**.

So as we discuss the different strategies, as **we go down the list**:
- It will result in an <b><span style='color: #98FB98'>increase accuracy & quality of model</span></b>
- But also an <b><span style='color: var(--mk-color-red)'>increase in complexity of code, training & compute</span></b> and also <b><span style='color: var(--mk-color-red)'>more access to the teacher model</span></b>

>[!success] But once we are done we have model that can take less inference power
>This is because it is compact, takes less memory & also less electricity to run.

>[!important] But this most important factor despite the strategies is that we need to have a good teacher
>Typically this means that the loss on the ground truth for the teacher is low.
## Response Distillation

Also known as <b><span style='color: #87CEEB'>output distillation</span></b> which is what we have covered **[[Year 3/Sem 2/CS4248 - Natural Language Processing/Augmenting LLMs.md#Teacher-Generated Data|previously]]**.

![[Response Distillation Overview.png|300]]

Overall essentially we have this unlabeled training data which we <b><span style='color: #FFD700'>ask a larger teacher LLM which will provide us with the true labels</span></b>. This forms the dataset to train the smaller student model.
## Logit Distillation

The **main problem with response distillation** is that it does <b><span style='color: var(--mk-color-red)'>not show how confident the larger model is when outputting </span></b>, so maybe the true label is only 50.1% certain as compared to the rest.

So the <b><span style='color: #FFD700'>student should also not be confident with this output</span></b>, because we are ultimately just trying to mimic the teacher.

![[Logit Distillation.excalidraw.png|center|300]]

>[!idea] The idea is that we want the response distribution of the student model to be the same as the teacher model
>If we do response distillation then it is possible that for this query the student model is very certain but in reality the response from the teacher model is undertain.

>[!question] Why not use the SoftMax probability?
>We can but typically we do not, this is because <b><span style='color: #FFD700'>SoftMax normalise the distribution between 0 & 1</span></b>. 
>
>So we are <b><span style='color: var(--mk-color-red)'>losing a lot of resolution</span></b> (*basically information*) but also <b><span style='color: var(--mk-color-red)'>hides the relative differences between choices</span></b> (*difference between logits*).
>
>>[!example] Example with a simple logit values
>>Lets take the logits for 10 & 9 vs 100 & 99. The second set is very confident with high logits but after SoftMax both will get the same probability.

>[!success] Does not require annotated dataset

>[!success] Logits capture more nuanced knowledge

>[!fail] High dependency on teacher
>Still if the <b><span style='color: var(--mk-color-red)'>teacher is bad or it has some bias</span></b> then it will also be reflected in the student model.
>
>Also <b><span style='color: var(--mk-color-red)'>not all models provides the logits</span></b>, so we can only do it if they expose it.

>[!fail] No grounding in true semantics

>[!fail] Less robust evaluation
>As we are missing the ground truth, we rely on the logits of the teacher model.
### Adding Ground Truth Labels

![[Logit Distillation With Ground Truth.excalidraw.png|center|350]]

This is an extension to logits distillation where we also <b><span style='color: #FFD700'>minimise the student loss based on the ground truth label</span></b> (*now our training data is labeled*).

>[!success] Richer training signal & more stable training

>[!success] Possibly we can converge faster

>[!success] Straightforward evaluation using common metrics

>[!fail] Additional complexity

>[!fail] Risk of conflicting signals

>[!fail] Non-obvious combination of loss terms
>Typically we use some weighted sum.
## Feature  Distillation

If we **have an open source model** we can train our <b><span style='color: #FFD700'>student model to think like the teacher</span></b> (*the internal architecture*).

>[!idea] We do not want the student to align itself with the output but also the process of getting to that output

![[Feature  Distillation.png|center|350]]

>[!example] If our student model is half the size of the teacher model then every layer in the student should represent 2 layers in the teacher model
>The same can be done with the attention heads or any components in the teacher model.

Then we just use some way to <b><span style='color: #FFD700'>compute the divergence</span></b> (*cosine similarity, L1, L2, KL divergence*) <b><span style='color: #FFD700'>of the representations</span></b> of the student & the teacher's architecture.

>[!note] This is often used together with [[Year 3/Sem 2/CS4248 - Natural Language Processing/Improving LLMs Efficiency.md#Logit Distillation|logit distillation]]

>[!success] Even richer signal between just logit distillation

>[!success] Deeper knowledge transfer beyond just outputs

>[!fail] Non-trivial layer alignment if the architectures are very different

>[!fail] Higher complexity & more expensive training

>[!fail] Can only be used with open source or open architecture models
>So if we do not have the architecture & the weights we cannot do this. But we can still do the other 2 methods.



