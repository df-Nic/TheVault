---
title: Linear Regression
Date Created: 2024-09-08
Last Updated: 2025-09-28
tags:
  - DSA3361
  - AI/ML/LinearRegression
---
# What is Linear Regression
---
It is a data analytical model that is used to <span style='color:var(--mk-color-yellow)'>quantify a relationship</span> (*And predict*) between **1 or more predictor variables** (*X attributes*) with a <b><span style='color:var(--mk-color-yellow)'>continuous</span></b> <span style='color:var(--mk-color-yellow)'>response variable</span> (*Y output*).

There are <span style='color:var(--mk-color-orange)'>2 types</span> of **linear regression model**:
- **Simple** linear regression - When there is only <span style='color:var(--mk-color-yellow)'>1 predictor variable</span>
- **Multiple** linear regression - Where there are <span style='color:var(--mk-color-yellow)'>many predictor variables</span>

In **real life**, <span style='color:var(--mk-color-turquoise)'>linear regression</span> is used to check if there is any relationship between variables. However if the $Y$ **variable** is <span style='color:var(--mk-color-red)'>not continuous then this will not work</span>.

**Before building the model** ask these questions:
1) Is there a relationship (*Scatterplot*)
2) How strong is the relationship (*Corelation*)
3) Can I model this relationship (*Linear regression*)
4) How reliable is this model ($R^{2}$)
5) Can I predict using this model (*Predict*)
6) Is there synergy between predictors (*Interaction Term*)
# Data-Informed Decision Making Framework
---
In short it stands for <b><span style='color:var(--mk-color-turquoise)'>DIDM</span></b> and there are <span style='color:var(--mk-color-orange)'>6 steps</span> in this framework:
## Ask

The first step is to <span style='color:var(--mk-color-yellow)'>ask questions that they will like an answer</span> to **based on the output** from the linear regression.

A <span style='color:var(--mk-color-orange)'>baseline</span> for questions to ask can be:
1) **Is there an association**
2) **Strength of the association**
3) **Accuracy of using this to predict that**
## Acquire

After forming the questions, this step is to <span style='color:var(--mk-color-yellow)'>gather the relevant data</span> required to answer the questions.

This process also include **doing computation** to get relevant data if they <span style='color:var(--mk-color-yellow)'>do not exist in the original dataset</span>.

This data will then be used to **create the linear regression model** and then answer our questions formulated in the previous step.
## Analyse
### Data Cleaning

Before diving into building the model, it is good to <span style='color:var(--mk-color-yellow)'>know if the quality of data is good</span> (*Clean*).

This is where we **analyse the data** acquired, we can <span style='color:var(--mk-color-yellow)'>check for the following</span>:
- **Missing cells** (`sum(is.na(df)`)
- **Duplicate rows of data** (`sum(duplicated(df)`)
- **Outliers** (Plot the <span style='color:var(--mk-color-blue)'>box plots</span>)

We can also <span style='color:var(--mk-color-yellow)'>check the distribution</span> of the data, By using <span style='color:var(--mk-color-blue)'>histograms</span> and <span style='color:var(--mk-color-yellow)'>calculating skweness</span>.

> [!abstract] Interpriting Skewness Values
> We can calculate the skewness of a attribute using, `skewness(df$<Column Name>)`.
> 
> This will output a **value** and it can be <span style='color:var(--mk-color-orange)'>interprited</span> as such:
> 1) Between **-0.5 and 0.5**, the distribution is approximately <span style='color:var(--mk-color-yellow)'>symmetric</span>
> 2) Between **-0.5 and -1** or **0.5 and 1**, the distribution is <span style='color:var(--mk-color-yellow)'>moderately skewed</span>
> 3) Beyond **-1 or 1**, the distribution is <span style='color:var(--mk-color-yellow)'>highly skewed</span>

**Knowing about outliers** is important as it can <span style='color:var(--mk-color-red)'>alter data accuracy</span> and affect the mode. Thus <span style='color:var(--mk-color-yellow)'>omitting them</span> can be a way to **remove them**.
### Check the Corelation

Before we start the model building, **always check** that the 2 variables have a <b><mark style='background:var(--mk-color-yellow)'>linear relationship</mark></b>. It cannot be logarithmic or quadratic or anything else. This can be **easily observed** through a <span style='color:var(--mk-color-blue)'>scatter plot</span>.

