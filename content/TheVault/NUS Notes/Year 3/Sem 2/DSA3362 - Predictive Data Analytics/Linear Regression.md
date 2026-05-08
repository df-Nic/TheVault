---
Title: Linear Regression
Date Created: 13-January-2026
Last Updated: 23-April-2026
Tags:
  - DSA3362
  - AI/ML/LinearRegression
---
# Simple Linear Regression (SLR)
---
Here simple means that our model will <b><span style='color: #FFD700'>only take in 1 input variable</span></b>. The goal is to find a <b><span style='color: #FFD700'>straight line that closely resembles the data points</span></b>.

Since it is a straight line the model will follow the following mathematical formula $y = mx + c$ to do its prediction. Thus the <b><span style='color: #FFD700'>y-intercept and the gradient are the models parameters</span></b>.

So we can model the data with the following:

$$
Y = \beta_{0} + \beta_{1}X_{1} + \epsilon
$$
Where:
- $\beta_{0}$ is the y-intercept
- $\beta_{1}$ is the gradient or slope
- $\epsilon$ denotes the observation error with zero mean
- $X_{1}$ is the input variable that is used

>[!important] $\epsilon$ is actually the residual or error
>The equation <b><span style='color: #FFD700'>above models the actual relationship</span></b> between the input and output variables.
>
>But when building the model it will only be $Y = \beta_{0} + \beta_{1}X_{1}$

Thus in SLR, $\beta_{0}$ and $\beta_{1}$ are <b><span style='color: #FFD700'>learnt and estimated</span></b> by the model.

>[!note] To get the best model we use the ordinary least squares criterion (OLS)
>It essentially uses the [[Year 3/Sem 2/DSA3362 - Predictive Data Analytics/Supervised Learning.md#For Regression Models|residual sum of squares (RSS)]] and it tries to <b><span style='color: #98FB98'>minimise</span></b> it.

The best fitting line <b><span style='color: #FFD700'>passes through the average point coordinate</span></b>, meaning that the line will pass through the average of the input variable values ($\bar{x}$) and the output variable values ($\bar{y}$). 

So we can **compute the intercept after finding** $\beta_{1}$ using the following formula:
$$
Y = \bar{y} + \beta_{1} (X_{1} - \bar{x}) \rightarrow \beta_{0} = \bar{y} - \beta_{1}(\bar{x})
$$
>[!danger] It is possible that this best fit line might not truly represent the underlying relationship
>This is known as <b><span style='color: #87CEEB'>model misspecification</span></b>.
>
>For instance it is possible that the relationship is a quadratic one, thus our model should look something like $Y = \beta_{0} + \beta_{1}X_{1} + \beta_{1}X_{1}^{2}$. However take note that the <b><span style='color: var(--mk-color-red)'>quadratic model overfits easily</span></b>.
# Multiple Linear Regression (MLR)
---
In multiple linear regression models, it is a generalisation of a simple linear regression model with <b><span style='color: #FFD700'>2 or more input variables</span></b>.

$$
Y = \beta_{0} + \beta_{1}X_{1}  + \beta_{2}X_{2} + \dots + \beta_{p}X_{p}  + \epsilon
$$
So given $n$ rows of data we essentially have $n$ [[Year 1/Sem 2/MA1522 - Linear Algebra for Computing/Linear Systems.md|linear equations to solve]]. Thus we can represent all this in a matrix form:
$$
  Y = 
  \begin{pmatrix}
    y_{1} \\ 
    y_{2} \\
    \vdots \\
    y_{n}
   \end{pmatrix}
   
   \beta = 
  \begin{pmatrix}
    \beta_{0} \\ 
    \beta_{1} \\
    \vdots \\
    \beta_{p}
   \end{pmatrix}
   
   \epsilon = 
  \begin{pmatrix}
    \epsilon_{1} \\ 
    \epsilon_{2} \\
    \vdots \\
    \epsilon_{n}
   \end{pmatrix}
$$
$$
  X = 
  \begin{pmatrix}
    1 & x_{11} & \dots & a_{1n} \\ 
    1 & x_{21} & \dots & a_{2n} \\
    \vdots & \vdots &  \dots      & \vdots \\
    1 & x_{n1} & \dots & a_{np}  
   \end{pmatrix}
$$
Then our model will be essentially:
$$
Y = X\beta + \epsilon
$$
>[!info] $X$ is called the design matrix
>The first column is all 1s & this is for the Y intercept.

>[!success] Similarly we want to minimise the residual sum of squares for a better model
>The <b><span style='color: #98FB98'>best coefficients is unique</span></b> and it can be expressed as the following:
>$$
>\hat{\beta} = (X^{T}X)^{-1}X^{T}Y
>$$

>[!warning] When handling multiple input variables, there can be multicollinearity
>It happens when <b><span style='color: #FFD700'>2 or more input variables are correlated with one another</span></b>.
>
>It <b><span style='color: var(--mk-color-red)'>indicates redundancy which affects precision, coefficients & interpretability</span></b> of the model.
>
>To solve this we can <b><span style='color: #98FB98'>pick a subset of input variables</span></b> to reduce multicollinearity. Or we can compute the [[R Basics#Handling Multicollinearity|variance inflation factors]] which tells us <b><span style='color: #FFD700'>how well the variable is explained by all other input variables</span></b>.

# Linear Regression In R
---
## Building A Linear Regression Model

To **build a simple linear regression model** in R we can use the `lm(formula, data)` function. The 2 arguments:
1) **Formula** is written as such `Y_col ~ x_col_1`
2) **Data** which can be either a data frame, list or an environment

**Specify which columns to use**:
```R
lrm <- lm(formula = y_col ~ x_col1 + x_col2, data = df)
```

**Use all columns** (*multiple linear regression model*):
```R
lrm <- lm(formula = y_col ~ ., data = df)
```

Once trained the model will have its **fitted values** (*predicted values on the training data*) we can access this using `model$fitted.values`.

>[!note] You need to import the `caret` library

An alternative way is to use the `train(form, data, method, trControl)` function:
```R
lrm <- train(form = y_col ~ ., data = df, method = "lm", trControl = trainControl(method = 'cv', number = 4))
```

Here `trControl` is for cross validation. And afterwards we can **get the coefficients** using `summary (lm4 ) $coefficients [ ,1]`
### Making a Prediction

To **make a prediction** with a model we can use the `predict(object, newdata, interval)` function. The 3 arguments:
1) **Object** is the fitted model
2) **New data** Is a data frame with new data
3) **Interval** (*optional*), we can set this to be `prediction` which will return a 95% confidence interval along with the predicted value

```R
predict(fitted_model, data.frame (x_col = 100), interval = "prediction")
```

