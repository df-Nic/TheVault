---
Title: Bagging
Date Created: 03-February-2026
Last Updated: 24-April-2026
Tags:
  - DSA3362
  - AI/ML/Bagging
---
# Idea of Bagging
---
>[!tldr] Aka bootstrap aggregation

In models like random forest has <b><span style='color: var(--mk-color-red)'>high variance</span></b> (*a slight change can yield different results*). We want a model with <b><span style='color: #98FB98'>low variance</span></b> so that the model will <b><span style='color: #98FB98'>yield similar results</span></b> if applied repeatedly to distinct datasets.

A **method to reduce variance** is to:
1) Take many training sets from the population
2) Each training set build a model
3) Take the average of the predictions which results in a low variance statistical learning model

>[!warning] However taking multiple training sets from the population is not always possible
>Usually there is only 1 training set.

Thus, we will <b><span style='color: #FFD700'>take multiple resampling with replacements from the original dataset</span></b> to create multiple <b><span style='color: #87CEEB'>bootstrapped datasets</span></b>.

>[!important] These bootstrapped datasets have the same size as the original

So now the **process will be**:
1) <b><span style='color: #FFD700'>Create a bootstrap dataset</span></b> using the `sample` function with replacement
2) <b><span style='color: #FFD700'>Train</span></b> a model
3) Make a <b><span style='color: #FFD700'>prediction</span></b>
4) *Repeat step 1 - 3 again for as many times as you want*
5) Then <b><span style='color: #FFD700'>take the average</span></b> of the predictions (*for classification take the majority class*)

>[!danger] If every tree from each bootstrap sample is the same then use [[Year 3/Sem 2/DSA3362 - Predictive Data Analytics/Random Forest.md|random forest]] instead!
>This tells us that <b><span style='color: var(--mk-color-red)'>there is a dominant predictor</span></b> (*might not be important*) that is very good in partitioning the data which results in the <b><span style='color: var(--mk-color-red)'>same aggregated trees</span></b>.

And thus this <b><span style='color: #FFD700'>entire process is known as bagging</span></b>.

>[!important] Typically bagging tries to solve a high variance problem

>[!success] It effectively reduces the variance of a prediction through its aggregation process
>It is especially <b><span style='color: #98FB98'>good for models with unstable predication</span></b> (*regression trees*), making them more stable.

>[!success] Can be done in parallel

>[!fail]  Computation cost & memory requirements increase as the number of bootstrap samples increase

>[!fail] Less interpretable
>We now can't represent the resulting statistical learning procedure using a single model.
## Out-Of-Bag

So how do we reliably test the accuracy of the model? We use data called out-of-bag (*OOB*).

>[!info] Out-of-bag
>They are <b><span style='color: #FFD700'>observations not used to fit</span></b> a given bagged tree.

>[!info] In-bag
>They are <b><span style='color: #FFD700'>observations that was used to fit</span></b> a given bagged tree.

So if we have 2 models and our dataset contains only 3 observation. Lets say model 1 does not use observations 1 & 2, model 2 does not use observation value 3. Then we <b><span style='color: #FFD700'>test the individual models on the observations not used</span></b> (*asking the model to predict using OOB values*).

>[!note] The algorithm will leave out some observations so it will rarely be 0

Then we take the <b><span style='color: #FFD700'>average of the predictions per observation</span></b> (*regression is average, classification is the majority class*).

Then we can <b><span style='color: #FFD700'>compare this aggregate with the true label</span></b> (*actual y value*) and this is called a <b><span style='color: #87CEEB'>OOB error</span></b> & is a <b><span style='color: #98FB98'>reliable estimate of the test error</span></b> for bagged models.

>[!success] The OOB error corelates well with the cross-validation error or test error
>This is because of the numerous number of bootstrap datasets (*if we did a lot of it*).
# Partial Dependence Plot
---
It can be hard to visualise black box models like random forest, neural networks and so on. Thus <b><span style='color: #87CEEB'>partial dependence plot</span></b> (*PDP*) offers a simple solution by helping us <b><span style='color: #FFD700'>understand the marginal effect of a feature</span></b>.

