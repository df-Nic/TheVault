---
Title: Encoder & Decoder
Date Created: 28-March-2026
Last Updated: 04-April-2026
Tags:
  - CS4248
  - AI/ML/NN/RNN
  - AI/ML/NN/Encoder
  - AI/ML/NN/Decoder
---
# Recurrent Neural Network
---
So previously we use an [[Year 3/Sem 2/CS4248 - Natural Language Processing/N-Gram Language Models.md#N-Gram Language Models|n-gram model to predict the next word utilizing the Markov assumption]]. Typically you would, **take the most likely word** but you can also do **random sampling** (*nothing wrong here*).

>[!abstract] Autoregressive Generation
>This process of picking the next word condition on $k$ previous words (*n-gram*) will only **terminate** when:
>- Reaching a <b><span style='color: #FFD700'>pre-determined length</span></b>
>- Until an <b><span style='color: #FFD700'>end-of-sequence token</span></b> is generated
>  

So **how does it work in practice**? Well as we **increase n** the <b><span style='color: #98FB98'>sentences gets more fluent</span></b>, but we need to <b><span style='color: var(--mk-color-red)'>have an exponential amount of information</span></b> ($V^{n}$).

But the main issue is that it <b><span style='color: var(--mk-color-red)'>does not capture long distance dependencies thus our Markov assumption does not hold</span></b>. Our n-grams can only capture so much information & <b><span style='color: #FFD700'>words outside the n-gram will not get considered</span></b>.

>[!note] So n-gram language models are not designed for text generation but rather just tell you the next most likely word

So this is where <b><span style='color: #87CEEB'>recurrent neural network</span></b> (*RNN*) come in.
## Basic Idea Of RNN

**Basic idea of RNN**:
![[RNN Basic Idea.png|center|400]]

>[!important] We are dealing with a fully connected neural network

So the only thing special is that now there is a concept of a <b><span style='color: #87CEEB'>hidden state</span></b> where we <b><span style='color: #FFD700'>pass in the output of the hidden layer back to itself in the next time step</span></b> (*size of this hidden state = size of hidden layer*).

So we want this <b><span style='color: #FFD700'>hidden state to have information of all the words it has seen</span></b> up till that time stamp.

So the **general formula for computing this hidden state** is:

$$
h_{t} = f_{\theta}(h_{t - 1}, x_{t})
$$

Now we just need to know what the **activation function** is, and typically we use the <b><span style='color: #87CEEB'>tanh function</span></b>:

$$
tanh(x) = \frac{e^{x} - e^{-x}}{e^{x} + e^{-x}}
$$

So putting everything together:

$$
h_{t} = tanh(\theta_{hh} h_{t - 1} + \theta_{xh}x_{t})
$$
Where:
- $\theta_{hh}$ of size $H \times H$ is essentially the weight matrix (*each neuron will have a set of weights for the past state*) to convert the hidden states from the previous time stamp
- $\theta_{xh}$ is the weight matrix of size $E \times H$ (*each neuron will have a set of weights for the input*) to convert the input to values which are input to each of the hidden layer neurons
- $h_{t - 1}$ is the hidden state from the previous time stamp
- $x_{t}$ is the input (*does not have to be text can be anything as long as it is embedded*) for the current time stamp
- $E$ is the word embedding size
- $H$ is the size of the hidden state

>[!important] ALL the weights are same throughout each time stamp

>[!important] The hidden state $h_{t}$ is not your output, we will need a $\theta_{hy}$ and some activation function to get the final output

Then we can do <b><span style='color: #FFD700'>backward propagation through time to update the weights</span></b> (*applying chain rule*).

>[!failure] But there is a huge problem which is we need to propagate the loss till time t = 1
>This thus allows our RNN model to suffer from <b><span style='color: var(--mk-color-red)'>vanishing or exploding gradients</span></b> (*gradients become 0 or too large respectively*). And it also takes a <b><span style='color: var(--mk-color-red)'>long time</span></b>.
>
>>[!question] How to mitigate this?
>>We can being back the **Markov assumption**, instead of backpropagating till the beginning, we can <b><span style='color: #FFD700'>do it for a particular window size</span></b>. But now it is <b><span style='color: var(--mk-color-red)'>not completely correct & is just an approximation</span></b>.
>
>>[!success] To solve this issue we can use different variations of RNN like long short term memory or gated recurrent unit
>>![[LSTM & GRU Overview.png|center|500]]

There are also different **types of RNN**:
![[Images/CS4248 Images/Types of RNN.png|center|400]]
## RNN For Language Modeling

We can **use the autoregression generation** to allow us to **use RNN's for language modeling**. Take a input, <b><span style='color: #FFD700'>predict the next word & use the prediction as the next input</span></b>. But now we have a <b><span style='color: #FFD700'>hidden state which passes in information in order of the previous words</span></b>.

>[!info] You do not need to start with a start of sentence symbol, you can give seed words
>These are <b><span style='color: #FFD700'>optional</span></b> but you can <b><span style='color: #FFD700'>start with some guiding words</span></b>.
>
>Then for these seed words you can omit that time stamp's prediction and just <b><span style='color: #FFD700'>use the actual word as the next input</span></b>.

So essentially <b><span style='color: #FFD700'>everything is the same</span></b> just that our <b><span style='color: #FFD700'>final output layer will be the size of our vocabulary</span></b> ($\theta_{hy}$ *a H by V matrix and passed through a SoftMax after matrix multiplication*).

>[!important] The only new thing you need is a embedding layer before you input anything to the RNN
# Conditional RNNs
---
Our vanilla [[Year 3/Sem 2/CS4248 - Natural Language Processing/Encoder & Decoder.md#Recurrent Neural Network|RNN]] is unconditional (*ok not really it is conditioning on the previous inputs*). But what we mean by <b><span style='color: #FFD700'>conditional is that it take in some information from the user</span></b>.

>[!question] So what are we doing here?
>Essentially the RNN's prediction is based on the dataset. But now we want to <b><span style='color: #FFD700'>predict based on what the user wants</span></b>.

So we now just introduce a new variable for the **user context** ($c$). So now our probability to sentence generation will be $P(w_{1}, \dots, w_{N}) \rightarrow P(w_{1}, \dots, w_{N} \vert c)$.

Then we can **apply the chain rule & the Markov assumption** to compute that probability:
$$
P(w_{1}, \dots, w_{N} \vert c) = \prod_{i = 1}^{N} P(w_{i} \vert c , w_{1 : i - 1}) \approx \prod_{i = 1}^{N} P(w_{i} \vert c , w_{i - k: i - 1})
$$
## Encoder & Decoder

>[!abstract] Encoder
>Essentially it takes an input (*does not have to be text*) and then <b><span style='color: #FFD700'>converts it into some lower-dimension representation</span></b> (*sparse to dense*) this is our context ($c$).

>[!abstract] Decoder
>It does the opposite, it takes our lower-dimension representation (*the context*) & <b><span style='color: #FFD700'>reconstruct the original form</span></b> (*dense to sparse*). But it is used to <b><span style='color: #FFD700'>output a sequence of words using the context</span></b>.

>[!warning] But as always when doing this, there will generally be some loss of information
>But hopefully we keep the important bits of information. 

>[!abstract] In the past
>the **encoder takes a user context**, then it uses a <b><span style='color: #87CEEB'>convolutional sentence model</span></b> (*CSM*). It then <b><span style='color: #FFD700'>takes the output from the CSM and multiply it with some weight vector</span></b>.
> $$
> s = \theta_{cs}CSM(\text{sentence})
> $$
>>[!abstract] Convolutional Sentence Model
>>At a high level it maps sentences into vectors.
> 
> Then our **decoder** will use the <b><span style='color: #FFD700'>output of our encoder and incorporate it when predicting the hidden state</span></b>.
> $$
> h_{t} = \sigma(\theta_{hh}h_{t - 1} + \theta_{xh}x_{t} + s)
> $$
> Then apply SoftMax to get the output.

<b><span style='color: #FFD700'>Now we use an RNN for both the encoder & decoder</span></b>:
- Our **encoder** (*many to 1*)
$$
h^{\text{enc}}_{t} = tanh(\theta^{\text{enc}}_{hh}h^{\text{enc}}_{t - 1} + \theta^{\text{enc}}_{xh}x_{t})
$$

>[!note] There is no need to compute the output as the output of the last hidden state will be input for the decoder

- Our **decoder**
$$
h^{\text{dec}}_{t} = tanh(\theta^{\text{dec}}_{hh}h^{\text{dec}}_{t - 1} + \theta^{\text{dec}}_{xh}x_{t})
$$
Now we output something so:
$$
y^{\text{dec}}_{t} = softmax(\theta^{\text{dec}}_{hy}h^{\text{dec}}_{t})
$$

>[!important] At time t = 1 for the decoder, which is the start of the decoding process
>$$
>h_{0}^{\text{dec}} = h_{T}^{\text{enc}}
>$$
>
>Also the first input to the decoder is usually a start of sentence token

>[!fail] During training the decoder might get a incorrect prediction in the next time stamp, causing this error to propagate
>So during training we can do <b><span style='color: #98FB98'>teacher forcing which just gives the ground truth word to the next iteration</span></b>.

>[!note] So the encoder and decoder can be the same RNN model, they can also be 2 different RNN models
>But they are <b><span style='color: #FFD700'>all trained at the same time not separately</span></b>.
## Attention

Now the big bottleneck is that for the last hidden state $h^{\text{enc}}_{T}$ for the encoder, it <b><span style='color: var(--mk-color-red)'>must capture all the information about the source sentence</span></b>.

Core idea is <b><span style='color: #87CEEB'>attention</span></b>, which is to give the decoder <b><span style='color: #FFD700'>"direct access" to the encoder to focus on different parts in the source sentence</span></b> (*all timestamps*).

>[!success] It alleviates the bottleneck problem

>[!success] Significantly improve performance

>[!success] Helps with the vanishing / exploding gradient problem in training

>[!success] Provides some interpretability through attention weights
>The larger attention score it means the model takes more information from that encoder's hidden state. But this is not always the case.

**Overview of the attention layer**:
![[Attention Overview.png|center|250]]

Where:
- The <b><span style='color: #98FB98'>green</span></b> box is our decoder (*right box*)
- The <b><span style='color: var(--mk-color-red)'>red</span></b> box is our encoder (*left bottom*)
- The <b><span style='color: #87CEEB'>blue</span></b> box is our attention layer (*left top*)

So how does it work, so in our **typical RNN decoder & encoder nothing changes**. It is only **after when the decoder compute its hidden state** then the attention comes in:
1) <b><span style='color: #FFD700'>Compute the attention score</span></b>

Looking at our diagram the decoder block is pointing to 3 circles, these **circles** are the <b><span style='color: #FFD700'>hidden state of our encoder at all time stamps</span></b>. We will then <b><span style='color: #FFD700'>compute</span></b> the <b><span style='color: #87CEEB'>attention score</span></b> for each time stamp which we will denote as $e_{i}$.

There are many **scoring function** (*so just pick one*):
$$
e_{i} = score(h_{t}, h_{s}^{(i)}) =
\begin{cases}
h_{t}^{T}h_{s}^{(i)}  & \text{dot product} \\
h_{t}^{T}\theta_{a}h_{s}^{(i)} & \text{general where $\theta$ is a hyper parameter} \\
v^{T}_{a} tanh(\theta_{a}[h_{t}^{T}, h_{s}^{(i)}]) & \text{concat}
\end{cases}
$$

Where:
- $h_{t}$ is the hidden state of the decoder at time $t$
- $h_{s}^{(i)}$ is the hidden state of the encoder at time $i$

2) <b><span style='color: #FFD700'>Compute the attention weights</span></b>

After computing the score we will pass each of the scores through a SoftMax layer to get the <b><span style='color: #87CEEB'>attention weights</span></b> which we denote as $a_{i}$. We will get essentially probabilities, which also <b><span style='color: #FFD700'>denotes which hidden state to pay more attention to</span></b> (*because we get a attention distribution*).

Just a recap the SoftMax function is:
$$
a_{i} = \frac{exp(e_{i})}{\sum_{i}exp(e_{i})}
$$

3) <b><span style='color: #FFD700'>Compute the context vector</span></b>

Here will will take the <b><span style='color: #FFD700'>attention weights and multiply it with the corresponding encoder hidden state</span></b> & then just <b><span style='color: #FFD700'>sum it all up</span></b>, this will give us the <b><span style='color: #87CEEB'>context vector</span></b> which we denote as $c_{t}$

$$
c_{t} = \sum_{i} a_{i} \times h_{s}^{(i)}
$$
>[!note] Note that $a_{i}$ is a scalar not a vector, so we are taking a vector an multiply it with a constant

4) Compute the output for the decoder

