---
title: Introduction to Neural Networks
Date Created: 2024-10-23
Last Updated: 2025-09-28
tags:
  - CS2109S
  - AI/ML/NN
---

# Perceptron
---
In neural network a <span style='color:var(--mk-color-turquoise)'>perceptron</span> is an AI representation of a **neuron in the brain**. It consists of multiple inputs, each with their own weights and a activation function.

**Example:**
![[Perceptron Example.png|center|300]]

And this is **very similar** to our <span style='color:var(--mk-color-teal)'>hypothesis function</span> as mentioned previously:
$$
\hat{y} = h_{w}(x) = g(\sum^{n}_{i = 0} w_{i}x_{i})
$$
**Where:**
- $g(z)$ is our <span style='color:var(--mk-color-teal)'>activation fcuntion</span>
## Perceptron Learning Algorithm

Like in the case for a [[Year 2/Sem 1/CS2109S - Introduction to AI & Machine Learning/Logistic Regression#Dealing with Continuous Variables|logistic regression model]], the <span style='color:var(--mk-color-teal)'>sign function</span> in this case (*Not sigmoid or step function*) <span style='color:var(--mk-color-red)'>is not differentiable</span>. Therefore we **cannot apply gradient descent**.

This is why this algorithm came about.

> [!abstract] Perceptron Learning Algorithm
> Initalize $\forall w_{i}$ some initial weight
> 
> Have a **loop which will iterate** until <span style='color:var(--mk-color-yellow)'>convergence</span> or <span style='color:var(--mk-color-yellow)'>max steps</span> has been reached.
> - For each $x_{i}$, get a prediction ($\hat{y}$) with the current weights.
> - Select <b><mark style='background:var(--mk-color-yellow)'>just one</mark></b> <span style='color:var(--mk-color-red)'>misclassified</span> instance.
> - **Update the weights** like in gradient descent $w \leftarrow w + \gamma (y_{i} - \hat{y}_{i})x_{i}$
> 
> >Note that $w$ and $x_{i}$ is the weight vector and all the $x$ values for $x_{i}$.

The ordering of the points **matters** it can **give different weights** and it can also <span style='color:var(--mk-color-green)'>help converge faster</span>.

**One downside** to this algorithm is that if the <span style='color:var(--mk-color-yellow)'>dataset is not linear separable</span>, then it <span style='color:var(--mk-color-red)'>will never converge</span>.
### Why Does it Work?

Here is the reasoning of why this <span style='color:var(--mk-color-yellow)'>works for calcification with 2 outcomes</span>.

![[Why Does the Perceptron Learning Algorithm Work.png|center]]

> [!note] Recap on Dot Product
> Give $v \cdot u$. This can be rewritten as the following:
> $$
> \vert\vert v \vert\vert \times \vert\vert u \vert\vert \times \cos\theta
> $$
> 
> Where $\theta$ is the angle between the 2 vectors $v$ and $u$.

Essentially if we misclassify $y$ to be -1 (<i><span style='color:var(--mk-color-red)'>Negative</span></i>) then $\theta$ will be <span style='color:var(--mk-color-yellow)'>between 90 and 180 degrees</span>. 

And if we $y$ to be 1 (<i><span style='color:var(--mk-color-green)'>Positive</span></i>) then $\theta$ will be <span style='color:var(--mk-color-yellow)'>between 0 and 90 degrees</span>. 

By taking the sum or minus of the 2 vectors we are <span style='color:var(--mk-color-yellow)'>essentially shifting the theta</span> down or up so that it will **classify correctly because of the value of** $\theta$.
# Single-Layer Neural Networks
---
The <span style='color:var(--mk-color-purple)'>perceptron model</span> that we have describe earlier is a **successor to the neural networks**.

Usually, a neural network the <span style='color:var(--mk-color-teal)'>activation function</span> <span style='color:var(--mk-color-yellow)'>can be many different types of function</span> (*can be non-linear*).

**Examples of different activation function:**
![[Different Types of Activation Function.png|center|350]]

> [!abstract] Representing Other Types of Models
> A **neural network** can <span style='color:var(--mk-color-yellow)'>represent other models</span> mentioned previously as well:
> 1) **Logistic regression** - Use no activation function or a <span style='color:var(--mk-color-yellow)'>linear activation function</span> ($g(x) = 1$)
> 2) **Binary classcification** - Use the <span style='color:var(--mk-color-yellow)'>sigmoid activation function</span>
> 3) **Multi-class classcification** - Use the <span style='color:var(--mk-color-yellow)'>softmax activation function</span>
> 
> **Softmax activation function:**
> $$
> g(z) = \frac{e^{z_{i}}}{\sum^{C}_{j = 1} e^{z_{j}}}
> $$

