---
title: Neural Network on Sequential Data
Date Created: 2024-11-07
Last Updated: 2025-09-28
tags:
  - CS2109S
  - AI/ML/NN
---
# Sequential Data
---
Unlike other types of data <span style='color:var(--mk-color-turquoise)'>sequential data</span> is data where there is some form of <span style='color:var(--mk-color-yellow)'>ordering is involved</span>. For example:
- **Text data**
- **Audio data**
- **Video data** (*The order of the frames matter*)
## One-hot Encoding

So how can we <span style='color:var(--mk-color-orange)'>encode text</span> input so that it can be **processed by the computer**. One way is through <span style='color:var(--mk-color-turquoise)'>one-hot encoding</span>.

It <span style='color:var(--mk-color-yellow)'>compresses a text into an array</span> where:
- The **length of the array** is the <span style='color:var(--mk-color-yellow)'>number of unique words</span> in the input text
- The array will contain <span style='color:var(--mk-color-yellow)'>one 1 and the rest will be 0</span>, the 1 specifies where the **word is located at in the string**.

> [!example] One hot encoding example
> Assume we have a text, "We saw this saw"
> 
> We will have **3 unique words** thus our array length will be 3, and this is the <span style='color:var(--mk-color-orange)'>corrosponding encoding</span>:
> - We `[1, 0, 0]`
> - saw `[0, 1, 0]`
> - this `[0, 0, 1]`
> - saw `[0, 1, 0]`
> 
> So **each element in the list** will be an <span style='color:var(--mk-color-yellow)'>input to the neural network</span>.

One <span style='color:var(--mk-color-red)'>downside</span> to this is that if the **ordering of the words does not matter then it will be fine**. But if it does matter then the **2 "saw"** will be <span style='color:var(--mk-color-red)'>treated as the same input and thus will have the same output</span> which **might not always be the case** depending on what you are predicting.

Thus **contextual information** is needed. And this is where <span style='color:var(--mk-color-turquoise)'>recurrent neural network</span> (*RNN*) becomes useful.
# Recurrent Neural Network
---
![[RNN Example.png|center|300]]
**Where:**
- $X_{t}$ is the input
- $H_{t-1}$ is the neuron in the network ($H_{0}$ is the bias)
- $\hat{Y}_{t}$ is the output for input $X_{i}$

The above is a **general visualisation** of how a **RNN model looks like**. It passes the <span style='color:var(--mk-color-yellow)'>output from the previous neuron into the next neuron</span>, this is what <span style='color:var(--mk-color-green)'>allows RNN to understand contextual information</span>.

It does not have to connect to $H_{t+1}$ it can **loop back to itself**. This means that the <span style='color:var(--mk-color-yellow)'>same weights are used by the same</span> $X_{t}$.

And if we instead **add more neurons** ($H_{i}$) instead of just outputting the result then we will get a <span style='color:var(--mk-color-turquoise)'>deep neural network</span>.
## Bidirectional Recurrent Neural Network

![[Bidirectional RNN Model.png|center]]

A <span style='color:var(--mk-color-turquoise)'>bidirectional RNN</span> is essentially <span style='color:var(--mk-color-yellow)'>2 RNN model combined</span>. It can get the contextual information from inputs <span style='color:var(--mk-color-yellow)'>before and after</span>. Thus making it <span style='color:var(--mk-color-green)'>more informatic</span>.
## Long Short-Term Memory

Also known as <span style='color:var(--mk-color-turquoise)'>LSTM</span> and it is a <span style='color:var(--mk-color-yellow)'>RNN with gating</span>.

**Visualisation of a Gate**
![[LSTM Visualisation.png]]

> [!info] One hot encoding example
> There are 4 main components but only <span style='color:var(--mk-color-orange)'>3 of them are considered gates</span>:
> - **Input gate** - Use the input or not
> - **Output gate** - Output something or not
> - **Forget gate** - Use the data in memory or not

So how do we **determine** what is $z$, $z_{i}$, $z_{o}$ and $z_{f}$. First we will take the output from $h_{t - 1}$ and the current input $x_{t}$ and then <span style='color:var(--mk-color-yellow)'>concatenate them both</span>. Then there are <span style='color:var(--mk-color-yellow)'>4 different weights for all the inputs which will be applied</span> (*Example*: $W_{c}[h_{t - 1}, x_{t}]$).

Then for the **memory cell** at $c_{t - 1}$ is used to <span style='color:var(--mk-color-yellow)'>generate the next memory cell</span> at $c_{t}$.

**Visualisation of a LSTM neuron**
![[LSTM Neuron Visualisation.png|center|400]]

## Types of RNN Architecture

![[Types of RNN Architecture.png|center]]

# Self Attention
---
The advantage of RNN is that it can <span style='color:var(--mk-color-green)'>capture contextual information from previous time stamps</span>. However this brings about a problem which is that at time $t$ it <span style='color:var(--mk-color-yellow)'>must wait for all previous steps to finish before computing</span>, which is <span style='color:var(--mk-color-red)'>not parallelism friendly</span>.

