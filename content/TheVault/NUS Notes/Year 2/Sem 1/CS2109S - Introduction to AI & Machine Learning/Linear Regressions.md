---
title: Linear Regressions
Date Created: 2024-09-09
Last Updated: 2025-09-28
tags:
  - CS2109S
  - AI/ML/LinearRegression
---
# What is Linear Regressions
---
Suppose that we have a set of data and we want to find a <b><mark style='background:var(--mk-color-yellow)'>linear</mark></b> **relationship with all these variables with a response variable** (*We are just finding the best fit line*).

And then with some data that is unseen, **predict what is the response value**. This is essentially what a <span style='color:var(--mk-color-turquoise)'>linear regression model</span> tries to do.

In general a <span style='color:var(--mk-color-turquoise)'>linear regression</span> will follow this <span style='color:var(--mk-color-orange)'>general formula</span>:
$$
h_{w}(x) = w_{0} + w_{1}x + w_{2}x + \dots
$$
**Where:**
- $h_{w}$ is our <span style='color:var(--mk-color-yellow)'>hypothesis</span> of the relationship
- $w$ is the <span style='color:var(--mk-color-yellow)'>model coefficient</span> based on the variable
## Non-Linear Relationships

Sometimes a variable will **not be linear** to the response variable. Some <span style='color:var(--mk-color-orange)'>ways to counteract</span> this is by:
- Taking the **log** of the variable
- Using <span style='color:var(--mk-color-yellow)'>higher order polynomials</span> in our hypothesis function ($x^{2}$, $x^{3}$, etc)
- Model the hypothesis function to use a function (*Example :* $h(x) = w_{0} + w_{1}f_{1}(0) + \dots$).
# Measuring Fit
---
Let our dataset be in the following format: $\{ (x_{1}, y_{1}), \dots, (x_{n}, y_{n})\}$.

A way to measure how good the fit is, by computing <span style='color:var(--mk-color-turquoise)'>average mean squared error</span> as follows:
$$
\text{MSE} = \frac{1}{2n} \sum^{n}_{i=1}(h_w(x_{i}) - y_{i})^{2}
$$
**Where:**
- $\frac{1}{2n}$ is just to **get the average** (*2 is just for mathematical convenience*) 

We want to make **MSE as low** as possible as it means the <span style='color:var(--mk-color-green)'>model has a better fit</span>.

> [!faq] What is Error?
> <span style='color:var(--mk-color-red)'>Error</span> is essentailly the <span style='color:var(--mk-color-yellow)'>difference between</span> the **predicted** value ($\hat{y}$) against the **actual** value.
> 
> And by **observing the MSE formula**, the error is just this part:
> $$
> h_{w}(x_{i}) - y_{i}
> $$
## Gradient Descent

An <span style='color:var(--mk-color-green)'>efficient</span> way of **finding the minimum point for MSE** is not by iterating every value of $w$ but to do <span style='color:var(--mk-color-turquoise)'>gradient descent</span>.

**Example:**
![[MSE Function Against w_1.png|center|250]]