This is nothing new we still use the SoftMax function but instead of just the hidden state we will <b><span style='color: #FFD700'>concatenate it with the context vector</span></b>.

>[!abstract] Concatenate vectors
>It just means it just <b><span style='color: #FFD700'>appends another vector to the back</span></b>.
>
>So for example if we have $[1, 2, 3]$ and $[4, 5, 6]$ we will just get $[1, 2, 3, 4, 5, 6]$.

So now the output is:
$$
y_{t} = softmax(\theta_{hy}[c_{t} , h_{t}])
$$
Where:
- \[  \] we denote this as to concatenate 2 vectors together

>[!important] Now our $\theta_{hy}$ instead of just $H \times V$ it will be $2H \times V$ now since we concatenate it with the context vector

And then we **repeat step 1 for the next iteration of the decoder** (*attention is only computed for the encoder not the decoder*).

>[!abstract] Query, key, value
>Sometimes, attention can be thought of these 3 things (*QKV*).
>
>If you think about it, the <b><span style='color: #FFD700'>query is our input for the decoder</span></b>.
>
>Our <b><span style='color: #FFD700'>keys are the encoder's hidden state</span></b> ($h^{\text{enc}}_{T}$), because these hidden states of the encoder tells us more about the <b><span style='color: #FFD700'>value</span></b> (*score times the hidden state*).
>
>So attention in 1 single formula is:
>$$
>\text{Attention}(Q, K, V) = \text{SoftMax}\left(\frac{QK^{T}}{\sqrt{d_{k}}}\right)V
>$$
>Where:
>- $d_{k}$ are the size of your key or query (*both os this have the same size*)
>  
> Scaling using $\sqrt{d_{k}}$ <b><span style='color: #98FB98'>leads to more stable gradients</span></b>.
## Beam Search Decoding