This is where the <span style='color:var(--mk-color-turquoise)'>self-attention layer</span> comes in. To solve this issue, at $x_{t}$ we need to <span style='color:var(--mk-color-yellow)'>know if all other inputs are relevant</span> and thus we need something called a <span style='color:var(--mk-color-turquoise)'>attention score</span>.

**Calculating attention score for 2 inputs**:
![[Calculating Attention Score.png|center]]

**An overview of a self attention layer**:
![[Overview of a Self Attention Layer.png|center]]

However we **can compute** $H$ ($h_{1}, h_{2}, \dots, h_{n}$) <span style='color:var(--mk-color-orange)'>all at the same time</span> using **6 matrix multiplications**:
![[Matrix Multiplication for Self Attention Layer.png|center]]
><span style='color:var(--mk-color-charcoal)'>Note that the example shows an input size of 4</span>
## Applications of Self Attention Layer

One popular application is the <span style='color:var(--mk-color-purple)'>transformer</span> (*used in GPT*), which is primary used in **translation of languages**. It <span style='color:var(--mk-color-orange)'>contains 2 parts</span>:
1) **Encoder**
2) **Decoder**

**Example of a transformer**
![[Transformer Visualisation.png|center]]

Here the <span style='color:var(--mk-color-purple)'>self attention layer</span> is the same as before but the <span style='color:var(--mk-color-turquoise)'>encoder-decoder attention layer</span> is different. As mentioned previously there are <span style='color:var(--mk-color-orange)'>3 pieces of information</span> which are needed in a self attention **layer, query, key and value**.

In a <span style='color:var(--mk-color-turquoise)'>encoder-decoder attention layer</span>:
1) **Query** is the **output generated** by the <b><mark style='background:var(--mk-color-yellow)'>self-attention layer in the decoder block</mark></b>
2) **Key** is from the <span style='color:var(--mk-color-yellow)'>output from the encoder</span>
3) **Value** is from the <span style='color:var(--mk-color-yellow)'>output from the encoder</span>

This allows the decoder to utilize the <span style='color:var(--mk-color-yellow)'>rich contextual information provided by the encoder</span>.

There is also something called a<span style='color:var(--mk-color-turquoise)'> vision transformer</span>, which **takes in images instead of text**. We can <span style='color:var(--mk-color-yellow)'>break down images into smaller segments</span> and <span style='color:var(--mk-color-yellow)'>pass it in some sequential order</span> into the RNN.
# Dropout
---
There are <span style='color:var(--mk-color-orange)'>2 known issues with deep learning</span>, they are <span style='color:var(--mk-color-red)'>overfitting</span> and <span style='color:var(--mk-color-red)'>gradient vanishing/exploding</span>.

We can solve overfitting through a <span style='color:var(--mk-color-orange)'>regularisation technique</span> called <span style='color:var(--mk-color-turquoise)'>dropout</span>. It is the process of <span style='color:var(--mk-color-yellow)'>randomly setting some activation function</span> to 0 ($g(x) = 0$).

![[Dropout Visualisation.png|center]]

This <span style='color:var(--mk-color-yellow)'>adds randomness into our inputs</span> which makes it **harder for the model to understand our training data**, therefore <span style='color:var(--mk-color-green)'>preventing overfitting</span>.
# Early Stopping
---
This method also <span style='color:var(--mk-color-green)'>prevents overfitting</span> as well.

![[Bias Vs Variance.png|center]]

At some point during training, the **training error will reduce but the validation or test error will start to go up**. Then at this point we can simply <span style='color:var(--mk-color-yellow)'>stop the training of the model</span>.
# Gradient Vanishing/Exploding
---
This happens due to <span style='color:var(--mk-color-yellow)'>certain usage of activation functions</span> and <span style='color:var(--mk-color-yellow)'>how backward propagation works</span>. 

> [!info]  Sigmoid Function
> Lets look at the <span style='color:var(--mk-color-blue)'>sigmoid function</span>.
> 
> In backwards propogation we will take the <span style='color:var(--mk-color-yellow)'>derrivative of the activation function</span> for the output which is $\sigma(x)(1 - \sigma(x))$ which has **a maximum value of 0.25**.
> 
> And thus as we compute backwards propogation many times, then at some point the <span style='color:var(--mk-color-yellow)'>gradient will be very small and reaches almmost 0</span>.

<span style='color:var(--mk-color-turquoise)'>Vanishing gradient</span>: <span style='color:var(--mk-color-yellow)'>Small gradients</span> got multiplied again and again until it reaches almost 0

<span style='color:var(--mk-color-green)'>Exploding gradient</span>: <span style='color:var(--mk-color-yellow)'>Large gradients</span> got multiplied again and again until it overflows

To solve this just <span style='color:var(--mk-color-yellow)'>use different activation functions</span> that are not saturating such as <span style='color:var(--mk-color-blue)'>ReLu</span>. Or we can <span style='color:var(--mk-color-yellow)'>define a range for the gradient</span> thus clipping the gradient with in range.