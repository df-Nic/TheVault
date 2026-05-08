---
Title: Support Vector Machines
Date Created: 28-November-2025
Last Updated: 08-February-2026
Tags:
  - CS2109S
  - AI/ML/SVM
---
# Problem of Overfitting
---
So what causes <span style='color:var(--mk-color-red)'>overfitting</span>, it happens when the <span style='color:var(--mk-color-yellow)'>model captures more features of the dataset</span>. This in turn will results in a <span style='color:var(--mk-color-yellow)'>complex polynomial hypothesis which oscillates</span> a lot and <span style='color:var(--mk-color-red)'>will not do well with test data</span> but will <span style='color:var(--mk-color-green)'>do very well with train data</span>.

![[Visualisation of Overfitting.png|center|400]]

> [!question] How to Address Overfitting?
> As we know a overfitted model will have a **very complexy polynomial** (*Lots of features*).
> 
> To <span style='color:var(--mk-color-orange)'>reduce overfitting</span> we can do the following steps:
> 1) **Reduce the number of features** - Just remove some polynomial terms
> 
> 2) **Regularization** - Keeps all features but <span style='color:var(--mk-color-yellow)'>reduces the magnitude of the weights</span>
> 
> **Regularizaion** follows <span style='color:var(--mk-color-turquoise)'>Occam's razor</span>, which states that **simple is ususally better**.
# Regularization
---
Let us recap on the <span style='color:var(--mk-color-teal)'>loss function</span> that was thought:
$$
j(w) = \frac{1}{2m} [\sum^{m}_{i = 1}(h_{w}(x^{(i)}) - y^{(i)})^{2}]
$$
Our goal is to <span style='color:var(--mk-color-orange)'>minimise it</span> since it will mean that our predications are close to the actual values. So how can we reduce the magnitude of the weights. 

We can <span style='color:var(--mk-color-yellow)'>penalise the model for using large weights</span> by adding some constant multiply by the weights. Now we force the model to make <span style='color:var(--mk-color-green)'>good predications while using small weight values</span>.

But what to penalize, if you are not sure **just penalize everything!**

Thus our <span style='color:var(--mk-color-teal)'>loss function with regularisation</span> will now be:
$$
J(w) = \frac{1}{2m} [\sum^{m}_{i = 1}(h_{w}(x^{(i)}) - y^{(i)})^{2} + \lambda\sum^{n}_{j = 1}w_{j}^{2} ]
$$
**Where:**
- $\lambda$ is some constant or **penalization factor**
- And the summation is the **sum of all the weight values squared**

This is known as <span style='color:var(--mk-color-turquoise)'>ridge regression</span> or **L2**, there is also <span style='color:var(--mk-color-orange)'>another regularisation</span> called <span style='color:var(--mk-color-turquoise)'>LASSO regression</span> or **L1** (*feature selection*), where instead of sum of square, we will take the <span style='color:var(--mk-color-yellow)'>sum of  absolute value of the weights</span>.

> [!info] Choosing the right $\lambda$
> Essentially, to choose the right value for $\lambda$ is by **trial and error**.
> 
> However, if we choose the $lambda$ value to be **close to 0**, then it is the <span style='color:var(--mk-color-yellow)'>same as having no regularization</span> and this the model will <b><span style='color:var(--mk-color-red)'>still be overfitted</span></b>.
> 
> If the $\lambda$ is **too high**, then the weights will <span style='color:var(--mk-color-yellow)'>natually go to 0</span> which will result in the bias being left and thus the <b><span style='color:var(--mk-color-red)'>model underfits</span></b>.

Thus in <span style='color:var(--mk-color-teal)'>gradient descent with regularisation</span>, it will be:
$$
\left(1 - \frac{\gamma\lambda}{m}w_{n}\right) - y \frac{1}{m}\sum^{m}_{i = 1}(h_{w}(x^{(i)}) - y^{(i)})x_{n}^{(i)}
$$