So far we are used to <b><span style='color: #87CEEB'>greedy decoding</span></b>, which is to just <b><span style='color: #FFD700'>pick the word with the highest probability</span></b> (*argmax*).

>[!question] Will this yield the best result?
>No not always, if we were to <b><span style='color: var(--mk-color-red)'>do greedy decoding, we might miss the optimal subsequence</span></b> (*we pick the most likely word at the start it will affect the rest of the downstream sequence*).
>
>Sometimes we might want the same input to <b><span style='color: #98FB98'>yield different results</span></b>.

>[!fail] Naive idea of computing all possible sequences of $y$ & picking the most likely one is slow
>This exhaustive search is very slow as it will take $O(V^{T})$ time.

So in <b><span style='color: #87CEEB'>beam search decoding</span></b>, we want to <b><span style='color: #FFD700'>pick a likely word</span></b> (*not most likely*). Essentially we will <b><span style='color: #FFD700'>keep track of some number of probable patrial outputs</span></b> (*top few words*).

>[!important] But our end goal is still the same which is to maximise the probability of the output sentence given the source sentence
>
> $$
> P(y \vert x) = P(y_{1} \vert x) \times \dots \times P(y_{t} \vert x, y_{1}, \dots, y_{y - 1}) = \prod^{T}_{t = 1} P(y_{t} \vert x, y_{1}, \dots y_{t - 1})
> $$
> 
>But take note that beam search <b><span style='color: var(--mk-color-red)'>does not guarantee a optimal solution</span></b>, but it is less greedy & <b><span style='color: #98FB98'>more efficient than exhaustive search</span></b>.

