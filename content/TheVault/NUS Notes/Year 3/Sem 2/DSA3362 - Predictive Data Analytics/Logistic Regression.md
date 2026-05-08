---
Title: Logistic Regression
Date Created: 14-January-2026
Last Updated: 23-April-2026
Tags:
  - DSA3362
  - AI/ML/LogisticRegression
---
# Logistic Regression
---
Unlike linear regression, logistic regression is for <b><span style='color: #FFD700'>classification problems</span></b>. It <b><span style='color: #FFD700'>predicts the probability of something being in this category</span></b>.

>[!question] Why can't we just use linear regression?
> When fitting a straight line the model could <b><span style='color: var(--mk-color-red)'>predict something larger than 1 or lower than 0</span></b> which makes it prediction not meaningful.

A logistic regression model has the following form (*2 class prediction*):
$$
p(X = x) = \frac{1}{1 + e^{-\beta_{0} -  \beta_{1}X_{1} - \dots - \beta_{p}X_{p}}}
$$
Where:
- $\beta$ is the coefficients

This limits the output to be between 0 & 1 which is within the acceptable range for any probability.

>[!info] You can think of logistic regression as a conditional probability

Typically a <b><span style='color: #FFD700'>simple cut off threshold of 0.5</span></b> is used to denote if the prediction is in this group or not.
## Odds

From the formula for logistic regression we can manipulate it to compute odds as well as log-odds (*logit*).

**Formula for odds**:
$$
\frac{p(X_{1})}{1 - p(X_{1})} = e^{\beta_{0}  +  \beta_{1}X_{1} + \dots + \beta_{p}X_{p}}
$$
>[!info] Odds denotes the ratio of something being in this particular category

**Formula for log odds or logit**:
$$
\ln \left(\frac{p(X_{1})}{1 - p(X_{1})} \right)= \beta_{0} +  \beta_{1}X_{1} + \dots + \beta_{p}X_{p}
$$

>[!abstract] Understanding log-odds
>Increase in $X_{1}$ the **logit** of the <b><span style='color: #FFD700'>probability of labeling in this category changes</span></b> by $\beta_{1}$.
>
>Or you can also interpret it as the **odds** of labeling in this category is <b><span style='color: #FFD700'>multiplied</span></b> by $e^{\beta_{1}}$ or the <b><span style='color: #FFD700'>increase / decrease in % in the odds of this category</span></b>.
# Sensitivity & Specificity
---
These are [[Year 3/Sem 2/DSA3362 - Predictive Data Analytics/Supervised Learning.md#For Classification Model|2 of the different metrices]] to evaluate a classification model. Ideally we want it <b><span style='color: #98FB98'>to be close to 1</span></b>.

However there is a <b><span style='color: var(--mk-color-red)'>inverse relationship between the 2 when we change the threshold</span></b>:
- **Specificity** increases as the cut off increases
- **Sensitivity** (*recall*) decreases as the cut off increases

>[!important] Thus a trade off between the 2 is required
## Receiver Operating Characteristics

Also known as the <b><span style='color: #87CEEB'>ROC</span></b> curve which is a <b><span style='color: #FFD700'>plot of sensitivity against specify</span></b> for all possible thresholds.

![[ROC Curve Example.png|center|400]]

Here the x-axis is specificity in decreasing order from 1 to 0, while the y-axis is sensitivity in increasing order from 0 to 1.

>[!question] How do we read the graph?
>We take many different thresholds and compute the sensitivity & specificity. This will form the curve as shown in the image above.

>[!note] When threshold is 0 sensitivity is 1 specificity is 0 & when the threshold is 1 its vice versa

To **evaluate the overall performance** of a classification model, we <b><span style='color: #FFD700'>compute the area under the ROC curve</span></b>.

>[!success] The ideal ROC will hug the top left corner
>This make the area under the curve to be 1.

>[!failure] If the area under the curve is 0.5 or less it is no better than making a random guess

>[!abstract] Obtaining the optimal cutoff point or the optimal trade off
>From the ROC curve we can also <b><span style='color: #98FB98'>retrieve the optimal cutoff point</span></b>. Essentially we draw a line (*the red dotted line*) at the top left corner and then we move it to the bottom right.
>
><b><span style='color: #FFD700'>The first time it intersects the curve is the optimal threshold</span></b> since it maximises specificity and sensitivity.

# Logistic Regression In R
---
## Building A Logistic Regression

To **build a logistic regression model** in R we can use the `glm(formula, data, family)` function. The 3 arguments:
1) **Formula** is written as such `Y_col ~ x_col_1`
2) **Data** which can be either a data frame, list or an environment
3) **Family** which specifies the error distribution to be used in the model

```R
# Similar to LR use the . for all other cols or specify yourself
glm <- glm(formula = y_col ~ ., data = df, family = binomial)
```

>[!note] For binary categories use `family = binomial`else use `family = poisson`

>[!note] You need to import the `caret` library

An alternative way is to use the `train(form, data, method, family, trControl)` function:
```R
glm <- train(form = y_col ~ ., data = df, method = "glm", family = "binomial", 
	trControl = trainControl(method = "none"))
```

Afterwards to get the coefficients we can do `glm$finalModel`.

## Making A Prediction

To **make a prediction** with a model we can use the `predict(object, newdata, type)` function. The 3 arguments:
1) **Object** is the fitted model
2) **New data** Is a data frame with new data
3) **Type** is usually set to `response` to return the estimated probability

```R
y_prob <- predict(fitted_model, data.frame(x_col = 100), type = "response") # Get the probability, use class to get the actual lable (50% threshold)
# This is to assign the lables, note we can change the threshold
predictions <- factor(ifelse(y_prob > 0.5, "Category 1", "Category 2") , levels = c("Category 1", "Category 2"))
```

>[!info] If we use the `train` function to build the model we can directly use the `predict` function as such `predict(model, data)`

We can **build a simple confusion** matrix using the `table` function to see our model's performance or we can use the [[Year 3/Sem 2/DSA3362 - Predictive Data Analytics/Introduction to Caret.md#Evaluating the Model|confusionMatrix function in caret]].

```R
table(predict = predictions, actual = original_data)
```
### Finding the Optimal Threshold

To plot the [[Year 3/Sem 2/DSA3362 - Predictive Data Analytics/Logistic Regression.md#Receiver Operating Characteristics|ROC curve]] we can use the `plot.roc` function with the following arguments:
```R
plot.roc(default_lables, predicted_probabilities, print.auc = TRUE, print.thres = "best")
```

Where the first 2 arguments are:
- **Observed lables** which is the original datasets labels
- **Predicted probabilities** which is the predicted probabilities that the model outputted.

With this it will show the best threshold on the graph when plotted.