The <span style='color:var(--mk-color-orange)'>2 variables</span> <b><mark style='background:var(--mk-color-yellow)'>must also be independent</mark></b> from each other.

> [!info] Corelation Function in R
> Another way is to use the corelation function in <span style='color:var(--mk-color-purple)'>R-studio</span>, `cor(df$<X Var Col>$, df$<Y Var col>$)`.
> 
> We want to <span style='color:var(--mk-color-yellow)'>get a value that is close to 1 or -1</span>, since this indicates a <span style='color:var(--mk-color-green)'>strong</span> positive / negative linear relationship.
> 
> Values <span style='color:var(--mk-color-red)'>close to 0 are weaker</span> (*No linear corelation*).
> 
> In general:
> 1) Between **-1 and -0.7** or **0.7 and 1**, the corelation is <span style='color:var(--mk-color-green)'>strong</span>
> 2) Between **-0.7 and -0.3** or **0.3 and 0.7**, the corelation is <span style='color:var(--mk-color-orange)'>moderate</span>
> 3) Between **-0.3 and -0.0** or **0 and 0.3**, the corelation is <span style='color:var(--mk-color-red)'>weak</span>
### Building the Linear Regression Model

The reason why we **check for linearity** is because the modeling of the graph can be as such: 
$$
Y = \beta_{1}X + \beta_{0}
$$
Which is simply the **standard formula for a straight line**. But in the context of linear regression models, $\beta$ are known as the <span style='color:var(--mk-color-turquoise)'>model coefficients</span> (*Parameters*).

$X$ is our predictor variable while $Y$ is our response variable.
#### Step 1 - Spilt the dataset

Usually the dataset will be **spilt into 70-30 or 80-20**, for the <span style='color:var(--mk-color-turquoise)'>training</span> and <span style='color:var(--mk-color-turquoise)'>testing</span> set.

The <span style='color:var(--mk-color-turquoise)'>training set</span> is to <span style='color:var(--mk-color-yellow)'>fit the parameters</span> of the model. while the <span style='color:var(--mk-color-turquoise)'>testing set</span> is to <span style='color:var(--mk-color-yellow)'>evaluate the performance</span>.

**Example:**
```R
# Spiltting the dataset
set.seed(10)
dt <- sort(sample(nrow(df.advert), nrow(df.advert ) * 0.8)) # 80 - 20
train <- df.advert[dt,] 
test <- df.advert[-dt,] # The - is to get the set difference of the dataset
```
#### Step 2 - Build the model

To make a **simple regression model**, do the following, `slr <- lm(<X Var> ~ <Y Var>, training_dataset)`.

To calculate the <span style='color:var(--mk-color-turquoise)'>residual</span> (*Error, which is, actual - predicted*), do the following command `redisuals <- resid(slr)`.

Now there are <span style='color:var(--mk-color-orange)'>2 assumptions</span> we need to **check** for:
- The <span style='color:var(--mk-color-turquoise)'>residuals</span> are <span style='color:var(--mk-color-yellow)'>normally distributed</span>
- The <span style='color:var(--mk-color-turquoise)'>residuals</span> are <span style='color:var(--mk-color-yellow)'>evenly scattered</span> and also they do <span style='color:var(--mk-color-yellow)'>not change with</span> the values of the <span style='color:var(--mk-color-yellow)'>predictor variable</span> (Also known as **Homoscedasticity**).

The **first** assumption can be checked with a <span style='color:var(--mk-color-blue)'>histogram</span> or with the `skewness` function. While the **second** assumption can be checked using a <span style='color:var(--mk-color-blue)'>scatter plot</span> or the `cor` function (*We want a value of 0 this time*).

If <b><mark style='background:var(--mk-color-green)'>these 2 assumptions hold</mark></b>, then we can proceed to **getting the coefficients**.

Be careful about <span style='color:var(--mk-color-red)'>overfitting</span> (*model captures noise from the dataset*), which is when the model cannot generalise real life scenarios as it will <span style='color:var(--mk-color-yellow)'>not perform well on unseen data</span>. This usually results in the **accuracy on training data significantly higher than testing data**.

> [!info] Size of the Dataset
> As a **rule of thumb** if we have $x$ number of variables we must have at least $100 \times x$ number of oservation.
> 
> This is because with many variables and very little data it can be <span style='color:var(--mk-color-red)'>difficult to capture the relationship</span> of the data between the variables.
#### Step 3 - Getting model coefficients