A <span style='color:var(--mk-color-turquoise)'>single layer neural network</span> is just **1 neuron** which takes in some inputs and then outputs something based on the activation function.

> [!question] How to improve?
> To help a single-layer NN **perform better**, we can **add more features** of <span style='color:var(--mk-color-yellow)'>different polynomials</span>.
> 
> However this makes it <span style='color:var(--mk-color-red)'>computationally more expensive</span> and is more <span style='color:var(--mk-color-red)'>prone to overfitting</span>.

**Example by modeling a NOR gate:**
![[Single-Layer Neural Network for the NOR Gate.png|center|550]]
# Multi-Layer Neural Network
---
A neural network might <span style='color:var(--mk-color-red)'>not converge</span> if the <span style='color:var(--mk-color-yellow)'>data is not linearly separable</span>. Therefore to **model more complex data**, we can <span style='color:var(--mk-color-yellow)'>add more single-layer neurons</span> to form a <span style='color:var(--mk-color-turquoise)'>multi-layer neural network</span>.

**Example by modeling a XNOR gate:**
![[Multi-Layer Neural Network for a XNOR Gate.png|center|550]]

For both single and multi layer neural network we can get the <span style='color:var(--mk-color-orange)'>output through matrix multiplication</span> with the general formula:
$$
\hat{y} = g_{l}(W^{T}_{l}g_{l-1}(W^{T}_{l-1}\dots g_{1}(W^{T}_{1}x)))
$$
Essentially we will <span style='color:var(--mk-color-yellow)'>start from the left</span> and **do a matrix multiplication** $W^{T}x$ which will give us a matrix ($x_{l+1}$) which will be used for layer $l + 1$.

To get $W$, each **column will be a neuron** <span style='color:var(--mk-color-yellow)'>starting from the top most neuron</span>. The row will be the weights for each input.

Thus for column $c$ will be for neuron $c$. Each **row will be the weights** of all the inputs from <span style='color:var(--mk-color-yellow)'>top to bottom</span>.

> [!question] How to improve
> To help a multi-layer NN **perform better**, we <span style='color:var(--mk-color-yellow)'>expand in depth or breath wise</span>.
> 
> Increasing <span style='color:var(--mk-color-green)'>breath wise is more efficient</span> than height wise.
> 
> However this makes it <span style='color:var(--mk-color-red)'>computationally more expensive</span> and is more <span style='color:var(--mk-color-red)'>prone to overfitting</span>.
# Difference Between NN and Other Models
---
As we mentioned previously a neural network can <span style='color:var(--mk-color-yellow)'>create a logistic and linear regression models</span>.

The main difference is that for linear regression or SVM, to **handle non-linear data** <span style='color:var(--mk-color-yellow)'>handcrafted feature mapping is required</span>, where as for NN, the model will <span style='color:var(--mk-color-green)'>learn its own feature mapping</span> **just by adding more layers**.

Though for NN, it is <span style='color:var(--mk-color-red)'>still non-robust</span> **unlike SVM** which maximises the marine (*NN no margin only decision boundary*).