**MAE and MSE** are <span style='color:var(--mk-color-red)'>susceptible to outliers</span>. Use <span style='color:var(--mk-color-turquoise)'>Huber loss</span> (*A combination of MAE and MSE*) or <span style='color:var(--mk-color-turquoise)'>log-cosh loss</span> (*Small values it will be similar to MSE but larger values it will be MAE*).

While for the <span style='color:var(--mk-color-teal)'>normal equation with regularisation</span>, it will be:

![[Normal Equation with Regularisation.png|center]]

In the original normal equation, we need to ensure that $X^{T}X$ is **invertible** but for regularisation, it <span style='color:var(--mk-color-yellow)'>will work if its not invertible but</span> $\lambda \gt 0$.
# Support Vector Machine
---
In a logistic regression model we can find a **boundary the separates the 2 groups**. In SVM, we are trying to <span style='color:var(--mk-color-yellow)'>maximise the margin</span> (*distance*) between the 2 groups while <b><mark style='background:var(--mk-color-yellow)'>maintaining the partition</mark></b> (*Also known as* <span style='color:var(--mk-color-turquoise)'>hard margin</span>).

This is why <span style='color:var(--mk-color-green)'>SVM model is robust</span> since it maximises the margin thus it is <span style='color:var(--mk-color-green)'>not prone to misclassification</span>.

We define the <span style='color:var(--mk-color-turquoise)'>margin</span> as $\frac{2}{\vert\vert w \vert\vert}$ and we will <span style='color:var(--mk-color-green)'>want to maximise this value</span> where $w$ is the set of all the weights.

We know that the <span style='color:var(--mk-color-teal)'>decision boundary</span> is when $w \cdot x \ge c$ we classify this data point as <span style='color:var(--mk-color-green)'>positive</span> (+). We can stretch the boundary of this decision by adding and subtracting some constant $k$ for both classes. $c$ is like the <span style='color:var(--mk-color-turquoise)'>bias</span>.

> [!example] Creating a Margin
> We know that for a point to be <span style='color:var(--mk-color-green)'>classcified as positive</span>, $w \cdot x - c \ge 0$ This is the decision boundary. To create a margin, we can do the following:
> 1) $w \cdot x - c + k \ge 0$, for the <span style='color:var(--mk-color-green)'>positive class</span>
> 2) $w \cdot x - c \ge 0 - k$, for the <span style='color:var(--mk-color-red)'>negative class</span>
> 
> We are trying to draw a line that **pushes the 2 classes far away from the decision boundry**.

**Example of a margin**
![[Example of a Margin.png|center|400]]

If we set the positive class as $y = 1$ and the negative class as $y = -1$, then based on our equation above we can get the following, $y^{(i)}(w \cdot x^{(i)} + c) - 1 \ge 0$. This means that <span style='color:var(--mk-color-yellow)'>for all points, the prediction times the actual value will be greater than 0</span>.

> If the equation results in a <span style='color:var(--mk-color-yellow)'>0 means the point is on the margin</span> ($y^{(i)}(w \cdot x^{(i)} + c) - 1 = 0$,*they are the support vectors*).

Therefore in **SVM**, our <span style='color:var(--mk-color-orange)'>objective</span> is to:
1) <span style='color:var(--mk-color-green)'>Maximise</span> the margin which is to maximise $\frac{2}{\vert\vert w \vert\vert}$ (*The numerator is a constant it can be any number*)
2) While also <span style='color:var(--mk-color-yellow)'>ensuring</span> that $y^{(i)}(w \cdot x^{(i)} + c) - 1 \ge 0$

There is a thing called **hard margin** which <span style='color:var(--mk-color-red)'>does not allow misclassification</span>, while a **soft margin**, <span style='color:var(--mk-color-green)'>allows some misclassification</span>.
## Lagrange Function

To maximise the margin we are <span style='color:var(--mk-color-yellow)'>essentially minimising</span> $\vert\vert w \vert\vert$, we can then **square it** to get rid of the square root and **multiply by half** ($\frac{1}{2}\vert\vert w \vert\vert^{2}$).