A way of getting the best coefficients is to use the <span style='color:var(--mk-color-blue)'>least squares method</span>. Which <span style='color:var(--mk-color-yellow)'>minimises the residual sum of squares</span> (**RSS**).
$$
\text{RSS} = \sum^{n}_{i = 1} (Y_{i} - \hat{Y}_{i})^{2}
$$
**Where:**
- $Y$ is the actual value
- $\hat{Y}$ is the predicted value

$$
\text{TSS} = \sum^{n}_{i = 1} (Y_{i} - \bar{Y})^{2}
$$
**Where:**
- $Y$ is the actual value
- $\bar{Y}$ is the **mean** of Y

**Total sum of squares**
>The <span style='color:var(--mk-color-yellow)'>variance of the variable Y</span> **before regression** (*Variability of Y before regression*)

**Residual sum of squares**
>The <span style='color:var(--mk-color-yellow)'>variability</span> of Y that is <span style='color:var(--mk-color-yellow)'>left unexplained</span> **after performing regression**

How <span style='color:var(--mk-color-orange)'>well does the model fit</span>? To do this we will calculate the $R^{2}$ value:
$$
R^{2} = 1 - \frac{\text{RSS}}{\text{TSS}}
$$
**Where:**
- RSS is the **residual sum of squares**
- TSS is the **total sum of squares**

This <span style='color:var(--mk-color-orange)'>value means</span> that the model can <span style='color:var(--mk-color-yellow)'>explain a said percentage of the variability</span> in Y. To **quickly** get this value in <span style='color:var(--mk-color-purple)'>R</span>, use the `summary` function.

Here there are <span style='color:var(--mk-color-orange)'>2 possibilities</span> for the $R^{2}$ values:
1) It is **near 0**, which means it the model <span style='color:var(--mk-color-red)'>does not explain the variability</span> in Y.
2) It is **near 1**, which means the model can <span style='color:var(--mk-color-green)'>perfectly explain all the variability</span> in Y. 

As a rule of thumb, for an <span style='color:var(--mk-color-green)'>acceptable</span> model, the $R^{2}$ value should be <b><mark style='background:var(--mk-color-green)'>0.7 or above</mark></b>.

>MSE is computed as $Variance + Bias^{2}$

Now <span style='color:var(--mk-color-orange)'>how significant is the model</span>? To do this we will carry out a hypothesis testing (*F-test/f-statistics*).

Here the $H_{0}$ and the $H_{1}$ will be as such:
- H0 : The model with <span style='color:var(--mk-color-yellow)'>no predictor</span> variable fits the data as good as the current regression model ($\beta_{0} = \beta_{1} = 0$).
- H1 : The <span style='color:var(--mk-color-yellow)'>current regression model fits the data better</span> than the model with no predictor variable ($\beta_{0} \neq \beta_{1} \neq 0$).

>Note that the f-test is to<span style='color:var(--mk-color-yellow)'> test the model as a whole</span> (*All the coefficients not just 1*). For testing **1 coefficient** use the <span style='color:var(--mk-color-yellow)'>t-test</span>, which can be done using the `summary` function

This is also shown in the `summary` function under p-value. If <span style='color:var(--mk-color-yellow)'>all of the values are less than 0.05</span> then **reject** the null hypothesis.

The values for $\beta_{1}$ and $\beta_{0}$ can be obtained from the `summary` function as well.

The <span style='color:var(--mk-color-turquoise)'>coefficient error</span> is defined as the **difference** between the **population model coefficients** and the **sample model coefficients**.

**Example:**
![[Summary Example of a Linear Regression Model.png|center]]

Here we can also **know which variables are significant** predictors:
- The <span style='color:var(--mk-color-green)'>lower</span> the **p-value** the better
- The <span style='color:var(--mk-color-green)'>higher</span> the **t-value** the better
#### Step 4 - Predict Using the Model

Since we have the model coefficients, the **linear equation can be formed**. Then all we need is the any $X$ value and it will give us an estimated $Y$ value.

However beware of <span style='color:var(--mk-color-red)'>extrapolation</span>, which is where we use an $X$ value which is <span style='color:var(--mk-color-yellow)'>out of the range of the dataset</span> for prediction.

This is because it can be misleading and we <span style='color:var(--mk-color-yellow)'>cannot assume that the same linear trend will hold</span> beyond the range of $X$ values in the training dataset.

