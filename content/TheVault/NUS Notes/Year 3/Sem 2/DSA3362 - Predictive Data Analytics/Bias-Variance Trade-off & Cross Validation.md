---
Title: Bias-Variance Trade-off & Cross Validation
Date Created: 20-January-2026
Last Updated: 24-April-2026
Tags:
  - DSA3362
---
# Bias & Variance
---
To **improve on the prediction** accuracy of a model, we can <b><span style='color: #FFD700'>increase its complexity</span></b>. For example, linear regression we can go into quadratic or cubic equations while for KNN we can reduce K.

>[!fail] This leads to overfitting as the model is too specific to the training data
## Prediction Error Components

There are 3 components of prediction errors:
1) **Bias**
2) **Variance**
3) **Irreducible error** (*Error or noise from the data which is unavoidable*)

![[Bias & Variance.png|center|500]]

>[!tldr] Bias is the difference between the average of the predicted labels & the true label
>High bias happens when models are <b><span style='color: var(--mk-color-red)'>underfitted</span></b>. Because the model is simple & it cannot capture the relationship thus making wrong predictions within the dataset.

>[!tldr] Variability is the variability of the model's prediction
>High variance happens when models are <b><span style='color: var(--mk-color-red)'>overfitted</span></b>. When the model is introduced to new data it gives the wrong answers.

Our aim is to have a model with <b><span style='color: #98FB98'>low bias & low variance</span></b>.
## Trade-Off

![[Bias-Variance Trade-Off Graph.png|center|350]]

From the graph there is a <b><span style='color: #FFD700'>inverse relationship between bias & variance</span></b> in terms if model complexity. As <b><span style='color: #FFD700'>complexity increases bias decreases while variance increases</span></b>.

>[!note] Bias here can also be though of as the training error

>[!success] Goal: Find the sweet spot which minimises bias & variance
## Zero & Near-Zero Variance

>[!important] Here we are focusing on the variance within the dataset

Sometimes the <b><span style='color: var(--mk-color-red)'>variable does not provide information</span></b> about the response variable. This is known as <b><span style='color: #87CEEB'>non-informative predictors</span></b>. **Omitting** these variable may <b><span style='color: #98FB98'>speed up the model training process</span></b>.

>[!info] Zero variance
>They are predictors comprising of single values. This means that the <b><span style='color: #FFD700'>column contains only 1 unique value</span></b>. Which means the standard deviation is 0

>[!info] Near zero variance
>There are **2 conditions** which makes a variable near zero:
>1) The column has <b><span style='color: #FFD700'>very few unique values relative to the number of samples</span></b> (*10% or less unique values*).
>2) The ratio of the <b><span style='color: #FFD700'>frequency of the most common value to the second most common value is large</span></b> (*more than 20% difference or a ratio  of 1:20*)
# Cross Validation
---
>[!tldr] Cross validation
>CV is a statistical method used to estimate the prediction error of the supervised learning model under consideration, on data that was not used to train or fit it.

We can use CV to <b><span style='color: #FFD700'>train a set of different complexity models</span></b> & <b><span style='color: #FFD700'>select the optimal model</span></b> that gives the lowest cross-validation error.

>[!info] When we say complexity models, it means different models
>For example, one can be a linear model, the other can be a quadratic model.
## Holdout Method

![[Holdout Method.png|center|250]]

The basic method is to <b><span style='color: #FFD700'>split the data into train & test</span></b>. We train the modeling using the training set & then <b><span style='color: #FFD700'>evaluate it using the test set and compute the error metric</span></b>.

We **repeat this process of evaluation** for all the other candidate models and <b><span style='color: #FFD700'>select the optimum model with the lowest error metric</span></b>.
## K-Fold Cross-Validation

![[K-Fold Cross-Validation.png|center|500]]

We split the data into <b><span style='color: #FFD700'>k equal nonoverlapping subsets</span></b> called <b><span style='color: #87CEEB'>folds</span></b>.

In a round we set <b><span style='color: #FFD700'>one of the folds to be the testing set</span></b> & we <b><span style='color: #FFD700'>train the model with the rest</span></b> & compute the error metric.

>[!important] We do this until each fold has a chance to be the testing set exactly once
>Similarly a fold will be used for training k - 1 times.
>

>[!success] It does not matter how the data is initially split, every fold will get a chance to be the test set

Thus in CV the cross validation error, though follows the [[Year 3/Sem 2/DSA3362 - Predictive Data Analytics/Bias-Variance Trade-off & Cross Validation.md#Trade-Off|U shape pattern against model complexity]] It will be <b><span style='color: #FFD700'>somewhere between the test & training error</span></b> for the best model from cross validation.

The <b><span style='color: #98FB98'>best model will be the one with the lowest</span></b> <b><span style='color: #87CEEB'>cross-validation error</span></b>, which is the <b><span style='color: #FFD700'>average of all the errors from each round</span></b> or <b><span style='color: #FFD700'>the best model</span></b>.
# Cross Validation in R
---
We can do CV using the <b><span style='color: #DDA0DD'>caret</span></b> package. Recall the [[Year 3/Sem 2/DSA3362 - Predictive Data Analytics/Introduction to Caret.md#Building a Model|train function]] there is an argument called `trControl` which we can specify to <b><span style='color: #FFD700'>control how the model is trained</span></b>.

```R
set.seed(987)
ctl <- trainControl(method = "cv", number = 4) # CV is cross validation and number is the no of folds

fit.glm <- train(form = price ~., # Change this based on the model you want to build
	data = training,
	method = "lm", # Model type
	trControl = ctl # To control how the model is optimised
)
```
## Extracting Information from a Trained Model

To **visualise the different folds** we can use `model$control$index`.

To get the **cross validation evaluation metrics** we can use `model$results`, but if we want the **evaluation metric for each fold**, use `model$resample`.

To see the **final best model** use the following `model$finalModel`.
# Removing Near Zero & Zero Variance Variables in R
---
In the <b><span style='color: #DDA0DD'>caret</span></b> there is a `nearZeroVar` function which does this for us. How it works is that it will [[Year 3/Sem 2/DSA3362 - Predictive Data Analytics/Bias-Variance Trade-off & Cross Validation.md#Zero & Near-Zero Variance|check if any of the 3 conditions is satisfied]] which makes it zero or near zero variance.

```R
omitcol <- caret::nearZeroVar(df, names = TRUE, freqCut = 20, uniqueCut = 10) 
# names = TRUE returns us the column names that needs to be removed
df_new <- df[ ,!(names(df) %in% omitcol)]

# You can also get the number of variables that hit the thresholds
# Near 0
sum(nzv_metrics$percentUnique < 0.1)
sum(nzv_metrics$freqRatio > 20)
sum(nzv_metrics$nzv == TRUE)

# Zero var
sum(nzv_metrics$zeroVar == TRUE)
```