By plotting points using the **MSE formula**, a **quadratic curve** can be formed. Thus we can use [[Partial Differentiation#Partial Differentiation|partial differentiation]] to <span style='color:var(--mk-color-yellow)'>find the minimum point</span> for each values of $w$. This works because **MSE** is a <span style='color:var(--mk-color-yellow)'>convex function</span> (*1 minimum point*).

Then we will <span style='color:var(--mk-color-yellow)'>update</span> $w_{i}$ with the <span style='color:var(--mk-color-yellow)'>value of the gradient</span>.

> [!info] Partial differentiate MSE
> Suppose that our $h_{w}(x) = w_{0} + w_{1}x + w_{2}x$. And we fix $w_{0} = 0$
> 
> Eeach of the $w_{1}$ to $w_{n}$ we will **partial differentiate it with respect** to $w_{i}$ (*The rest are constants except $w_{i}$*).
> 
> **Example:**
> $$
> -\frac{\partial MSE}{\partial w_{1}} = -\frac{1}{m}\sum^{n}_{i = 1}(h_{w}(x_{i}) - y_{i})x_{i}
> $$
> 
> >This is with <b><mark style='background:var(--mk-color-yellow)'>respect to our loss function</mark></b> is not always MSE
> 
> **Why use gradient** is because it <span style='color:var(--mk-color-yellow)'>points in the direction of the greatest increase</span>.

In addition, instead of scaling $w_{i}$ by the gradient, we can add a <span style='color:var(--mk-color-turquoise)'>learning rate</span>, which is essentially a <span style='color:var(--mk-color-orange)'>constant</span> to <span style='color:var(--mk-color-yellow)'>scale the gradient by some factor</span> to update $w_{i}$ <span style='color:var(--mk-color-green)'>faster</span> or <span style='color:var(--mk-color-red)'>slower</span>.

If the learning rate is **too small**, it will take <span style='color:var(--mk-color-red)'>too long to reach the minimum</span>, if it is **too large**, it might <span style='color:var(--mk-color-red)'>bounce around and not reach the minimum</span>.

> [!question] Work around for large epochs?
> Gradient descent for large epoch you can <span style='color:var(--mk-color-yellow)'>start with a higher learning rate</span> then **as you iterate** <span style='color:var(--mk-color-yellow)'>decrease the learning rate</span>.
> 
> This is known as <span style='color:var(--mk-color-turquoise)'>learning rate scheduler</span>.

We can represent the gradient for all $w_{i}$ as a **vector** at some point:
$$\text{Gradient} =
\left(
\begin{matrix}
\frac{\partial MSE(w)}{\partial w_{0}} \\
\frac{\partial MSE(w)}{\partial w_{1}} \\
\vdots \\
\frac{\partial MSE(w)}{\partial w_{i}}
\end{matrix}
\right)
$$
In a nutshell, we will <span style='color:var(--mk-color-yellow)'>repeat</span> this process until the **minimum is reached** or the **increase in weights are minimal**.

Is is important when **calculating the gradient for the subsequent points** after $w_{i}$ <b><mark style='background:var(--mk-color-yellow)'>reuse the old value</mark></b> of $w_{i}$ and <b><mark style='background:var(--mk-color-red)'>not the new one</mark></b>.

> [!summary]  Updating a Weight
> With <span style='color:var(--mk-color-blue)'>gradient descent</span>, we will have calculated $frac{\partial MSE}{\partial w_{1}}$.
> 
> Then to update $w_{1}$ for instance do the following:
> $$
> w_{1} = w_{1} - \gamma(\frac{\partial MSE}{\partial w_{1}})
> $$
> 
> Where $\gamma$ is the learning rate. 

### Variation of Gradient Descent

So far the method covered is called <span style='color:var(--mk-color-turquoise)'>batch</span> gradient descent which takes <span style='color:var(--mk-color-yellow)'>all the data to find the minimum point</span>.

|                                                Batch Gradient Descent                                                |                                              Mini-Batch Gradient Descent                                               |                                   Stochastic Gradient Descent                                    |
| :------------------------------------------------------------------------------------------------------------------: | :--------------------------------------------------------------------------------------------------------------------: | :----------------------------------------------------------------------------------------------: |
|                   Uses <span style='color:var(--mk-color-yellow)'>all</span> the training example                    |            Considers <span style='color:var(--mk-color-yellow)'>a random subset</span> (*Sample*) at a time            |    Select <span style='color:var(--mk-color-yellow)'>1 random data</span> point per iteration    |
| <span style='color:var(--mk-color-red)'>Cannot escape</span> the **local minima** since<br>it takes the optimal path |                 It is <span style='color:var(--mk-color-green)'>cheaper / faster</span> per iteration                  |   It is the <span style='color:var(--mk-color-green)'>cheapest / fastest</span> per iteration    |
|                                                                                                                      | There are elements of randomness<br>which can escape <span style='color:var(--mk-color-green)'>the local minima</span> | More randomness and may <span style='color:var(--mk-color-green)'>escape the local minima</span> |
**Visualisation of the 3 variants**
![[Gradient Descent Variants Visualisation.png|center]]
### Normalisation

When doing gradient descent lets say we modify $w_{1} \rightarrow 5$ and $w_{2} \rightarrow 20000$. Then the <span style='color:var(--mk-color-yellow)'>model essentially only considers</span> $w_{2}$ (*Optimises only* $w_{2}$), which is a problem.

One way is to <span style='color:var(--mk-color-turquoise)'>normalise</span> the values of the particular variable using the following formula:
$$
x_{j} = \frac{x_{j} - \mu_{j}}{\sigma_{j}}
$$
**Where:**
- $\mu_{j}$ is the <span style='color:var(--mk-color-yellow)'>average of the values</span> in that variable
- $\sigma_{j}$ is the <span style='color:var(--mk-color-yellow)'>standard deviation</span> of the variable

We will **repeat** this for all values with in the variable.

There are also <span style='color:var(--mk-color-orange)'>other ways</span> like:
- Min-max scaling
- Robust scaling
- Different learning rates for each $w$

> **Another method** instead of using the normalisation is to <span style='color:var(--mk-color-yellow)'>have a specific learning rate for each variable</span>.
# Normal Equation
---
As from [[#Gradient Descent|gradient descent]] we can observe that we are finding the minimum using differentiation which can be easily <span style='color:var(--mk-color-yellow)'>achieved by setting the gradient to be 0</span>, which is what <span style='color:var(--mk-color-turquoise)'>normal equation</span> does.

**Normal equation example:**
![[Normal Equation Example.png|center|500]]

A one important condition is that $X^{T}X$ <b><mark style='background:var(--mk-color-yellow)'>must be invertible</mark></b> and it can be <span style='color:var(--mk-color-red)'>slow</span> if the number of features is large. To check we can calculate the [[Matrices#Determinant|determinant]].

What if it <span style='color:var(--mk-color-red)'>is not invertible</span>?
- Can try a pseudo inverse ([[Orthogonality#Least Squares Solution|Least squares solution]])
- Or we can get a invertible matrix by $X^{T}X + \alpha I$ for some large $/alpha$

> [!info] Pros & Cons
> Below is a <span style='color:var(--mk-color-yellow)'>summary</span> on the **pros and cons** between gradient descent and normal equation.
> 
> ![[Pros & Cons of Gradient Descent & Normal Equaltion.png|center]]
> 

Note that $w_{0}$ is a constant and thus we need to <span style='color:var(--mk-color-yellow)'>add a variable</span> with values of all 1.