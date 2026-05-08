---
title: Regularisation Techniques
Date Created: 2024-10-27
Last Updated: 2025-09-28
tags:
  - DSA3361
  - AI/ML/LinearRegression
---
# Why Regularisation
---
There are <span style='color:var(--mk-color-red)'>2 problems</span> which can arise when building a model. One is [[Year 2/Sem 1/DSA3361 - Inferential Data Analytics/Linear Regression#Step 2 - Build the model|overfitting]] and the other is [[Year 2/Sem 1/DSA3361 - Inferential Data Analytics/Linear Regression#Multicollinearity|multicollinearity]].

And the **solution to this** is through <span style='color:var(--mk-color-turquoise)'>regularisation</span>. This technique **reduces the model complexity** by <span style='color:var(--mk-color-yellow)'>penalizing large coefficients</span> (*$w_{0}$ or the bias will not be regularised*).

There are <span style='color:var(--mk-color-orange)'>2 commonly used</span> regularisation techniques:
1) **Ridge regression** (*L2*), which solves multicollinearity by <span style='color:var(--mk-color-yellow)'>shrinking coefficients of the corelated predictors</span> to some small number and will <span style='color:var(--mk-color-yellow)'>fix the sign</span> of the coefficients.
2) **LASSO regression** (*L1*), which solves multicollinearity by **reducing coefficients** of some <span style='color:var(--mk-color-yellow)'>corelated predictors to exactly 0</span>.

> [!summary] Variable Selection
> LASSO or **L1** is also known as <span style='color:var(--mk-color-turquoise)'>variable selection</span>, since by definition, it **reduces variable coefficients to 0** meaning we can discard that variable.
> 
> This can help **simplify models** with <span style='color:var(--mk-color-yellow)'>high number of variables</span> and <span style='color:var(--mk-color-yellow)'>thus can help in overfitting</span>.
> 
> Variable selection is beneficial as it:
> 1) <span style='color:var(--mk-color-green)'>Prevent overfitting</span>
> 2) <span style='color:var(--mk-color-green)'>Improve</span> the <span style='color:var(--mk-color-green)'>model interpretability</span>
> 3) Make it <span style='color:var(--mk-color-green)'>easier to execute</span> the **business solution in practice**

Regularised models tend (*might*) to have a <span style='color:var(--mk-color-red)'>slightly higher error rate</span> on the **training dataset**, but in return, they have a <span style='color:var(--mk-color-green)'>lower error rate </span>on the **test dataset**.

> [!fail] Drop the Related Variable
> It is <span style='color:var(--mk-color-red)'>not always the case</span> where we can **just choose one of the 2** related variables and drop them.
> 
> Sometimes there can be multiple different related coefficients but it is **possible we might need to use 2 ot 3 of them**. Therefore we use regularisation.
> 
> Every predictor variable is recomended to have 100 observations, so 4 variables, 400 observations.
# Prediction Errors
---
## Types of Errors

There are <span style='color:var(--mk-color-orange)'>3 types of prediction errors</span>:
1) **Bias**
2) **Variance**
3) **Random error**

Between **bias and variance**, there is a inverse relationship, the <span style='color:var(--mk-color-yellow)'>lower the bias the higher the variance</span>. Therefore we aim to find the **appropriate level of complexity** for our model to <span style='color:var(--mk-color-yellow)'>strike a balance between the bias-variance tradeoff</span>.

![[Bias-Variance Tradeoff.png|center|350]]
### Bias
![[What is Bias.png|center|300]]

<span style='color:var(--mk-color-turquoise)'>Bias</span> is the <span style='color:var(--mk-color-yellow)'>difference</span> between the <span style='color:var(--mk-color-yellow)'>average prediction</span> of our model and the <span style='color:var(--mk-color-yellow)'>true target value</span>.

**High bias** means that the model <span style='color:var(--mk-color-red)'>cannot capture key information</span> of the training dataset or in other words the model may be <span style='color:var(--mk-color-turquoise)'>oversimplified</span> or <span style='color:var(--mk-color-turquoise)'>underfitted</span> (*high training and testing error*).
### Variance
![[What is Variance.png|center|300]]

<span style='color:var(--mk-color-turquoise)'>Variance</span> is the <span style='color:var(--mk-color-yellow)'>variability of a model prediction</span> for a given data point. Essentially if we repeat the model building process <span style='color:var(--mk-color-yellow)'>how much spread for the predictions of a datapoint</span>.

