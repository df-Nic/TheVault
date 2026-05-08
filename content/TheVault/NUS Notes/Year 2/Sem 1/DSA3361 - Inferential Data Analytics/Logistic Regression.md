---
Date Created: 2024-09-25
Last Updated: 2025-09-28
tags:
  - DSA3361
  - AI/ML/LogisticRegression
Title: Logistic Regression
---
# Classification Problems
---
In [[Year 2/Sem 1/DSA3361 - Inferential Data Analytics/Linear Regression|linear regression]] we are interested when the **response variable is continuous**, now we are interested when it is not continuous but <span style='color:var(--mk-color-yellow)'>categorical</span>.

The $y$ <b><span style='color:var(--mk-color-yellow)'>must be contained</span></b> **between 0 and 1**.

There are <span style='color:var(--mk-color-orange)'>2 types of categories</span>:
1) **Binary** -<span style='color:var(--mk-color-yellow)'> Only 2</span> categories
2) **Multinomial** - <span style='color:var(--mk-color-yellow)'>More than 2</span> classes or categories

> [!info] Categorical Data in R
> Categorical data type in <span style='color:var(--mk-color-purple)'>R</span> is known as factors. We can use the tidyverse function `mutate` to <span style='color:var(--mk-color-yellow)'>convert variables into factors</span>.
> 
> **Example**: `mutate(default = as.factor(default))`
> 
> Note that being a **factor it will do a key value pairing** of the values, but <b><span style='color:var(--mk-color-red)'>not actually convert them into integers</span></b>.
> 
> We can use the `as.numeric()` function to convert into an integer.

In order to **make a logistic model**, we need to match the categorial variables into a integer.

For **binary category** - `mutate(<Var name> = ifelse(<variable> == <Value>, 1, 0))`.
# Exploratory Data Analysis
---
Unlike in linear regression, the **variables are not continuous** and sometimes are <span style='color:var(--mk-color-red)'>not even in integers</span>.

To prevent [[Year 2/Sem 1/DSA3361 - Inferential Data Analytics/Linear Regression#Multicollinearity|multicollinearity]] here are some <span style='color:var(--mk-color-orange)'>ways to check</span>:
1) **Plot a box plot**

![[Box Plot To Determine Categorical Significance.png|center|400]]

We want the <span style='color:var(--mk-color-yellow)'>box plot to have a significant difference</span>. For this example we can see that between defaulters and non defaulters the **distribution is similar** thus it is <span style='color:var(--mk-color-red)'>not significant</span>.

2) **Convert each value into a integer**