But how can we be sure that the <span style='color:var(--mk-color-orange)'>prediction is accurate for the population</span>? This is where the [[Data Analysis#Confidence Intervals|confidence interval]] comes in. We can use `confint(model, level = 0.95)` to get the confidence interval.

Which will give us a range of possible values for $\beta_{0}$ and $\beta_{1}$ for the <b><span style='color:var(--mk-color-yellow)'>population regression model</span></b>.
##### Prediction Interval

It is the **range of values** on which a <span style='color:var(--mk-color-yellow)'>future individual observation would fall</span>.

**Example:**
![[Prediction & Confidence Interval.png|center|500]]

The **dashed lines** represents the <span style='color:var(--mk-color-turquoise)'>prediction interval</span> while the **grey area in the middle** is the <span style='color:var(--mk-color-turquoise)'>confidence interval</span>.

> [!info] Using Predictions to Calculate CI & PI
> When calculating <span style='color:var(--mk-color-blue)'>confidence intervals</span> using **prediction values**, `predict(model, data.frame(X Var = x), interval = "confidence")`.
> 
> This means that 95/100 samples, their true values (Y) will fall within this range.
> 
> When calculating <span style='color:var(--mk-color-blue)'>prediction intervals</span> using **prediction values**, `predict(model, data.frame(X Var = x), interval = "prediction")`.
> 
> This means that 95/100 predictions will fall within this range. And this range is ususally bigger than CI (*Single point*).
#### Step 5 - Evaluating the Regression Model

There are <span style='color:var(--mk-color-orange)'>4 ways to quantify</span> how **good** the model is:
1) **Mean squared error** (*MSE*) - `mse <- mean((actual-predicted )^2)`
2) **Mean absolute error** (*MAE*) - `mae <- mean(abs(actual - predicted))`
3) **Root mean square error** (*RMSE*) - `rmse <- sqrt(mse_data)`
4) **Mean absolute percentage error** (*MAPE*) - `mape <- mean(abs((actual - predicted)/actual))*100`

For the first 2 we would <span style='color:var(--mk-color-yellow)'>want a lower value</span> for both as it means the <span style='color:var(--mk-color-yellow)'>values do not differ</span> a lot and the model has a <span style='color:var(--mk-color-green)'>high predictive power</span>.

As for **RMSE**, the <span style='color:var(--mk-color-green)'>smaller the value the better</span>, as it **measures** the <span style='color:var(--mk-color-yellow)'>deviance of the predicted value from the best fit line</span> and thus, it will be closer to the actual values.

For **MAPE**, it **measures the simple average of the absolute percentage errors** and like before, the <span style='color:var(--mk-color-green)'>smaller the value the better</span> the mode.
## Apply

Based on the model, try and apply what was learnt to <span style='color:var(--mk-color-yellow)'>solve the question that was asked</span>, or <span style='color:var(--mk-color-yellow)'>make predictions</span> based on certain $X$ values.
## Announce

Let others know <span style='color:var(--mk-color-yellow)'>how well the model is and why they can rely on it</span>. Also announce what can be done to solve the questions asked.
## Assess

Try and <span style='color:var(--mk-color-yellow)'>explore further</span> into other possible $X$ variables than can affect the $Y$ variable. And **keep on updating the model** as as time passes it will be <span style='color:var(--mk-color-red)'>inaccurate or irrelevant</span>.
# Multiple Linear Regression Model
---
Everything mentioned above was for the <span style='color:var(--mk-color-blue)'>simple linear regression model</span>. Now with a <span style='color:var(--mk-color-blue)'>multiple linear regression model</span>, we will be <span style='color:var(--mk-color-yellow)'>using multiple</span> $X$ variables instead of only 1.

> [!abstract] Difference for Multiple LRM
> Now our linear equation will be:
> $$
> Y = \beta_{n}X_{n} + \dots + \beta_{2}X_{2} + \beta_{1}X_{1} + \beta_{0}
> $$
> 
> As for **assumptions**:
> - There must be <span style='color:var(--mk-color-red)'>no multicollinearity</span> between the predictor variables
> - **Redisuals** are <span style='color:var(--mk-color-yellow)'>normally distributed</span> instead of evenly scattered

The **DIDM** framework **still applies for this type of model** as well.

**Building a multiple linear regression model**
>Use the following code `mlrm <- lm(<Y variable> ~ <X var> + <X var> + ..., training_set`.
## Evaluating a MLRM Model