**High variance** means that it is <span style='color:var(--mk-color-red)'>very sensitive to input data</span>, a small **change in the input can have a drastic change in the output** (*unseen data*). This can be due to <span style='color:var(--mk-color-red)'>overfitting</span> (*learning the noise of the dataset*).
### Random Error

It is **error** that happens <span style='color:var(--mk-color-yellow)'>due to random chance</span>. This error is unavoidable as it **always exist**. 

Thus **we need to** **find the optimal model** that <span style='color:var(--mk-color-yellow)'>captures the actual relationships</span> while <span style='color:var(--mk-color-yellow)'>avoiding incorporating the random noise</span>.
## Cross Validation

In regularisation (*[[Year 2/Sem 1/CS2109S - Introduction to AI & Machine Learning/Support Vector Machines#Regularization|formula shown here]]*) there is a <span style='color:var(--mk-color-turquoise)'>regularisation parameter</span> usually denoted as $\lambda$ which controls the <span style='color:var(--mk-color-yellow)'>degree of regularisation</span> which in turn **determines how much the coefficients are adjusted**.

A **larger regularisation parameter value** leads to a <span style='color:var(--mk-color-yellow)'>model with smaller coefficients</span> (*in terms of their absolute values*) (*too small it leads to <i><span style='color:var(--mk-color-red)'>underfitting</span></i>*).

**Choosing the right value** can lead to a <span style='color:var(--mk-color-green)'>decrease in variance</span> and some <span style='color:var(--mk-color-red)'>affordable increase in bias</span> (*tradeoff*).

So how do we choose this, is by using <span style='color:var(--mk-color-turquoise)'>cross validation</span>, which is a <span style='color:var(--mk-color-yellow)'>estimation of the performance measure for models</span>.

There are a <span style='color:var(--mk-color-orange)'>many ways of cross validation</span> but we will **focus** on <span style='color:var(--mk-color-turquoise)'>K-fold cross validation</span>.
### K-fold

Remember that we **spilt the dataset into training and testing datasets**, <span style='color:var(--mk-color-turquoise)'>K-fold</span> has the same concept:
1) Spilt the data into $k$ <span style='color:var(--mk-color-yellow)'>equal sized folds</span>
2) Then essentially we will have $k$ rounds where at **each round** a <span style='color:var(--mk-color-yellow)'>unique fold will be used as testing</span> and the <span style='color:var(--mk-color-yellow)'>rest will be used for training</span>
3) Take the <span style='color:var(--mk-color-yellow)'>average of all the error rates</span> (*training error*) **based on the testing data** in all $k$ rounds (*a new model for each round*), this is known as <span style='color:var(--mk-color-turquoise)'>cross validation error rate</span>
4) The <span style='color:var(--mk-color-green)'>optimal model or coefficients</span> is the one that has the **lowest cross validation error rate**.

In summary every fold will be used as the testing set **exactly once**.

**This is what K-fold does visually** (*or other cross validation techniques*):
![[What does Cross Validation Do.png|center|300]]
# Ridge Regression
---
This is the **cost function** of <span style='color:var(--mk-color-orange)'>incorporating ridge regularisation</span> into our model:
$$
\sum_{i}(y_{i} - \hat{y_{1}})^{2} + \lambda \sum_{j = 1}^{n}\beta_{j}^{2} 
$$
**Where**:
- $\beta_{j}$ is the weight coefficient
- $\lambda \ge 0$ known as the <span style='color:var(--mk-color-turquoise)'>regularisation parameter</span>

When $\lambda$ is **close to 0**, it will be the<span style='color:var(--mk-color-yellow)'> same as not applying regularisation</span>, while **higher values** will <span style='color:var(--mk-color-yellow)'>make coefficients approach 0</span>. We **use it when** <span style='color:var(--mk-color-yellow)'>majority of the predictors are significant</span>.

The term $\lambda \sum_{j = 1}^{n}\beta_{j}^{2}$ is known as a <span style='color:var(--mk-color-turquoise)'>shrinkage penality</span>.

The <span style='color:var(--mk-color-orange)'>L2 norm</span> is defined as $\vert\vert \beta \vert \vert_{2} = \sqrt{\sum_{j = 1}^{n} \beta_{j}^{2}}$, this is just to measure the **distance of a vector from the origin**.

![[L2 Norm Graph.png|center|300]]