The <span style='color:var(--mk-color-teal)'>Lagrange function</span> is simply a function used to <span style='color:var(--mk-color-yellow)'>solve a objective with some constraint</span>, like what we have to maximise the margin.

**Outcome from manipulating the Lagrange function**
![[Lagrange Function Example.png|center]]

**Where:**
- $\alpha^{(i)}$ is call the **Lagrange multiplier**, which <span style='color:var(--mk-color-yellow)'>can be 0</span> but <span style='color:var(--mk-color-red)'>cannot be less than 0</span>
- $b$ is some **constant** for the <span style='color:var(--mk-color-yellow)'>decision boundary</span>

Therefore, essentially we want to <span style='color:var(--mk-color-yellow)'>maximise the function the end</span> which only depends on $\alpha$ (*Lagrange multiplier*).

Therefore, we have converted our primal optimisation problem to a dual optimisation problem.
## Non-linearly Separable Data

If our data is not linearly separable, then we can give it some <span style='color:var(--mk-color-turquoise)'>slack</span> (*Allow for some misclassification*). And create a <span style='color:var(--mk-color-turquoise)'>soft margin</span>.

Thus our boundary will now be:
1) $w \cdot x^{+} + b \ge 1 -  s$
2) $w \cdot x^{-} + b \ge -1 +  s$
**Where:**
- $s$ is the value of the slack

>For $s$ it <span style='color:var(--mk-color-yellow)'>has to be</span> $ge 0$.

Tuus now we will be <span style='color:var(--mk-color-orange)'>minimising</span> the sum of all slack variables as such:
$$
J(w,b) = \frac{1}{2}\vert\vert w \vert\Vert^{2} + c \sum_{i}max(0, 1 - y^{(i)}(w \cdot x^{(i)} + b))
$$
# Kernel Methods & Tricks
---
This trick is used when the <span style='color:var(--mk-color-yellow)'>data is truly not linearly-separable</span>. We define $\phi(X)$ as the <span style='color:var(--mk-color-teal)'>feature transformation function</span>. which essentially converts $x \rightarrow x^{2}$ or any other transformation which is suited for the data.

> [!example] Example of Feature Transformation
> ![[Feature Mapping Example.png|center|200]]
> 
> Initially there is <span style='color:var(--mk-color-red)'>no way that it can be lineary seperated</span> using just 1 feature $x_{1}$.
> 
> Then lets **condider transforming** the feature $\phi(x) = \{x, x^{2}\}^{T}$. Which results in a quardratic curve which we can draw a <span style='color:var(--mk-color-yellow)'>hyperplane to seperate the 2 classes</span>.
> 
> **Transformed Feature: ** $w_{0} + w_{1}x + w_{2}x^{2} \ge 0$

This function can map the <span style='color:var(--mk-color-yellow)'>data points in an infinite-dimension</span>.

So now in our <span style='color:var(--mk-color-teal)'>Lagrange function</span>, if we were to use feature transformation we will replace $x^{(i)}$ to $\phi(x^{(i)})$. and we can easily simplify the dot product in to $K(x^{(i)},x^{(j)}) = (x^{(i)} \cdot x^{(j)})^{d}$, this is known as the <span style='color:var(--mk-color-turquoise)'>kernel trick</span>.

The above equation is known as the <span style='color:var(--mk-color-teal)'>gaussian radical basis function kernal</span>:
$$
K(u, v) = e^{-\frac{\vert\vert u - v \vert\vert^{2}}{2 \sigma^{2}}} = \phi(u) \cdot \phi(v) 
$$

**Effect of the sigma value**
![[Gaussian RBF Kernel Effect of the Sigma Value.png|center]]


> [!info] Family of Kernels
> People sometimes came up with $K$ before knowing what the feature mapping $\phi$ is. In this case, $K$ is valid if it satisfies <span style='color:var(--mk-color-turquoise)'>Mercer’s theorem</span> (i.e., <span style='color:var(--mk-color-yellow)'>continuous, symmetric, positive semidefinite</span>).
> 
> **Other kernels:**
> • String kernel
> • Chi-squared kernel
> • tanh kernel