# Gradient Descent on Neural Network
---
The general equation for the [[Linear Regressions#Gradient Descent|gradient descent]] is:
$$
w_{i} \leftarrow w_{i} - \gamma \frac{\delta{L}}{\delta{w_i}}
$$
And by <span style='color:var(--mk-color-blue)'>chain rule</span>:
$$
\frac{\delta{L}}{\delta{w_{i}}}= \frac{\delta{L}}{\delta{\hat{y}}}\frac{\delta{\hat{y}}}{\delta{a}}\frac{\delta{a}}{\delta{w_i}}
$$

> [!info] Derivative of a Sigmoid Function
> $$
> \frac{\delta{\sigma}}{\delta{x}} = \sigma(x)(1 - \sigma(x)) \rightarrow \hat{y}(1 - \hat{y})
> $$

**Summary of chain rule**
![[Cases of Chain Rule.png|center|400]]
><span style='color:var(--mk-color-charcoal)'>Note that there are 2 cases for chain rule</span>.
## Gradient Descent on Single-Layer NN

So we know that the loss is $L = \frac{1}{2}(\hat{y} - y)^{2}$ (*Mean square error*), $\hat{y} = \alpha(a)$ and $a = \sum^{n}_{i = 0} w_{i}x_{i}$.

And if we follow the <span style='color:var(--mk-color-blue)'>chain rule</span> above with the following equations we will get:
$$
\frac{\delta{L}}{\delta{w_{i}}} = (\hat{y} - \hat{y})\hat{y}(1 - \hat{y})x_{i}
$$
## Gradient Descent on Multi-Layer NN

For this type of neural network we will use <span style='color:var(--mk-color-turquoise)'>backpropagation</span>. Before this when we **calculate the value at a specific neuron** we will do $g(w_{0}x_{1}+ w_{1}x_{1} + \dots)$, there is a term for this and it is called <span style='color:var(--mk-color-turquoise)'>forward propagation</span>.

**How backpropagation works**
![[Visualisation of Backpropagation.png|center|550]]

The **orange boxes** represents <span style='color:var(--mk-color-orange)'>forward propagation</span>, while the blue boxes represent <span style='color:var(--mk-color-blue)'>backwards propagation</span>. We will **need both** to <span style='color:var(--mk-color-yellow)'>calculate the gradient with respect to a certain weight</span>.

In general the <span style='color:var(--mk-color-orange)'>derivative of loss with respect to a weight</span> ($w_{i}$) will be:
$$
\frac{\delta L}{\delta w_{1}} = \frac{\delta L}{\delta u_{i}} \times \frac{\delta u_{i}}{\delta w_{1}} = \frac{\delta L}{\delta u_{i}} \times v_{i} 
$$
><span style='color:var(--mk-color-charcoal)'>Note that the symbols are based on the image above</span>.

For the <span style='color:var(--mk-color-blue)'>blue boxes</span> (*backwards propagation*) instead of starting from the beginning, we will <span style='color:var(--mk-color-yellow)'>start from the output neuron</span>.

> [!question] Getting the Values for the Blue Boxes
> **First** we need to compute $\delta L / \delta \hat{y}$ which is just to <span style='color:var(--mk-color-yellow)'>differentiate the loss function</span> with respect to $\hat{y}$.
> 
> Then <span style='color:var(--mk-color-orange)'>base on chain rule</span>:
> $$
> \frac{\delta L}{\delta u_{i}} = \frac{\delta L}{\delta \hat{y}} \frac{\delta \hat{y}}{\delta u_{i}}
> $$
> 
> Then we know that at **neuron** where $\hat{y}$ is calculated, $\hat{y} = u_{1}w_{1} + \dots + u_{i}w_{i} + \dots$.
> 
> <span style='color:var(--mk-color-yellow)'>Differentiating with respect to</span> $u_{i}$ we will get $w_{i}$. Thus it will just be:
> $$
> \frac{\delta L}{\delta u_{i}} = \frac{\delta L}{\delta \hat{y}} \times w_{i}
> $$
> 
> Then we continue and move accordingly.

# Computer Vision to Analyse Images
---
So how can use use <span style='color:var(--mk-color-purple)'>neural network</span> to classify an image? Well we can by asking it to analyse the pixels of an image.

Given an image of size $n$ by $m$ a naive way is to just take every pixel as an input parameter which which will mean that our <span style='color:var(--mk-color-purple)'>NN</span> will have a input size of $n \times m$, which<span style='color:var(--mk-color-red)'> can be very large</span>, thus <span style='color:var(--mk-color-red)'>computationally expensive</span>.

> [!note] Modeling a NN to classify an Image
> ![[Neural Network Analysing Images.png|center|500]]
> 
> Lets look at the **example** above, we can see that each pixle is its own input to the <span style='color:var(--mk-color-purple)'>NN</span>. 
> 
> To predict what image this is, we can model the images to <span style='color:var(--mk-color-yellow)'>find certain aspects of the image</span> for example the eyes, mouth, ears, tail etc. Which will be their own neuron.
> 
> Then based on these observations we can <span style='color:var(--mk-color-yellow)'>combine the result at the end to get a prediction</span>.

## Convolution Layer

Why not we <span style='color:var(--mk-color-yellow)'>only visualise a subset of pixels</span> as an input rather than each individual pixel. This method allows us to <span style='color:var(--mk-color-green)'>solve the issue of too many inputs</span>. Using this is <span style='color:var(--mk-color-purple)'>NN</span> is also known as <span style='color:var(--mk-color-turquoise)'>convolution neural network</span>.

**Example of a convolution layer**
![[Convolution Layer.png|center|400]]

General formula is: Output Dimension = [(Input Dimension - Kernel Dimension + 2 * Padding) / Stride] + 1

Essentially we will have a<span style='color:var(--mk-color-yellow)'> filter or a kernel</span> which will <span style='color:var(--mk-color-yellow)'>convert the input into a feature mapping</span> for a specific neuron (*1 feature 1 unique filter*). 

For instance if we have a ear detector neuron, this kernel will feature map the input into a **smaller input** representing the ears. Possibly by setting the weights in the top half of the matrix $W$ to have a higher number.

> [!attention] Is it necessary to Shrink the Input Size
> For one yes this method does reduce the input size but what are we potentially <span style='color:var(--mk-color-red)'>missing here is the information from the edges</span> since by applying a filter some corder pixes of **information will be "removed"**.
> 
> Therefore a **common practice** is to <span style='color:var(--mk-color-yellow)'>add a padding</span> around the input matrix. Which will <span style='color:var(--mk-color-yellow)'>retain the original shape</span> of the input in the feature mapping. Thus<span style='color:var(--mk-color-green)'> retaining information from the input</span>.

Pairing with **padding**, we can also use <span style='color:var(--mk-color-turquoise)'>strides</span>, which is essentially the <span style='color:var(--mk-color-yellow)'>step size the filter takes</span>. So after the first processing, it will **move left** by $x$ times (*default is 1*) **same for going downwards**.

**Dealing with RGB inputs**
![[Neural Network on a RGB Input.png|center]]

It is the same as before just that for **each RGB it will be their own input matrix**.
## Pooling Layer

This layer essentially just <span style='color:var(--mk-color-yellow)'>down samples the feature mapping</span> or in other words lowers the dimension of the feature mapping.

Some <span style='color:var(--mk-color-orange)'>aggregation methods used</span> in this pooling layer are:
1) **Max-pool**
2) **Average-pool**
3) **Sum-pool**

Thus **given some boundary and the aggregation method**, it will output a <span style='color:var(--mk-color-yellow)'>smaller feature mapping</span>. It usually works along side convolution layers.

### Convolution Neural Network Structure

**Overview of the CNN structure**
![[Convolution Neural Network Structure.png|center]]