> [!summary] Advantages & Disadvantages of Ridge
> **Advantages**
> - Ridge regression models tend to have <span style='color:var(--mk-color-green)'>slightly better acccuracy</span>
> 
> **Disadvantages**
> - It **retrains all predictors** thus it <span style='color:var(--mk-color-red)'>cannot perform feature selection</span>
> - Models will have a relatively <span style='color:var(--mk-color-red)'>poorer interpretability</span>
# LASSO Regression
---
This is the **cost function** of <span style='color:var(--mk-color-orange)'>incorporating ridge regularisation</span> into our model:
$$
\sum_{i}(y_{i} - \hat{y_{1}})^{2} + \lambda \sum_{j = 1}^{n}\vert\beta_{j}\vert 
$$
**Where**:
- $\beta_{j}$ is the weight coefficient
- $\lambda \ge 0$

When $\lambda$ is **close to 0**, it will be the<span style='color:var(--mk-color-yellow)'> same as not applying regularisation</span>, while **higher values** will <span style='color:var(--mk-color-yellow)'>make coefficients approach 0</span> (*Only strongly corelated variables will have a coefficient, the rest will be 0*). We **use it when** <span style='color:var(--mk-color-yellow)'>a few of the predictors are significant</span>.

This is a benefit of using LASSO as it <span style='color:var(--mk-color-green)'>can perform variable selection</span> and on top of what it already solves, it <span style='color:var(--mk-color-green)'>improves the models interpretability</span> (*less variables simpler model*).

The <span style='color:var(--mk-color-orange)'>L1 norm</span> is defined as $\vert\vert \beta \vert \vert_{1} = \sum_{j = 1}^{n} \vert \beta_{j} \vert$, this is just to measure the **distance of a vector from the origin**.

![[L1 Norm Plot.png|center|300]]

> [!summary] Advantages & Disadvantages of LASSO
> **Advantages**
> - Ridge regression models tend to have <span style='color:var(--mk-color-green)'>slightly better interpretability</span>
> - Can <span style='color:var(--mk-color-green)'>perform feature selection</span>
> 
> **Disadvantages**
> - It may cause a <span style='color:var(--mk-color-red)'>loss of information</span> due to variable selection resulting in a <span style='color:var(--mk-color-red)'>relatively lower accuracy</span>.
# Elastic Net Regression
---
It is essentially a <span style='color:var(--mk-color-yellow)'>combination of ridge and LASSO</span>. The **cost function** looks like this:
$$
\sum_{i}(y_{i} - \hat{y_{1}})^{2} + \lambda \sum_{j = 1}^{n} ((1 - \alpha)\beta_{j}^{2} + \alpha\vert\beta_{j}\vert)
$$
**Where**:
- $\beta_{j}$ is the weight coefficient
- $\lambda \ge 0$
- $\alpha$ is known as the <span style='color:var(--mk-color-turquoise)'>mixing parameter</span>, $0 \le \alpha \le 1$

If $\alpha$ is **closer to 0**, it will <span style='color:var(--mk-color-orange)'>resemble more like a ridge regression model</span> while if its **closer to 1** its <span style='color:var(--mk-color-orange)'>closer to a LASSO regression model</span>.

If a <span style='color:var(--mk-color-yellow)'>balance between accuracy and interpretability</span> is required then **use elastic net regression**.
# Standardisation
---
It is a **pre-processing technique** for when <span style='color:var(--mk-color-yellow)'>variables are measured at different scales</span>. The formula is as follows:
$$
\hat{X} = X_{\text{standardised}} = \frac{X}{\sigma x_{i}}
$$
Essentially we will take every value in an attribute and divide it by the standard deviation of that variable. Note that we <span style='color:var(--mk-color-yellow)'>need to do this for the</span> $Y$ variable as well.

> [!question] Why Standardised?
> As mentioned previously regularisation will heavily penalise large coefficients. But **what about smaller ones**? Yes it will still get updated but at a slower rate.
> 
> Therefore standardisation helps in ensuring that the values are all at the same unit of measurement and <span style='color:var(--mk-color-yellow)'>prevnt significant predictors to have their coefficients reduced to near 0</span>.

The <span style='color:var(--mk-color-yellow)'>coefficients will also be standardised</span> ($\hat{\beta_{i}}$) and are known as <span style='color:var(--mk-color-turquoise)'>standardised coefficients</span>. It means that after increasing $x_{i}$ by **1 standard unit** (by $1 \times \sigma x_{i}$), it will change $\hat{y}$ by $\hat{\beta_{i}} \times \sigma_{}y$. Thus the <b><mark style='background:var(--mk-color-orange)'>standard deviation of standardised values is 1</mark></b>.

