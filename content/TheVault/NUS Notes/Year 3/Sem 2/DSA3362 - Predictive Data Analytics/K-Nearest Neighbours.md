---
title: K-Nearest Neighbours
Date Created: 2026-01-20
Last Updated: 2026-01-23
tags:
  - DSA3362
  - AI/ML/KNN
---
# K-Nearest Neighbours
---
It is an algorithm to <b><span style='color: #FFD700'>solve classification problems</span></b>. But unlike approaches which models the relationship between X and Y, it <b><span style='color: #FFD700'>directly predicts the label by looking at the closest K points</span></b> on the dataset to the observed point.

KNN itself is a <b><span style='color: #FFD700'>simple model</span></b>, thus its not used quite as often because there is <b><span style='color: #FFD700'>very little fine tuning needed</span></b>. But though is simple, it is <b><span style='color: #98FB98'>used for its efficiency purposes</span></b> for certain tasks like image classification.
## KNN Algorithm

>[!info] Assume we have 2 input variables X1 & X2

![[KNN Algorithm Example.png|450]]

To **compute the distance** between points we can use the <b><span style='color: #87CEEB'>Euclidean distance</span></b>:
$$
d(A, B) = \sqrt{(X_{1}^{A} - X_{1}^{B} ) ^ {2} + (X_{2}^{A} - X_{2}^{B} ) ^ {2} + \dots + (X_{n}^{A} - X_{n}^{B} ) ^ {2}}
$$
## Factors Affecting a KNN Algorithm

Some factors which KNN is sensitive to are:
1) **Value of K**
Changing K will increase the number of neighbours which can change the final prediction.

>[!note] Setting `k` to be the number of observations leads to underfitting while setting it to 1 leads to overfitting
>So we will want a [[Year 3/Sem 2/DSA3362 - Predictive Data Analytics/Bias-Variance Trade-off & Cross Validation.md#Trade-Off|trade off between bias & variance]].

>[!important] Always set K to be odd
>If there is a <b><span style='color: var(--mk-color-red)'>tie, the algorithm will randomly pick a label</span></b>. Thus setting it to odd will prevent ties from happening.

2) **Scaling on input variables**
For a continuous variable, <b><span style='color: #87CEEB'>Z-score scaling</span></b> is used for scaling:
$$
Z = \frac{X - \mu_{X}}{\sigma_{X}}
$$
Where:
- $\mu_{X}$ is the mean of X
- $\sigma_{X}$ is the standard deviation of X

>[!important] We scale because KNN calculates distance which is sensitive to scale
# KNN in R
---
We can generate **all pairs distance matrix** using the `dist(data, method, upper)` function:
```R
# Replace whats incide c() with the columns you are using
dist(df[c(1,2,3)], method = "euclidean", upper = TRUE)
```

To **scale the data**, we can use the `scale` function:
```R
# Change the indexs based on your dataset & what you want to scale
df[1:2] <- scale(df[1:2], center = TRUE, scale = TRUE)
# Center takes each datapoint and minus the average, scale divides it by the SD
```

What `center` does is takes the <b><span style='color: #FFD700'>average of the column & subtracts it from each value</span></b>.

For `scale`, it <b><span style='color: #FFD700'>divides the value by the standard deviation</span></b>.
## Building a KNN Model

But to **train a KNN model**, we can use the `knn3(formula, data, k)` function in caret:
```R
# Update the forumla depending on the variables you want to use
knn_model <- knn3(formula = Y_col_name ~ ., data = df, k = 3) # k specify the number of nearest neighbours
```

If using the `train` function:
```R
knn_model <- train ( Y_col_name ~ ., 
	data = df ,
	method =" knn", 
	tuneGrid = data.frame (k=3) , # Set K, BUT REMOVE this if we using CV to find the best K
	trControl = trainControl ( method = " none ") # Change to method = "cv", number = 4 for CV
)
```

After building the KNN model, we can **predict** using the `predict(object, newdata, type)` function:
```R
knn_predictions <- predict(object = knn_model, newdata = df, type = 'class') # Use raw if you are using the train function from the caret package
```

>[!important] If we do not put `type = class` it will return the proportion of the majority class and not the label itself
## Evaluating the KNN Model

Then we can **evaluate the model** by creating the confusion matrix by using the `table` function
```R
cm <- table(expected_labels, predicted_labels)
```

Or you can use the [[Year 3/Sem 2/DSA3362 - Predictive Data Analytics/Introduction to Caret.md#Evaluating the Model|Caret's confusionMatrix function]].
## Visualising the KNN Model

We can interpret the KNN model and understand how it predicts by using the `knn.plot(x, y, model, k, positive)` function.

```R
KNN.plot (
	x = df [ ,1:2] , y = df [,3] , # Replce the indexes according to your dataset
	model = knn_model , k = 3, positive = "Y")
```

This is how the graph will look like, and how to interpret it:
![[KNN Plot Interpretation.png|500]]

>[!info] As K increases, the regions of prediction tend to be simpler & the boundaries become smoother