So when doing beam search we need to **compute the score of our partial sentence**:
$$
\text{score}(y_{1}, \dots, y_{t}) = \sum^{t}_{t = 1} \log{P(y_{i}\vert x, y_{1} \dots, y_{i - 1})}
$$
Where:
- $x$ is the source sentence
- $y$ is the words that are outputted

To **conduct** bean search decoding:
1) Find the $k$ most likely sequences  from all the partial sentence from the previous time stamp
2) Compute the score for each of the new partial sequence in the current time stamp
3) Then select only the $k$ most likely partial sequence (*these are called hypothesis*)
4) Repeat step 1

>[!example] Example of conducting beam search decoding
> ![[Beam Search Example.png|center|450]]

So you might **get a end of sentence token** (`</s>`*for instance*) mid way through the beam search. Then that <b><span style='color: #FFD700'>means the hypothesis or sentence for that beam is finished, but you still need to continue with the rest</span></b>.

>[!question] So when to stop?
>There are some **conditions** that are generally used:
> - When we hit a <b><span style='color: #FFD700'>maximum number of decoding steps</span></b> (*maximum number of tokens*)
> - Or at least <b><span style='color: #FFD700'>some number of hypothesis is complete</span></b> (*some number of beans predicted the end of sentence token*).
>
>Then we just pick the sequence with the highest score (*after summing all the paths*).
### Sampling Strategies

We can go even further, besides taking the sentence with the highest probability, we can also do <b><span style='color: #FFD700'>some sampling to get more variation in our output sequece</span></b>:

1) **Pure** sampling

So we can just <b><span style='color: #FFD700'>randomly sample from the probability distributions of all our sentences from beam search</span></b>. So essentially we are doing a weighted sampling based on their final score / probability.

2) **Top-m** sampling

So out of all our sentences from beam search we only <b><span style='color: #FFD700'>consider words with m-highest probabilities</span></b>.

If $m = 1$, it is a greedy search, if $m = V$ than it is pure sampling.

>[!warning] The value of $m$ does affect the final output
>Setting $m$ to be <b><span style='color: #FFD700'>lower, the output is more generic</span></b>.
>
>Setting $m$ to be <b><span style='color: #FFD700'>larger, the output is more diverse but risky</span></b>.