One benefit of standardisation is that we can **rank predictors based on the absolute value of the standardised coefficients**. The <span style='color:var(--mk-color-green)'>larger the value the more important the predictor</span> is.
0.96 + 1.6 0.7
We can also get $\hat{\beta_{i}}$ **from a non standardised model** and the formula is as follows:
$$
\hat{\beta_{i}} =
\begin{cases}
\beta_{i} \times \sigma_{x_{i}} / \sigma_{y} & \text{if $i$ } \neq 0 \\[2ex]
\beta_{0} / \sigma_{y} & \text{if $i$} = 0
\end{cases}
$$
# Building a Regularised Model
---
The function in <span style='color:var(--mk-color-purple)'>R</span> to <span style='color:var(--mk-color-orange)'>create a regression model</span> is as such:
```R
model <- glmnet(x, y, alpha = 0, lambda = L)
```
**Where:**
- `x` is the data matrix of variables (*use* `model.matrix()` in <span style='color:var(--mk-color-purple)'>R</span>)
- `alpha` is the mixing parameter between 0 and 1
	1) **0 is for ridge regression**
	2) **1 is for LASSO regression**
	3) **Strictly between 0 and 1 is for elastic net regression**
- `lambda` is the regularisation parameter which can be a constant value or a sequence of values. The <span style='color:var(--mk-color-orange)'>default</span> will be <span style='color:var(--mk-color-yellow)'>a sequence of values</span> by <span style='color:var(--mk-color-purple)'>R</span>.

**Take note that the above** is for a [[Year 2/Sem 1/DSA3361 - Inferential Data Analytics/Linear Regression|linear regression model]] and for a [[Year 2/Sem 1/DSA3361 - Inferential Data Analytics/Logistic Regression|logistic regression model]] change the `family` parameter to `"binomial"`.

> [!abstract] Assumptions
> 1) **Independence**: Each observation is independent from the others.
> 2) **Linearity**: The relationship, between the predictors Xs and the dependent variable Y, is linear.
> 3) **Constant Variance**: The residuals are evenly scattered around the center line of zero.
> 
> **Assumption for normality** (*normally distributed*) is <span style='color:var(--mk-color-red)'>not needed</span>.
> And we <span style='color:var(--mk-color-red)'>do not interpret</span> **p-value and confidence intervals** since it <span style='color:var(--mk-color-yellow)'>outputs biased estimates of the coefficients</span>.

>There is also something called <span style='color:var(--mk-color-turquoise)'>best subset selection</span> which tries all permutations of variables and report the best one $P \choose k$ for $k$ from 1 to $p$.
## Getting the Best Regularisation Parameter
---
We will use a function called `cv.glmnet()` which will <span style='color:var(--mk-color-green)'>get the best value</span> through **cross validation**.
```R
cv_ridge <- cv.glmnet(train.x, train.y, alpha = 0, type.measure = "mse")
```

Note that we can change `type.measure` to `mae` as well for mean absolute error. But by <span style='color:var(--mk-color-orange)'>default</span> it will be `mae`.

We can also change the `family` to **be a logistic regression** instead of a linear regression. And `alpha` is the **same meaning as above**.

Also by <span style='color:var(--mk-color-orange)'>default</span> `cv.glmnet` will have a **k-fold value of 10**, and to change it set the parameter `nfolds` to the number you want.

The above function will <span style='color:var(--mk-color-orange)'>provide 2 values</span>:
1) `lambda.min` - Which is the lambda value at which the <span style='color:var(--mk-color-green)'>lowest MSE is achieved</span>
2) `lambda.1se` - Which is the **largest lambda** at which it is within <span style='color:var(--mk-color-yellow)'>1 standard error of the smallest MSE</span>

>You can **choose** `1se` if you <span style='color:var(--mk-color-yellow)'>prefer interpretability</span> rather than accuracy.

There is also a `measure` column, which <span style='color:var(--mk-color-yellow)'>shows the loss function value specified</span>.

**Here is how the process looks like**:
![[Cross Validation Graph.png|center|500]]
**Where:**
- The<span style='color:var(--mk-color-red)'> red dots</span> are the <span style='color:var(--mk-color-yellow)'>mean cross validation error</span>
- The **error bar** represents the <span style='color:var(--mk-color-yellow)'>standard error of the MSE estimate</span>

To <span style='color:var(--mk-color-orange)'>make a prediction</span> do the following:
```R
new_data <- data.frame(X)
# If our model uses standardisation then we need to do the conversion
new_x <- data.matrix(new_data/scaler)
predict(model, new_x ) * scaler[i]
```