For this model the $R^{2}$ value <span style='color:var(--mk-color-red)'>cannot be used</span> because, with **more variables**, the $R^{2}$ value will <span style='color:var(--mk-color-yellow)'>just increase</span> but it can <span style='color:var(--mk-color-red)'>add more noise</span> (*Overfitting*). Therefore, we will use the <span style='color:var(--mk-color-yellow)'>adjusted</span> $R^{2}$ formula.
$$
\text{Adjusted } R^{2} = 1 - \frac{\text{RSS} / (n - d - 1)}{\text{TSS} / (n - 1)}
$$
**Where:**
- $n$ is the number of <span style='color:var(--mk-color-yellow)'>observations</span>
- $d$ is the number of <span style='color:var(--mk-color-yellow)'>variables</span>

Also we <span style='color:var(--mk-color-red)'>cannot plot</span> the graph onto the <span style='color:var(--mk-color-blue)'>scatterplot</span> since with every **additional variable**, the <span style='color:var(--mk-color-yellow)'>dimension will increase</span>.

We can also determine which [[#Step 3 - Getting model coefficients|variables are significant]], those that are <span style='color:var(--mk-color-yellow)'>insignificant can be dropped</span> and then build the model again.
## Potential Hurdles

### Multicollinearity

Happens when **two or more independent variables** in a regression model are <span style='color:var(--mk-color-yellow)'>highly correlated</span>. If used for <span style='color:var(--mk-color-yellow)'>prediction, it is not a problem</span>, but if present the <span style='color:var(--mk-color-red)'>model coefficients will be unstable</span> (*Hard to determine the effect of each variable*).

To determine <span style='color:var(--mk-color-turquoise)'>multicollinearity</span>, use the `cor` function on the $X$ variables only to **create** a <span style='color:var(--mk-color-turquoise)'>corelation matrix</span>. As a rule of thumb, any <b><span style='color:var(--mk-color-red)'>value above 0.7 means there is multicollinearity</span></b>. But **how bad is the severity**, we will use the <span style='color:var(--mk-color-turquoise)'>variance inflation factor</span>.

> [!abstract] Variance Inflation Factor
> **Variance Information Factor** (**VIF**)
> ><span style='color:var(--mk-color-yellow)'>Quantifies</span> the severity of multicollinearity in a regression analysis.
> 
> The <span style='color:var(--mk-color-orange)'>formula for VIF</span> is as follows:
> $$
> VIF_{i} = \frac{1}{1 - R^{2}_{i}}
> $$
> **Where:**
> - $R^{2}_{i}$ is the $R^{2}$ value of the regression model <span style='color:var(--mk-color-yellow)'>using all other variables except</span> $i$ ($i = \beta_{0} + \beta_{1}\text{Var 1} + ...$, excluding $Y$ and $i$ itself).
> 
> We can use the `vif` function from the <span style='color:var(--mk-color-purple)'>car R package</span> to get the value:
> - If the **value is 1** it means the <span style='color:var(--mk-color-green)'>variable is uncorrelated</span> to all other variables
> - If the **value is above 5** then there is <span style='color:var(--mk-color-red)'>high multicolinearity</span>

You can <span style='color:var(--mk-color-orange)'>plot the correlation matrix</span> as such:
```R
corrplot(cor(df.carprice), method = "number", type = "upper",
				 tl.col = "black", tl.srt = 30)
```

If **not delt** with it can <span style='color:var(--mk-color-red)'>cause some problems</span>:
1) Creates inaccurate estimates of the coefficients (*wrong sign*)
2) Provide false or non-significant p-values
3) Degrade the interpretability and the predictability of the model
#### Dealing with Multicollinearity

There a <span style='color:var(--mk-color-orange)'>2 ways</span> to **deal with multicollinearity**:
1) **Principle component analysis** (**PCA**) which <span style='color:var(--mk-color-yellow)'>combines highly corelated variables</span> into a unique principle component
2) **Omit** one of the multicollinearity predictor (*Choose which variable to study on or is more impactful*)
### Variable Selection

Aim to **include the right number of attributes**, adding too many will <span style='color:var(--mk-color-yellow)'>introduce irrelevant variables</span> which can <span style='color:var(--mk-color-red)'>affect model performance</span>.