As [[#Classification Problems|mentioned previously]] we can use the `mutate()` function to convert the categorical variables into a numeric form.

We can then use the `cor` function to generate a [[Year 2/Sem 1/DSA3361 - Inferential Data Analytics/Linear Regression#Check the Corelation|corelation matrix]]. And plot it as such, `corrplot(corr = correlation, method = 'number', type = 'upper')`.

3) **Stacked bar plot**

What if we want to <span style='color:var(--mk-color-yellow)'>compare 2 categorical variables</span> and their significance. One way is to use a **stack bar plot** which can tell us <span style='color:var(--mk-color-yellow)'>which categories are significant</span>.

**Example:**
![[Stack Bar Plot to Determine Significance.png|center|400]]

Here we can tell that students have a higher rate of defaulting, which can be a good predictor.

> [!question] Other Ways Besides Plotting
> Since both are categorical we can also use the <b><span style='color:var(--mk-color-blue)'>chi-squared test</span></b> to determine significance.
> 
> **Example**: `chisq.test(df$<var>, df$<var>)`
> 
> As long as the p-value is **below 0.05** <span style='color:var(--mk-color-green)'>it is significant</span>.
# Logistic Regression Model
---
The logistic model <span style='color:var(--mk-color-yellow)'>fits the predictions between values 0 and 1</span>. This is just the **probability**. And the [[Year 2/Sem 1/CS2109S - Introduction to AI & Machine Learning/Logistic Regression#Sigmoid Function|probability function]] is given as such:
$$
P(X) = \frac{e^{\beta_{0} + \beta_{1}x}}{1 + e^{\beta_{0} + \beta_{1}x}}
$$
>This only <b><mark style='background:var(--mk-color-yellow)'>applies to binary classification models</mark></b>

This will yield a "**S-shaped**" curve and this function is called the [[Year 2/Sem 1/CS2109S - Introduction to AI & Machine Learning/Logistic Regression#Sigmoid Function|sigmoid function]].

This is a form of <span style='color:var(--mk-color-turquoise)'>soft classification</span> since it **returns a probability** and it will <span style='color:var(--mk-color-yellow)'>need a human to define a threshold</span> to make it into a <span style='color:var(--mk-color-turquoise)'>hard classification</span>,
## Odds

It is a description of <span style='color:var(--mk-color-yellow)'>how rare the event is to occur</span>.

By rearrange the formula above we can get the <span style='color:var(--mk-color-orange)'>odds of a particular event occurring</span>:
$$
\frac{P(X)}{1 - P(X)} = e^{\beta_{0} + \beta_{1}x}
$$
**Where:**
- $P(X) / 1 - P(X)$ represents the <span style='color:var(--mk-color-turquoise)'>odds</span>.

This will yield a **logistic curve**. And the range of odds can be from 1 to $\infty$.

>Here an **increase in 1 unit** of $X$ will <b><mark style='background:var(--mk-color-yellow)'>multiply the odds</mark></b> by $e^{\beta_{1}}$.
### Log Odds

We can also turn the **log equation into a linear one** by taking the $ln$ on both sides, this is known as <span style='color:var(--mk-color-turquoise)'>logit</span> (*This is what <span style='color:var(--mk-color-purple)'>R</span> tells us*).
$$
\ln\left({\frac{P(X)}{1 - P(X)}}\right) = \beta_{0} + \beta_{1}x
$$
>Here an **increase in 1 unit** of $X$ will <b><mark style='background:var(--mk-color-yellow)'>increase the log odds</mark></b> by $\beta_{1}$.

If $\beta_{1}$ is **positive**, then increasing $X$, will associate with increasing $P(X)$ but we <mark style='background:var(--mk-color-red)'>will not know how much</mark>.
## Finding the Best Fit Curve

We need to **iterate all possible** $\beta$ **values** to find the best fit curve and to do this we will use a <span style='color:var(--mk-color-turquoise)'>maximum likelihood estimation</span> (*MLE*) method.
$$
L(\beta_{0}, \beta_{1}) = \prod P(X)
$$
>If we want to **calculate the probability of failure** use $1 - P(X)$ instead

We will <span style='color:var(--mk-color-green)'>want to maximise this value</span> the value In <span style='color:var(--mk-color-purple)'>R</span>, the `glm()` function is used to get the maximum.

> [!tldr] Using More Variables
> Evenything mentioned so far is using **only 1 predictor vvariable**.
> 
> To add more variables is the same as in the [[Year 2/Sem 1/DSA3361 - Inferential Data Analytics/Linear Regression#Multiple Linear Regression Model|linear regression model]].
> 
> And for the likelyhood function we will want to find the best $\beta_{1}, \dots, \beta_{n}$ that maximises the value.
## Fitting a Logistic Regression Model

To **fit a logistic regression model** we can use the `glm()` function as such:
```R
model1 <- glm(<Response> ~ <Predictor Variables>,
			data = train,
			family = binomial)
model1
```

>Important to <b><mark style='background:var(--mk-color-yellow)'>set the family to binomial</mark></b> for a logistic regression model.

To evaluate the model we will want to <span style='color:var(--mk-color-yellow)'>have a variance/bias tradeoff</span>:
- A **simple model** (*Low variance*)
- **Best fit** model (*Low Bias*)

To predict with a logistic model, we can use the following <span style='color:var(--mk-color-purple)'>R</span> code, `pred <- predict(<model>, newdata = data.frame(<values>), type = "response")`.
### Deviance

Deviance is the same as how [[Year 2/Sem 1/DSA3361 - Inferential Data Analytics/Linear Regression#Multiple Linear Regression Model|SSE in linear regression]] where we want a <span style='color:var(--mk-color-green)'>smaller deviance for a better model fit</span>.

There are<span style='color:var(--mk-color-orange)'> 2 types of deviances</span>:
1) **Null deviance** ($D^{2}_{o}$) - Is the <span style='color:var(--mk-color-yellow)'>deviance of the null model</span>. A null model has no predictor variables but only the intercept term. It is analogous to the SST (*sum of squares total*) in multiple regression.
2) **Residual deviance** ($D^{2}$) is the **deviance of a given model**, which is the <span style='color:var(--mk-color-yellow)'>sum of all deviance</span> $d_{i}$

The<span style='color:var(--mk-color-orange)'> residual deviance has a formula</span> as well **for 1 row**:
$$
d_{i} = sign(y_{i} - \hat{y_{i}}) \sqrt{-2(y_{i} \times \ln{\hat{y_{i}}}) + (1 - y_{i})\ln{1 - \hat{y_{i}}}}
$$
**Where:**
- $sign(x)$, is a function where if $x \gt 0$ then output 1, $x \lt 0$ output -1, $x = 0$ output 0.

With this we can do **something similar to the f-test** which is called the <span style='color:var(--mk-color-turquoise)'>overall significance test</span>. Where $H_{o}$ can be <span style='color:var(--mk-color-red)'>rejected</span> at $\alpha$ if $D^{2}_{o} - D^{2} \lt X^{2}_{p, \alpha}$.

The RHS value can be computed as such `qchisq(p = 0.05, df = 3, lower.tail = FALSE)`. Where `df` can be retrieved from the `summary` function.
### Akaike Information Criterion

One way to compute the goodness of our model is using the <span style='color:var(--mk-color-turquoise)'>akaike information criterion</span> or (*AIC*).
>The **AIC**, <span style='color:var(--mk-color-yellow)'>judges the models fitted values</span> with the true values while also <span style='color:var(--mk-color-yellow)'>penalising complex models</span>.

The <span style='color:var(--mk-color-orange)'>formula</span> for **AIC** is as such:
$$
\text{AIC} = -2 \text{loglik}(\hat{\beta}) + 2k
$$
**Where:**
- $k$ is the number of parameters used
- $\hat{\beta}$ is the coefficient estimates of the model ($\beta_{0}$, $\beta_{1}$, etc)
- $loglik$ is the <span style='color:var(--mk-color-turquoise)'>maximum log likelihood</span> of the model

AIC is given in the `summary` of the model or you **can use the function** `AIC(model)`. The <span style='color:var(--mk-color-green)'>lower the AIC the better the model</span>, which we will then select.

AIC is **only used for logistic regression models only**.

We can use something called a <span style='color:var(--mk-color-turquoise)'>step AIC</span> which essentially just <span style='color:var(--mk-color-yellow)'>iterates through all possible permutation of the x-variables</span> and calculate the **AIC** and <span style='color:var(--mk-color-green)'>gives the best possible model based on AIC</span>.

**Do step AIC in R**:
```R
# Start with a null model
fit.glm <- glm(default ~ 1, data = df, family = "binomial")

(bestfit <- stepAIC(fit.glm,
	scope = list(upper = ~ student * balance * incom, lower = ~1)))
# Replace with the attributes in the dataset
```
## Outliers using Deviance

To define outliers, we can use the <span style='color:var(--mk-color-turquoise)'>deviance residual</span>. As long as this interval ($d_{i}$) is <span style='color:var(--mk-color-red)'>above 3 then it is an outlier
</span>.

**How to calculate deviance residual**
```R
df.deviance <- df %>% mutate(default.prob = fit.glm3$fitted.values,
	deviance.residual = summary(fit.glm3)$deviance.resid,
	resid = residuals(fit.glm3, type = "deviance")
)

head(df.deviance)
```
# Evaluation Matrices
---
When making **predictions using logistic regressions** there are <span style='color:var(--mk-color-orange)'>2 possible errors</span> than can occur:
1) **Type 1 error** - False positives
2) **Type 2 error** - False negatives

We will define <span style='color:var(--mk-color-green)'>positive</span> as **something of interest** that we want to observe, and <span style='color:var(--mk-color-red)'>negative</span> to be **a usual event**.
## Confusion Matrix

A <span style='color:var(--mk-color-turquoise)'>confusion matrix</span> can help **visualise the predictions** made by the model.

![[Images/CS2109S Images/Confusion Matrix.png|center]]

To <span style='color:var(--mk-color-orange)'>generate a confusion matrix</span> in <span style='color:var(--mk-color-purple)'>R</span> we can do the following:

```R
df$true_value <- factor(df$true_value, levels = c("Yes", "No"))
df$y_pred <- factor(df$y_pred, levels = c("Yes", "No"))

coefficient_matrix <- table(df$true_value, df$y_pred, deparse.level = 0)

colnames(coefficient_matrix) <- c("y_pred = Yes", "y_pred = No")
rownames(coefficient_matrix) <- c("true_value = Yes", "true_value = No")

TP <- coefficient_matrix[1,1]
TN <- coefficient_matrix[2,2]
FP <- coefficient_matrix[2,1]
FN <- coefficient_matrix[1,2]
```

**Accuracy or classcification rate**:
>How <span style='color:var(--mk-color-yellow)'>often is the model correct</span> (*Overall accuracy*). But this <span style='color:var(--mk-color-red)'>does not show how well the model does in each category</span>

**Precision** or **Positive predicted value**
> When the **model predicts positive** <span style='color:var(--mk-color-yellow)'>how often is it correct</span>. The <span style='color:var(--mk-color-green)'>higher the precision the better the model</span>.

**Recall** or **Sensitivity** or **True positive rate**
>When the **actual outcome is positive** <span style='color:var(--mk-color-yellow)'>how often does the model predict is as positive</span>. In general <span style='color:var(--mk-color-green)'>higher sensitivity is better</span>.

**Specificity** or **True negative rate**
> When the **actual outcome is negative** <span style='color:var(--mk-color-yellow)'>how often does the model predict is as negative</span>. In general <span style='color:var(--mk-color-green)'>higher sensitivity is better</span>.

$$
\text{Specificity} = \frac{TN}{TN + FP}
$$
**F1 Score**
>**Combines** both <span style='color:var(--mk-color-yellow)'>sensitivity</span> and <span style='color:var(--mk-color-yellow)'>precision</span>. The <span style='color:var(--mk-color-green)'>higher the F1 score the better</span>. Is the <span style='color:var(--mk-color-yellow)'>harmonic mean</span> of both recall and precision.

There is also a <span style='color:var(--mk-color-turquoise)'>false positive rate</span> (1 - Specificity) and <span style='color:var(--mk-color-turquoise)'>false negative rate</span> which is just <span style='color:var(--mk-color-yellow)'>1 minus the respective value</span>.

**Yuden matric**
><span style='color:var(--mk-color-green)'>Maximise</span> sensitivity + specificity

To **get a value from the confusion matrix** use the following code, `confusion_matrix[row, col]`.

> [!important] Confusion Matrix Tradeoff
> In logstic regression <span style='color:var(--mk-color-yellow)'>we will set a cut off</span> (*threshold*) for a prediciton to be positive or negative.
> 
> This in turn will also <span style='color:var(--mk-color-yellow)'>affect the values inside the confusion matrix</span>. Thus at different $\alpha$, the <span style='color:var(--mk-color-red)'>values will differ leading to a biased conclusion</span>.
> 
> In general if the **threshold is lowered**, <b><mark style='background:var(--mk-color-yellow)'>specificity reduces and sensitivity increases</mark></b>.
## Receiver operating characteristic Curve

ROC is a curve that shows the <span style='color:var(--mk-color-yellow)'>relationship between sensitivity and specificity</span> of a logistic model.

The x-axis is the **false positive rate** and the y-axis is the **sensitivity** of the model.

![[Images/CS2109S Images/ROC Curve.png|center|300]]

Essentially we are **plotting a curve based on the different** $\alpha$ (*Thresholds*) and then <span style='color:var(--mk-color-yellow)'>calculating the area under the curve</span> (*AUC*).

There is also a <span style='color:var(--mk-color-turquoise)'>reference point</span> as shown as a **dotted line**. This is known as a <span style='color:var(--mk-color-yellow)'>random classifier or random chance</span>!  Our goal is to make a model such that the <span style='color:var(--mk-color-green)'>area under the curve is greater than random chance</span> ($\gt 0.5$).

A **perfect model** will <span style='color:var(--mk-color-yellow)'>hug the top left</span> hand corner of the graph with a AUC of 1.

**Potting ROC curve**
```R
library(pROC) # for plotting ROC curve

# Generate predictions for threshold = 0.2, 0.5 and 0.8
pp <- pp %>% mutate(y_pred_low = ifelse(y_prob > 0.2, "Yes", "No"))
pp <- pp %>% mutate(y_pred = ifelse(y_prob > 0.5, "Yes", "No"))
pp <- pp %>% mutate(y_pred_high = ifelse(y_prob > 0.8, "Yes", "No"))

idx <- order(-pp$y_prob)

sensitivity <- cumsum(pp$default[idx] == "Yes") / sum(pp$default == "Yes")

specificity <-(sum(pp$default == "No") - cumsum(pp$default[idx] == "No")) / sum(pp$default == "No")

roc_df <- data.frame(sensitivity = sensitivity, specificity = specificity)

# ROC plot 
ggplot(roc_df, aes(x = 1 - specificity, y = sensitivity)) +
	geom_line(color = "blue") +
	scale_x_continuous(expand = c(0, 0)) +
	scale_y_continuous(expand = c(0, 0)) +
	geom_line(
		data = data.frame(x = (0:100) / 100),
		aes(x = x, y = x),
		linetype = "dotted",
		color = "red") +
	labs(x = "False Positive Rate = 1-Specificity", y = "Sensitivity") +
	theme_light()

# AUC value
auc <- sum(roc_df$sensitivity[-1] * diff(1 - roc_df$specificity))
```

To get the <span style='color:var(--mk-color-green)'>best threshold</span> for our classification model we can do the following.
```R
y_true <- train$default
y_probs <- predict(model2, newdata = train, type = "response")
plot.roc(
	y_true,
	y_probs,
	print.auc = TRUE,
	thresholds = "best",
	print.thres = "best"
)
```

A good gauge of how well the model is, if out of the 6 evaluation matrixes there is as long as <span style='color:var(--mk-color-yellow)'>4 of them are above 0.8</span>, then our model is good.

We can also **compare these values** to <span style='color:var(--mk-color-yellow)'>check if there is overfitting</span> by doing the same thing but on the test data set and compare their values.
# Multinominal Logistic Regression
---
Unlike binary logistic regression, now there are <span style='color:var(--mk-color-yellow)'>more than 2 categories</span>. Another word for this is <span style='color:var(--mk-color-turquoise)'>polytomous</span>.

First lets assume that we have $n$ number of categories. To build a <span style='color:var(--mk-color-turquoise)'>multinominal logistic regression</span>, we can <span style='color:var(--mk-color-yellow)'>choose 1 class as our base line</span> lets call this $c$.

Then for <span style='color:var(--mk-color-yellow)'>every other category</span> $k$, where $k \neq c$, we will **build a logistic regression mode**l. This follows the one versus all method.

Thus we will end up with $n - 1$ models and with $x + 1$ parameters for each model.

What if we want to <span style='color:var(--mk-color-orange)'>find the odds of some</span> $k_{1}$ against $k_{2}$, then we can do the following.

![[Multinomial Logistic Model.png|center|500]]

To <span style='color:var(--mk-color-orange)'>build this type of model</span> in <span style='color:var(--mk-color-purple)'>R</span> we can do the following:
```R
libarary(VGAM)
ml <- vglm(<y_var ~ x_vars, family = multinomial(refLevel = <Category Name>),
			data = data)
```

The **summary** of the model will look as such:
![[Multinomial Logistic Regression Model Summary.png|center|400]]

It is essentially the same thing but with 1 difference is that the <span style='color:var(--mk-color-yellow)'>categories are labeled with a number</span> and it corresponds to the model following the **"Names of linear predictors"**.

We can get the <span style='color:var(--mk-color-orange)'>fitted probabilities</span> for each category as such:
```R
# Gives the probability for each data point
prob <- fitted(ml)

pd1 <- data %>% select(x_vars) %>% mutate(catrogy_1 = probs[,1], category_2 = probs[,2],...)
```

We can **use the same evaluation matrix** to evaluate our model:
```R
preds <- colnames(fitted(ml))[apply(fitted(ml), 1, which.max)]
pd1 <- pd1 %>% mutate(pred_class = preds)

# Get the mean of correct predictions 
mean(pd1$prog$ == pd1$pred_class$)
```

Note that for multinomial models, we can <span style='color:var(--mk-color-yellow)'>only calculate the classification rate</span>.