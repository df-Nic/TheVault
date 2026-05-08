---
Title: Introduction into Connectionist Machine Learning
Date Created: 06-March-2026
Last Updated: 01-May-2026
Tags:
  - CS4248
  - AI/ML/LogisticRegression
  - AI/ML/NN
---
# Generative & Discriminative Classifiers
---
If you recall for any classification task we are trying to find a [[Year 3/Sem 2/CS4248 - Natural Language Processing/Text Classification.md#Formal Setup|function]] that maps the input space to the output space,  $h : X \rightarrow Y$ or $h(x) = y$, which means the model needs to learn $P(Y \vert X)$.

This can be done in 2 basic approaches:
- **Generative** classifiers
Here you learn the <b><span style='color: #FFD700'>joint probability</span></b> of $P(x, y)$ and then <b><span style='color: #FFD700'>apply bayes rule</span></b> to get $P(y \vert x)$. Essentially it <b><span style='color: #FFD700'>learns the data distribution of each class</span></b>, the classifies data by comparing with each class's distribution (*think of it as based on what you observed what class does this sentence belongs to*).

- **Discriminative** classifiers
Here it <b><span style='color: #FFD700'>directly learns</span></b> $P(y \vert x)$. Essentially it <b><span style='color: #FFD700'>learns the decision boundaries</span></b> between classes and then classifiers data depending on the region they fall into.
# Logistic Regression
---
In a logistic regression we **assume** that there is <b><span style='color: #FFD700'>some linear relationship</span></b> (*some weighted sum*) between $x$ and $y$ (*dependent/output/target variable*).

We can express it as such:
$$
\hat{y}^{(j)} = h_{\theta}(x^{(j)}) = f(b + \theta_{1}x_{1}^{j} + \dots + \theta_{n}x_{n}^{j}) = f\left(\sum^{n}_{i = 1} \theta_{i}x_{i}^{j} + b \right)
$$
Where:
- $\theta$ is our <b><span style='color: #FFD700'>parameters that we need to train</span></b> (*or learn*) to find the right values and $\theta \in \Bbb R$
- b is called the <b><span style='color: #87CEEB'>bias</span></b> or offset where $b \in \Bbb R$
- $f$ is some function which we apply to our weighted sum
- $\hat{y}^{(j)}$ is our predicted value
- $x_{i}^{j}$ just means the j-th data point's i-th column value

>[!question] Why do we need the bias?
> The bias is actually our <b><span style='color: #FFD700'>y-intercept</span></b>. If our <b><span style='color: #FFD700'>input values are all 0 we cannot assume that the final output must be 0</span></b>.

We can do a simple <b><span style='color: #87CEEB'>bias trick</span></b> by <b><span style='color: #FFD700'>introducing a constant feature</span></b> $\color{#FFD700}{x_{0}^{j}}$, which will <b><span style='color: #FFD700'>always be 1</span></b> with a weight of $\theta_{0}$ (*which the model now needs to learn as well*). Then our linear sum will just be in terms of $\theta$ and $x$ .

>[!important] $\theta$ will change if we scale the values

So all that is left is to define $f$ and **for logistic regression** we will use the <b><span style='color: #87CEEB'>sigmoid function</span></b> (*or the logistic function*).

>[!tldr] [[Year 2/Sem 1/CS2109S - Introduction to AI & Machine Learning/Logistic Regression.md#Sigmoid Function|Sigmoid function]]
>$$
>f(x) = \frac{L}{1 + e^{-k(x - x_{0})}}
>$$
>
>Typically $k = 1$ and $x_{0} = 0$ and $L = 1$. However the most **important** one is setting $L$ to be <b><span style='color: #FFD700'>1 as this ensures our final output to be between 0 and 1</span></b>.
>
>If $x = 0$, sigmoid will output 0.5, thus <b><span style='color: #FFD700'>providing a clear decision boundary</span></b>. And on top of this it is <b><span style='color: #FFD700'>smooth & differentiable</span></b>.
>
>With this, the output now <b><span style='color: #FFD700'>gives us the probability</span></b> whether the input belongs to which class.

Our **input to this sigmoid function** can be though of as [[Year 1/Sem 2/MA1522 - Linear Algebra for Computing/Matrices.md#Matrix Multiplication|1 big matrix multiplication]]:
- We have $\theta$ which consist of all the weight for $\theta_0$ to $\theta_{n}$, it will look like $(\theta_{0}, \theta_{1}, \dots, \theta_{n})$
- We then have $X$ which is the values (*feature values*) of our input, which will look like $(x_{0} = 1, x_{1}, \dots, x_{n})$

Then we can transpose $\theta$ (*or X depending on how you write it*) to get:
$$
X \theta^{T} = 
\begin{pmatrix} 
	x_{0} & x_{1} & \dots & x_{n}
\end{pmatrix}
\begin{pmatrix}
    \theta_{0} \\
    \theta_{1} \\
    \vdots \\
    \theta_{n}   
  \end{pmatrix} 
   =
  \begin{pmatrix}
    \theta_{0} \times x_{0} + \theta_{1} \times x_{1} + \dots + \theta_{n} \times x_{n}
  \end{pmatrix}$$
Which is essentially what we are trying to do here:
$$
\sum^{n}_{i = 0} \theta_{i}x_{i}^{j}  
$$
>[!important] The value from this summation is not the probability it can be bigger than 1 this is why we use the sigmoid function

Now with the notations out of the way, assume that $h_{\theta} = f(X \theta^{T})$ compute the probability for $y = 1$ (*some class*). This means that $\hat{y} = P(y = 1 \vert X, \theta)$. And if there are only **2 classes** then $\hat{y} =  1 - P(y = 0 \vert X, \theta)$.

>[!info] Typically a threshold of 0.5 is used to denote if $X$ is in this class or not
>But this threshold can be adjusted.
## Finding $\theta$ ?

Different $\theta$ values will result in different probabilities, but how can we find the best one? We can break this down into **2 steps**:
1) We need to know how good the current set of $\theta$ values are
2) How can we update our $\theta$ values to be better

Let's first handle the 1st step which is how to know how good the current $\theta$ is. So we need some <b><span style='color: #87CEEB'>loss function</span></b>.

>[!tldr] Loss function
>You can think of it as <b><span style='color: #FFD700'>how off your model is</span></b> when predicting. Which we will denote as $L(\hat{y}, y)$.
>
>So our goal is always to <b><span style='color: #98FB98'>minimise the loss function</span></b>.

So in logistic regression the **best model** will be the one that <b><span style='color: #FFD700'>maximises the probability of the correct label</span></b>.

Recall that $\hat{y} = P(y = 1 \vert X, \theta) = 1 - P(y = 0 \vert X, \theta)$. **Combining the 2 equations**, we will get:
$$
P(y \vert X) = \hat{y}^{y}(1 - \hat{y})^{1 - y}
$$

>[!important] This is applicable if we are predicting 2 classes only

This essentially for a **problem with 2 classes** if our true label is 1 or 0, essentially one of the terms will be to the power of 0. Thus we just need to maximise $\hat{y}$.

We can **simplify the equation by using logarithms**:
$$
\log P(y \vert X) = y \log \hat{y} + (1 - y) \log (1 - \hat{y})
$$
But this is to maximise the probability, which is the same task as minimising the negation of its value so we **negate the whole thing** and we get the <b><span style='color: #87CEEB'>cross entropy loss</span></b>:
$$
L_{CE} = - [y \log \hat{y} + (1 - y) \log (1 - \hat{y})]
$$
This is only for 1 training sample, the **loss of all training samples** we just <b><span style='color: #FFD700'>take the average</span></b>.
### Gradient Descent

So now how do we find the minimum for our cross entropy loss. Luckily it is a <b><span style='color: #FFD700'>convex function meaning that it has 1 global minimum</span></b> (*because we have n+1 equations and n+1 unknowns*).

>[!fail] The naive way will be to just do random search but this is very slow and impractical

If you recall we can compute the gradient $\delta L / \delta \theta$, with lots of math:
$$
\frac{\delta L_{CE}}{\delta \theta} = - \frac{1}{m}X^{T}[\sigma(X, \theta) - y]
$$
Where:
- $\sigma$ is our sigmoid function
- $m$ is the total number of data samples

So we can set his equation to 0 and solve for $\theta$. However there is <b><span style='color: var(--mk-color-red)'>no close form solution for this</span></b>. Thus we need <b><span style='color: #87CEEB'>gradient descent</span></b> to <b><span style='color: #FFD700'>adjust</span></b> $\color{#FFD700}{\theta}$ <b><span style='color: #FFD700'>iteratively to minimise the loss</span></b>.

For our loss function which is a multivariable function, we will typically take the partial derivative:
$$
\frac{\delta L}{\delta \theta} = 
\begin{bmatrix}
    \frac{\delta{L}}{\delta \theta_{0}} \\
    \frac{\delta{L}}{\delta \theta_{1}} \\
    \vdots \\
    \frac{\delta{L}}{\delta \theta_{n}}   
  \end{bmatrix} 
$$
This resulting vector is our gradient, which <b><span style='color: #FFD700'>points to the steepest ascent</span></b>. Basically, if our $\delta{L} / \delta \theta_{0}$ is **negative**, it means that an <b><span style='color: #FFD700'>increase</span></b> in $\theta_{0}$ will <b><span style='color: #98FB98'>decrease the loss</span></b>. If it is **positive** then an <b><span style='color: #FFD700'>decrease</span></b> in $\theta_{0}$ will <b><span style='color: #98FB98'>decrease the loss</span></b> (*and vice versa for both*).

The **larger** the gradient, the <b><span style='color: #FFD700'>larger it affects change in the loss value</span></b>.

So we <b><span style='color: #FFD700'>adjust the our weights by reducing it off by the gradient</span></b>. But if we just do this the change might be drastic, thus we have something called a <b><span style='color: #87CEEB'>learning rate</span></b> ($\alpha$) (*typically it is from 0.0001 - 0.01*).

So our update will be $\theta \leftarrow \theta - (\alpha \cdot \frac{\delta L}{\delta \theta})$

>[!question] How learning rate affects the change in $\theta$
>![[How Learning Rate Affects Weight Update.png|center|500]]
>
>Therefore we <b><span style='color: #FFD700'>avoid high learning rates</span></b>.

There are a few **variations** to gradient descent:
1) **Basic** gradient descent
Also known as <b><span style='color: #87CEEB'>batch gradient descent</span></b>, is where we <b><span style='color: #FFD700'>compute the average loss over the entire training dataset</span></b>, then we compute the gradient based on this average.

It results in:
- Smooth descent
- Smaller gradients
- Smaller update steps

>[!success] Stable convergence

>[!fail] Slow if we have a very large dataset

>[!fail] Memory heavy because we are computing matrix multiplications on a large dataset

2) **Stochastic** gradient descent

Instead of computing the loss over the entire training dataset we just <b><span style='color: #FFD700'>use 1 random datapoint to compute the gradient</span></b> (*does not choose the same point in future iterations*).

>[!success] Very fast

>[!success] Uses very little memory

>[!success] Escapes local minima
>Because gradient from a single point can be noisy which we have a chance to escape a local minima

>[!fail] Highly volatile
>Since we are using 1 data point to update the weights.

3) **Mini-batch** gradient descent

Here we <b><span style='color: #FFD700'>take a small batch of datapoints</span></b> (*these will not be picked in future iterations*), then compute the gradient.

It results in:
- Choppy descent
- Larger gradients
- Larger update steps

>[!success] Balance between speed and a smoother update

>[!warning] Choosing the correct batch size can make a difference
>Too small and it becomes stochastic, too large it just becomes the normal gradient descent.

So now **when do we stop**?
- If the change in loss is below a certain threshold
- If our loss is small enough
- Max number of iterations is reached

This is so that if we reach a <b><span style='color: var(--mk-color-red)'>almost flat gradient</span></b>, updates will be small and <b><span style='color: var(--mk-color-red)'>convergence to the global minimum will be slow</span></b>.
## Overfitting & Regularisation

Our trained model can fall under one of these categories:
- **Underfitting**, low training & test accuracy, because the <b><span style='color: var(--mk-color-red)'>model fails to capture the relationship</span></b> of the data 
- **Good fit**, a balance between high train & test accuracy, the <b><span style='color: #98FB98'>ideal outcome</span></b>
- **Overfitting**, high training but low test accuracy, because the <b><span style='color: var(--mk-color-red)'>model over generalises with the training data</span></b>.

>[!warning] Typically if one of the weights ($\theta$) is way larger than other weights, then there is some overfitting going on

To handle overfitting, we use <b><span style='color: #87CEEB'>regularisation</span></b> techniques to <b><span style='color: #FFD700'>penalize large weight values</span></b>.

There are **2 types** of regularisation:
1)  **Ridge** regression (*L2*)
$$
\lambda \sum^{n}_{i = 1} \theta_{i}^{2}
$$
2) **Lasso** regression (*L1*)
$$
\lambda \sum^{n}_{i = 1} \vert \theta_{i} \vert
$$
Where:
- $\lambda$ is a hyper parameter to control the strength of the regularisation
- $n$ is the number of weights or $\theta$

>[!info] L1 can do feature selection as it shrinks the weights to zero for L2 it brings it close to 0 but never 0

So depending on which one you want to use, <b><span style='color: #FFD700'>just add this to your loss function</span></b>.
## Multiclass Problems

So far we only talk about when there are 2 classes. For a **multiclass** problem we will have $C$ number of probabilities where $C$ is the number of classes.

Instead of the sigmoid function use the <b><span style='color: #87CEEB'>SoftMax function</span></b> to <b><span style='color: #FFD700'>squishes all the scores into a probability that sums to 1</span></b>.

$$
P(y = c \vert X) = \frac{e^{X^{T}\theta_{c}}}{\sum^{C}_{i = 1} e^{{X^{T}\theta_{i}}}}
$$
Where:
- $\theta_{c}$ is the weights for the model to predict if the data point belong to class $c$

Then our **generalized cross-entropy loss function** will be:
$$
L_{CE}(\hat{y}, y) = - \sum^{C}_{i = 1}y_{i} \log(\hat{y}_{i})
$$
Where:
- $y_{i} = 1$ for the true class (*correct class*) for data point $i$ and 0 otherwise
- $\hat{y}_{i}$ is the probability output after SoftMax for predicating class $c$

>[!note] This make computing the loss function simpler as we only need the probability for the true class, the rest will just be 0
# Introduction To Neural Networks
---
There are **limitations** to logistic regression models namely because its a <b><span style='color: var(--mk-color-red)'>linear model</span></b>. This means that it is limited to:
- Linear combination of features
- Linear decision boundaries

Here is where **neural networks** comes in, it helps <b><span style='color: #FFD700'>handle non linear relationships</span></b>.

>[!info] In terms of logistic regression we are building a "stacked" logistic regression
>Meaning we pass the input into multiple neurons or in another standpoint multiple logistic regression models.

**Example of a neural network**:
![[Simple Neural Network Example.png|center|400]]

>[!note] There can be more than 1 output neuron

Our NN can be **stacked for**:
- **Width**, which mean many neurons in 1 layer
- **Depth**, which mean that neurons from the previously layer will be passed into more layers of neurons

In a neural network, **each neuron will take** in:
- A set of inputs multiplied by their weights
- Sum the values up
- Pass this summation into an <b><span style='color: #87CEEB'>activation function</span></b>

So <b><span style='color: #FFD700'>computing the output is just 1 big matrix multiplication</span></b>.

>[!tldr] Activation functions
>They are just regular functions which you just pass in the weighted sum and outputs something. So in the case of a logistic regression it will be the Sigmoid function.
>
>>[!important] These activation functions must be a non linear function
>>If it is a linear function then the model will collapse into a single layer. Because it can be <b><span style='color: #FFD700'>combined into a set of matrix multiplications</span></b> (*but adding it does not cause an error it just makes the model not able to learn complex relationships*).
>>
>>This is how we add non-linearity to our neural networks.
>
>There are a wide range of activation functions:
>- Sigmoid
>- Sign
>- Tanh
>- ReLU (*Rectivified linear unit*)
>- Leaky ReLU (*prevents gradient vanishing*)

>[!tldr] Hidden layers
>Hidden layers are <b><span style='color: #FFD700'>neurons other than the input layers & the output</span></b> layers. They are hidden because we <b><span style='color: #FFD700'>will not get to see their output</span></b>.
>
>And based on the <b><span style='color: #DDA0DD'>universal approximation theorem</span></b>, we actually only need 1 hidden layer to approximate any continuous function in the $\Bbb R^{n}$ space. 

>[!note] In our example this neural network is a Feedforward NN
>This is because it <b><span style='color: #FFD700'>contains no loops</span></b>.

As the NN gets more complex it will be hard to **tell which values belong to which weights**, for this course it uses this **notation**:
$$
\theta^{[l]}_{i, j}
$$
Where:
- $l$ is the layer level in the neural network, <b><span style='color: #FFD700'>1 being the first hidden layer</span></b> (*0 will be the input layer*)
- $i$ is the index of the neuron in layer $l$, <b><span style='color: #FFD700'>1 being the first neuron</span></b>
- $j$ is the index of the neuron in layer $l - 1$, <b><span style='color: #FFD700'>0 if there is no previous neuron</span></b> (*for the bias*)

So if we put all the weights in the matrix, $i$ is your row and $j$ is the column.

>[!example] So if we were to take our example above
>The weight for the bias in our hidden layer to the output layer will be:
>$$
>\theta^{[2]}_{1, 0}
>$$

Then now how do we **compute the weights**? So everything is the [[Year 3/Sem 2/CS4248 - Natural Language Processing/Introduction into Connectionist Machine Learning.md#Gradient Descent|same as the gradient descent]] in logistic regression. We <b><span style='color: #FFD700'>define the loss function and then minimise it</span></b>.

But now we need to do <b><span style='color: #87CEEB'>backwards prorogation</span></b>:
- **Forward** pass to compute the output (*input to output*)
- **Backward** pass to compute the gradients (*output to input*)

>[!success] And since everything is a matrix we can do it all in 1 big matrix multiplication with parallelism though GPUs

We can still apply the same [[Year 3/Sem 2/CS4248 - Natural Language Processing/Introduction into Connectionist Machine Learning.md#Overfitting & Regularisation|regularisation]] techniques to prevent overfitting of our neural network.

>[!fail] It will be harder to do gradient descent for NN
>As the loss function is not a <b><span style='color: var(--mk-color-red)'>convex function</span></b> (*think of a landscape visualisation lots of crevices*), meaning there can be <b><span style='color: var(--mk-color-red)'>local minima</span></b>. 