We are essentially trying to understand how the <b><span style='color: #FFD700'>response variable changes as we change the value of a feature</span></b> (*increase or decrease*) while taking into account the average effect of all the other features in the model.

Here is how the **partial dependence algorithm** works:
1) Define $x$ number of evenly spaced values.
2) Copy the entire dataset
3) Replace the values for the chosen column to be $x_{i}$ (*the first evenly spaced number*)
4) Predict & take the aggregate
5) Repeat step 2 to 4 but take the next evenly spaced number

We can **plot a PDP graph** for this in R:
```R
partial.gr_liv_area <- partial(
	model,
	pred.var = "x col", # The chosen x column you want to visualise
	type = "regression",
	grid.resolution = 20, # creates 20 evenly spaced grid, change this
	chull = TRUE, # Your convex hull
	prob = TRUE,
	plot = TRUE
)
```

# Bagging in R
---
To do bagging we can call the `bagging` function in the <b><span style='color: #DDA0DD'>ipred</span></b> package:

```R
library(ipred)
set.seed(1) # Bagging involves randomness
bag <- bagging (
	y_col ~ x_cols,
	data = df,
	method = "class" # Or anove for regression tasks
	coob = TRUE,
	nbagg = 25, # nbagg just specify the number of bootstrap replicas of the original dataset
	control = rpart.control(minsplit = 1, xval = 1), # xval is the number of CVs
	parms = list(split = "gini") # Or information, no need this for regression
)
# For control there is also minbucket
bag # To print out the results of the bagged model
```

The `coob = TRUE` so that the <b><span style='color: #FFD700'>OOB sample is used to estimate the prediction error</span></b>.

You can also do **bootstrapping one by one** using the `sample` function:

```R
set.seed(1)
# Replace size with the length of the original dataset
# dim(): Row & Col, nrow(), ncol(), length(): Number of cols (same as ncol)
b1 <- df[sample(nrow(df),size = 10, replace = TRUE), ]
```

After building the bagged model, we can use `bag` (*or whatever the variable name is*) with `predict` to make the predictions & `confusionMatrix` for classification tasks to show the results.

**Alternatively** we can use the `train` function:

```R
tree_bagging <- train(y_col ~ x_cols,
	data = train ,
	method = "treebag",
	metric = "RMSE", # Change to Accuracy for classification
	coob = TRUE, # Same definition as above
	nbagg = 25, # number of bootstrap samples
	keepX = TRUE, # if Coob is tue this must be true as we need the predictors used
	minsplit = 1,
	minbucket = 1,
	xval = 1,
	trControl = trainControl(method = "oob") # A new method besides CV
	# We can also use trainControl(method = "boot", number = 25)
)
```

Then to get the **OOB error** do:
```R
tree_bagging$finalModel
```

Or we can **specify in the train control** as well:
```R
train_control <- trainControl(method = "boot", number = 25)
rpart_control <- rpart.control(cp = 0)

metric <- "Accuracy"

# Build the tree model
model <- train(
  y_col ~ x_col,
  data = train,
  method = "rpart2", # Or ranger
  trControl = train_control,
  metric = metric,
  control = rpart_control
)
```

There is also `ranger` which we need to import `library(ranger)`:

```R
n <- seq(from = 20, to = 200, by = 2)
err.bagcc <- numeric(length(n))
nt.bagcc <- numeric(length(n))
for (i in n){
	set.seed(123)
	fit.bagcc <- ranger:: ranger(formula = subscribed ~ .,
		data = trainset,
		num.trees = (i),
		mtry = ncol(trainset) - 1,
		min.node.size = 1
	)
	err.bagcc[i] <- fit.bagcc$prediction.error
	nt.bagcc[i] <- (i)
}
result.bagcc <- data.frame(Numtree = nt.bagcc, Error= err.bagcc) %>% filter(Numtree> 0)

head(result.bagcc)
```