> [!attention] Issues Arised from Variable Selection
> What happens when we **include irrelevant predictors**?
> - Adding irrelevant predictors will slightly increase the $R^{2}$ values as Y can be explained by the extra predictors.
> - The Adjusted $R^{2}$ values takes into account the number of predictors, may end up with a <span style='color:var(--mk-color-red)'>value that is lower</span> than a model without those irrelevant predictors.
> - <span style='color:var(--mk-color-red)'>Trouble finding the significance</span> of the regression model, carry out the F-test using `anova()`.
> 
> What happens when we **omit relevant predictors**?
> - Prediction will not be good as essential <span style='color:var(--mk-color-red)'>information will be missing</span> from the model.
> - $R^{2}$ and Adjusted $R^{2}$ value will <span style='color:var(--mk-color-red)'>not be optimal</span>.
> - Might not even get a significant F-test result for our regression model.

**Steps to choose variables**
1) **Select** a <span style='color:var(--mk-color-yellow)'>response variable Y</span>
2) **Select** the <span style='color:var(--mk-color-yellow)'>most important predictor X</span>, to determine or explain the response variable
3) **Select** the next most important predictor, <span style='color:var(--mk-color-yellow)'>based on the consideration that if the first most important predictor has been considered</span> (*Which one gives more information*)
4) Repeat steps 2 and 3 until **all crucial predictors have been included**

This is all **subjective**, but there are <span style='color:var(--mk-color-green)'>several advantages</span>:
- <span style='color:var(--mk-color-yellow)'>Control over the selection</span> if there are **2 equally good predictors**
- <span style='color:var(--mk-color-yellow)'>Gain further insights</span> from the data and have a deep understudying on why is it important

This can be done **automatically** as well in <span style='color:var(--mk-color-orange)'>2 ways</span>:
1) **Forward step-wise selection**: <span style='color:var(--mk-color-yellow)'>Begin</span> with a model that contains <span style='color:var(--mk-color-yellow)'>no predictor</span> and then start <span style='color:var(--mk-color-yellow)'>adding</span> the most significant predictor variables <span style='color:var(--mk-color-yellow)'>one by one</span> until a pre-determined stop rule is met.
2) **Backward step-wise selection**: Begin with a model that <span style='color:var(--mk-color-yellow)'>contains all the predictor variables</span> and then <span style='color:var(--mk-color-yellow)'>start removing</span> the non-significant predictor variables one at a time based on the highest p-value greater than 0.05. (*Might not guarantee the best model*)

>Note that **step-wise selection** <b><mark style='background:var(--mk-color-red)'>does not guarantee the best model is produced</mark></b>.
### Model Misspecification

Even if all the variables are selected perfectly, the model can still <span style='color:var(--mk-color-red)'>fail to represent the situation</span>.

This **happens** when:
- Non-linear relation
- Variability is unequal (*Homoscedasticity, unable to capture variability*)
- Outliers (`plot(model, which = 1` to **find outliers**)
#### Dealing with Outliers

Firstly <span style='color:var(--mk-color-red)'>not all outliers affect the model</span> only some greatly affects the model and these are called <span style='color:var(--mk-color-turquoise)'>influential points</span>.

**Cook's Distance**
><span style='color:var(--mk-color-yellow)'>Measures the influence</span> of an observation by quantifying how a **regression model changes when an observation is removed**, by taking into account both the <span style='color:var(--mk-color-yellow)'>leverage</span> and <span style='color:var(--mk-color-yellow)'>residual</span> of each observation.

General rule of thumb to identify these points (*influential points*):
- A Cook’s Distance of more than <span style='color:var(--mk-color-yellow)'>3 times the mean</span> (μ) of all cooks distance.
- Alternatively a Cook’s Distance of <span style='color:var(--mk-color-yellow)'>more than 4/n-(p + 1)</span>, where **n is the number of observations** and $p$ is the **number of predictors used in the model**
- Others suggests that Cook’s distance value of <span style='color:var(--mk-color-yellow)'>more 1 indicates an influential point</span>, and those **above 0.5** should be investigated.

We can <span style='color:var(--mk-color-orange)'>get the cooks distance</span> using the following command in <span style='color:var(--mk-color-purple)'>R</span>, `cooks.distance(model)`. It can **find the outliers in the X and Y space**.

If we **follow point 1** to find influential points, `influential <- cooksD[(cooksD > (3 * mean(cooksD , na.rm =TRUE)))]`.

