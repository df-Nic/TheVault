---
Title: Random Forest
Date Created: 03-February-2026
Last Updated: 16-February-2026
Tags:
  - DSA3362
  - AI/ML/RandomForest
---
# Idea of Random Forest
---
We have introduced [[Year 3/Sem 2/DSA3362 - Predictive Data Analytics/Tree Based Methods.md|tree-based methods]] by looking at single trees. Then to reduce variance we looked at a [[Year 3/Sem 2/DSA3362 - Predictive Data Analytics/Bagging.md|bag of trees]] (*multiple trees*).

Now the **problem with all of this** when there is a <b><span style='color: var(--mk-color-red)'>dominant predictor in the dataset</span></b>. Even with bagging it would still have this dominant predictor in the top split (*the first split*).

>[!question] Why is this a problem?
>This results in different trees to be very similar & will <b><span style='color: var(--mk-color-red)'>not reduce the variance as much</span></b> when we aggregate the predictions.

We need to find a method to tweak the bag trees & <b><span style='color: #FFD700'>decorrelate the trees with the dominate predictor</span></b>. This is where <b><span style='color: #87CEEB'>random forest</span></b> comes in.

We essentially **do the same** as [[Year 3/Sem 2/DSA3362 - Predictive Data Analytics/Bagging.md#Idea of Bagging|bagging]], **but** when training these decision trees, <b><span style='color: #FFD700'>random sample a set of predictors from the entire collection at each split</span></b>.

>[!tldr] This ensures that not all trees will have the dominant predictor if it was not sampled
>We build multiple trees is because a single tree has high variance, by <b><span style='color: #98FB98'>aggregating the models it will solve the variance issue</span></b> (*boosting*). But if the multiple <b><span style='color: #FFD700'>trees are the same it means there are dominant predictors</span></b>.
>
>So this is when you might want to use random forest.

In practice for (*these are the defaults for the `randomForest` function in R*):
- **Regression** we sample $x / 3$ predictors
- **Classification** we sample $\sqrt{x}$ predictors

>[!important] Random forest is good when we have a lot of correlated inputs

>[!fail] Random forest is computationally expensive
>It does a $P \choose m$ (*P choose m*) at every split.

# Random Forest In R
---
To do random forest we can call the `randomForest` function in the <b><span style='color: #DDA0DD'>randomForest</span></b> package:

```R
library (randomForest)
rf_model <- randomForest(y_col ~ x_cols,
	data = df,
	mtry = 3, # How many predictors to randomly sample at each split
	importance = TRUE # can use "impurity"
)

print(rf_model) # Show the rmse & mape of the random forest
```

We can also use the `train` function in the <b><span style='color: #DDA0DD'>caret</span></b> package:

```R
tgbos <- expand.grid(
	mtry = c(4:6), # variables to sample, or leave blank if doing CV
	splitrule = "variance", # gini also works (for ranger only)
	min.node.size = c(3:5) # A list of 3 to 5 (for ranger only)
)

rf_model <- train(y_col ~ x_cols,
	data = df,
	method = "rf", # Same for classification & regression tasks. Can change to ranger if you want
	importance = TRUE, # can use "impurity"
	# We use CV to optmise the best mtry value
	trControl = trainControl(method = "cv",number = 5),
	tuneGrid = tgbos
)
```

In the above code snippet we did not include metric but we can include it depending on the task.

Then we can use the model with the `predict` to make the predictions & `confusionMatrix` for classification tasks to show the results.