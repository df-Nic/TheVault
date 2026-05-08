---
title: Logistic Regression
Date Created: 2024-09-23
Last Updated: 2025-09-28
tags:
  - CS2109S
  - AI/ML/LogisticRegression
---
# Classification
---
For a <span style='color:var(--mk-color-turquoise)'>logistic regression</span> its goal is to simply <span style='color:var(--mk-color-yellow)'>decide weather this data point belongs to which group</span> (*Classify*).

[[Introduction to Machine Learning & Decision Trees#Decision Tree|Decision trees]] are good in making decisions, however it <span style='color:var(--mk-color-orange)'>only works well in the following conditions</span>:
- We have **discrete** or **categorical** inputs
- **Not too many options** per variable

Thus given a **continuous variable** a <span style='color:var(--mk-color-red)'>decision tree might not work</span>.
## Dealing with Continuous Variables

Let $h(x)$ be our <span style='color:var(--mk-color-turquoise)'>hypothesis function</span> which tells us the category $x$ is in.

A simple way of dealing with continuous variables is to just <span style='color:var(--mk-color-yellow)'>bin the data into groups</span>:

**Example:**
$$
h(x) =
\begin{cases}
1,  & w_{1}x - w_{0} \gt 0 \\
0, & \text{Otherwise}
\end{cases}
$$
Essentially, if the value if $x  \gt w_{0} / w_{1}$ then it will be long to group 1 else it will be in group 0. This is known as the <span style='color:var(--mk-color-turquoise)'>step/threshold function</span>.

> [!fail] An Issue with a Step Function
> ![[Step Function Visualisation.png|center]]
> 
> Lets look at the example above, we can see that the function is <span style='color:var(--mk-color-yellow)'>discontinuous</span>, and therefore <span style='color:var(--mk-color-red)'>not differentiable</span>.
> 
> Which is a <b><span style='color:var(--mk-color-red)'>problem for gradient descent</span></b> to optimise the weights properly.
### Sigmoid Function

This function **solves the issue mentioned previously**. It essentially squishes a continuous variables into a <span style='color:var(--mk-color-yellow)'>range between 0 and 1</span> (*Probability*),  $h(x) = P(X = x)$.
$$
\sigma(x) = \frac{1}{1 + e^{-x}}
$$
Thus our $h(x) = \sigma(w_{0} + w_{1}x)$, essentially we will take the <span style='color:var(--mk-color-yellow)'>output from our linear function into the sigmoid function</span>.

This function <span style='color:var(--mk-color-yellow)'>works for any number of variables</span>.
## Performance Measures for Logistic Models

To evaluate a logistic regression model, we can use the [[Linear Regressions#Measuring Fit|mean square error]]. However, the sigmoid function makes the $y$ <span style='color:var(--mk-color-red)'>non convex</span> due to how the curve looks. Thus there can be a lot of local minima and we <span style='color:var(--mk-color-red)'>cannot find the global minimum</span>.
### Cross Entropy

A better way is to use <span style='color:var(--mk-color-turquoise)'>cross entropy</span>, which measures the **closeness between the probability distribution**.
$$
CE(y,\hat{y}) = \sum^{C}_{i = 1} - y_{i}\log{\hat{y}_{i}}
$$
**Where:**
- $C$ is the number of classes (*Groups*)
- $y$ is the true value
- $\hat{y}$ is the predicted value

There is also something called <span style='color:var(--mk-color-turquoise)'>binary cross entropy</span> which only <span style='color:var(--mk-color-yellow)'>works when there are 2 possible outcomes</span>.
$$
BCE(y,\hat{y}) = - y\log({\hat{y}}) - (1 - y)\log{(1 - \hat{y})}
$$
The **smaller the value** the <span style='color:var(--mk-color-green)'>closer it is to the true value</span>.

Therefore the <span style='color:var(--mk-color-orange)'>loss</span> is just the <span style='color:var(--mk-color-yellow)'>summation of cross entropy of all the points</span> just like in mean square error.
$$
J_{BCE} = \frac{1}{m}\sum^{m}_{i = 1} BCE(y_{i}, h_{w}(x_{i}))^{2}
$$
And cross entropy function is **convex**.
### Receiver Operator Characteristic

Then we can use [[Linear Regressions#Gradient Descent|gradient descent]], but instead we will <span style='color:var(--mk-color-yellow)'>use cross entropy instead</span> of MSE.

For this performance measure we will use the concepts of the [[Introduction to Machine Learning & Decision Trees#Classification Models|confusion matrix]].

There are <span style='color:var(--mk-color-orange)'>2 equations</span> which are going to be used:
1) **True positive rate**
$$
TPR = \frac{TP}{(TP + FN)}
$$
2) **False positive rate**
$$
FPR = \frac{FP}{FP + TN}
$$
As mentioned above, we say that anything above 0.5 belongs to this class, but this is not always the case, as we can <span style='color:var(--mk-color-yellow)'>defined our own threshold</span> ($\alpha$), which will **affect the values of the 2 equations** above.

Essentially we are trying to **plot a graph against the true positive and false positive rates** can <span style='color:var(--mk-color-yellow)'>calculating the area under this curve</span>.

**An ROC curve:**

![[Images/CS2109S Images/ROC Curve.png|center|250]]
So to plot this graph we essentially need to <span style='color:var(--mk-color-yellow)'>iterate through different points</span> of $\alpha$ and then **calculate** the **TPR** and **FPR** of the model and plot the points respectively.

> [!info] Reading the Curve
> By using **randomisation** we should expect to see a 50/50 spilt thus the <span style='color:var(--mk-color-yellow)'>area under the curve is 0.5</span>.
> - If our model is **above the 0.5 mark**, then is is <span style='color:var(--mk-color-green)'>better than random chance</span>.
> - If our model is **below 0.5** is <span style='color:var(--mk-color-red)'>worse than random chance</span>
> 
> It is possible for the model to have an **area of 1**, which mean it is a <b><span style='color:var(--mk-color-green)'>perfect model</span></b> (*Unlikely to happen*).
## Challenges of Logistic Regression

**Multi variable logistic regression**
> Same as linear regression, we can do **gradient descent** by <span style='color:var(--mk-color-yellow)'>partial differentiation on each of the variables</span>

**Dealing with non-linear decision boundary**
> In cases where the decision boundary is not linear (*Straight line*), then we can <span style='color:var(--mk-color-yellow)'>modify the hypothesis function</span> like by squaring or cubing the attributes.

![[Function Modification.png|center|300]]
# Multi-class Classification
---
What was mentioned above was for 2 classes but what about <span style='color:var(--mk-color-orange)'>3 or more</span>? 
## One vs All

One method is to do a <span style='color:var(--mk-color-yellow)'>one vs all</span> which <span style='color:var(--mk-color-yellow)'>focuses on one of the category</span> against the rest.

**Example:**
![[One Vs All Example.png|center|500]]

So if we have $C$ number of groups then we will <span style='color:var(--mk-color-yellow)'>make</span> $C$ <span style='color:var(--mk-color-yellow)'>different logistic regression models</span>. Afterwards we will **ask each model to classify this data point**.

The <span style='color:var(--mk-color-green)'>correct classification</span> is the model with the <span style='color:var(--mk-color-yellow)'>highest probability</span>.
## One vs One

Another method is to do a <span style='color:var(--mk-color-yellow)'>one vs one</span> which <span style='color:var(--mk-color-yellow)'>focuses on a pair of categories</span>.

![[One Vs One Example.png|center|500]]

First make <span style='color:var(--mk-color-yellow)'>all possible pairs of of groups</span> and then **make a model for each of the pairs**. Afterwards we will take the highest count based on the predictions of each pair.
# Model Evaluation & Selection
---
For any model we will generally use the **loss function** to <span style='color:var(--mk-color-yellow)'>compute the goodness of the model</span>. So can we compare the values against multiple models and pick the best model, well <span style='color:var(--mk-color-red)'>no</span>.

> [!question] Why can't we Take the Best One?
> Essentially by picking the **best model based on the loss function**, we are essentially showing a <span style='color:var(--mk-color-yellow)'>biasness</span>.
> 
> Since it can be possible that the best model is <span style='color:var(--mk-color-red)'>overfitted</span> and <span style='color:var(--mk-color-yellow)'>performs badly on unseen data</span>.

**Model evaluation**
![[Model Evaluation.png|center|400]]

A less biased method is to <span style='color:var(--mk-color-yellow)'>spilt the testing set to have a validation and a testing set</span>. Since the 2 datasets are independent (*Assuming the data is independent also*).

Then **based on the validation result**, we pick the best model and then we use it on our test data.

**Bias vs variance**
![[Bias Vs Variance.png|center]]

# Hyperparameter Tuning
---
This is the process of <span style='color:var(--mk-color-yellow)'>picking our parameters</span> (*Degree of polynomials, learning rate*) and training the model to see its performance.

**Some methods of hyperparameter tuning:**
- **Grid search** (exhaustive search)
	>Exhaustively try all possible hyperparameters
- **Random search**
	>Randomly select hyperparameters
- **Successive halving**
	>Use all possible hyperparameters but with reduced resources or successively increase the resources with smaller set of hyperparameters
- **Bayesian optimization**
	>Use Bayesian methods to estimate the optimization space of the hyperparameters
- **Evolutionary algorithms**
	>Use evolutionary algorithms (e.g., genetic algo) to select a population of hyperparameters