**Leverage plot**
>A plot that **shows leverage of all residuals**. <span style='color:var(--mk-color-turquoise)'>Leverage</span> is the <span style='color:var(--mk-color-yellow)'>distance of a point to the center of all other points</span>.

A r**ule of thumb** is that a <span style='color:var(--mk-color-orange)'>point is influential</span> if the <span style='color:var(--mk-color-turquoise)'>leverage</span> is **above** $2(p+1) / 2$. But this only can <span style='color:var(--mk-color-yellow)'>find outliers in the X space</span>.

We can plot the leverage plot using the following command in <span style='color:var(--mk-color-purple)'>R</span>, `plot(model, which = 5)`.

**Example:**
![[Leverage Plot Example.png|center|500]]

Any <span style='color:var(--mk-color-yellow)'>observations in the red areas</span> are considered to be **influential points**.

If it is we can do the following:
- **Check if it an error**
- **Remove it and see if the model improves or not**
### Nonlinear Relationships & Unequal Variability

In such cases we can do the <span style='color:var(--mk-color-orange)'>following</span>:
1) **Transform** some/all the predictor variables using some <span style='color:var(--mk-color-yellow)'>logarithms</span> do deal with nonlinearity
2) **Introduce new variables** like an <span style='color:var(--mk-color-yellow)'>interaction term</span>
3) Use other models like <span style='color:var(--mk-color-blue)'>nonlinear regression</span>

#### Variable Transformation

For **nonlinear relation** between bivariate data (*2 variables*) we can use <span style='color:var(--mk-color-turquoise)'>logarithmic transformation</span>, to give us a <span style='color:var(--mk-color-yellow)'>log linear relationship</span>.

Yes **sometimes the best fit lines captures** the relationship of the data, but <span style='color:var(--mk-color-red)'>at some points it can be worse in predicting</span>.

**Example:**
![[Logarithmic Transformation Example.png|center|450]]

We will <span style='color:var(--mk-color-yellow)'>need to explore which variable to log</span> to give us a more linear relationship, as shown in the image above logging 9-month salary is better.

This works because $b^{y} = x \rightarrow y = \log_{b}x$, in general we will <span style='color:var(--mk-color-yellow)'>use the natural logarithm</span> (*Base $e$ default or the* `log(col, base = x)` function in <span style='color:var(--mk-color-purple)'>R</span>).

**List of transformation techniques**
![[List of Transformation Techniques.png|center]]

Since we **transformed the data using logarithms**, the equation <b><span style='color:var(--mk-color-yellow)'>will not follow the standard</span></b> $y = mx + c$, but:
$$
\log_{e}y= \beta_{1}x + \beta_{0} \rightarrow y = e^{\beta_{1}x + \beta_{0}}
$$
This is the **same** for multiple $X$ variables. And now $\beta$ is now a <span style='color:var(--mk-color-yellow)'>percentage increase for 1 unit</span> instead.
#### Dummy Variables

Also known as <span style='color:var(--mk-color-turquoise)'>indicator variables</span> can be used to <span style='color:var(--mk-color-yellow)'>handle categorical or non integer variables</span> by **assigning a unique value to some integer**.

**For example**: Male = 0, Female = 1

The **number of dummy variables** will be <span style='color:var(--mk-color-yellow)'>1 less than the number of categories</span>. But no worries as <span style='color:var(--mk-color-purple)'>R</span> will **auto generate** it in the `lm` function.

To change the variable focus do the following command , `credit$Gender <- relevel(credit$Gender, ref = "Female")`.
## Interaction Term

When **2 or more variables** are <span style='color:var(--mk-color-red)'>not independent</span> on one another, it can have a combined effect of affecting the prediction of the $Y$ variable.

Essentially, if the **sum of changes when 2 variables are changed one by one**, is <span style='color:var(--mk-color-yellow)'>different</span> then the change when **2 variables are changed simultaneously**, then <span style='color:var(--mk-color-yellow)'>there are dependencies</span>.

One common way of creating an <span style='color:var(--mk-color-turquoise)'>interaction term</span> is through **cross product**, which can be between
- **2 categorical variables**
- **1 categorical and 1 continuous variable**
- **2 continuous variables**

**Example:**
```R
# Do cross product on discipline and years since PHD
lm3 <- lm(log ( salary ) ~ rank + sex + discipline * yrs.since.phd, train)
summary (lm3)
```

If the **interaction term is significant**, when we <span style='color:var(--mk-color-yellow)'>cannot remove the 2 variables</span>.