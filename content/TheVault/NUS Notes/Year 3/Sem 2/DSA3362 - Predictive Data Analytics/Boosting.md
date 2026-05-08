---
Title: Boosting
Date Created: 03-February-2026
Last Updated: 23-April-2026
Tags:
  - DSA3362
  - AI/ML/Boosting
---
# What Is Boosting
---
In [[Year 3/Sem 2/DSA3362 - Predictive Data Analytics/Boosting.md#What Is Boosting|bagging]] we bootstrap many datasets & make many models. In <b><span style='color: #87CEEB'>boosting</span></b>, we <b><span style='color: #FFD700'>grow the trees in a certain order utilising data from earlier trees</span></b> (*this is an iterative method & not like bagging which can be done in parallel*). This means that <b><span style='color: #98FB98'>it learns from its past mistakes</span></b>.

In other words each tree is <b><span style='color: #FFD700'>fitted to a modified version of the original dataset</span></b> rather than doing bootstrap sampling.

>[!important] The ideas it that we are predicting the residual not the actual value
>This is for gradient boosting.

The size of the tree is denoted by $d$.

**How boosting works**:
![[Images/DSA3362 Images/How Boosting Works.png|center]]

>[!info] Models that tend to learn slowly perform better so typically the learning rate is set to 0.1
>This is **denoted** by $\color{#FFD700}{\lambda}$ which is also known as the <b><span style='color: #87CEEB'>shrinkage parameter</span></b>.
>
>Generally boosting learns slowly, which leads to <b><span style='color: #98FB98'>less overfitting</span></b>.

>[!important] So typically boosting is used to solve high bias problem

So **as we build the random forest tree** if we take the <b><span style='color: #FFD700'>computed residual and add to the mean computed at the start it will be closer to the actual Y value</span></b>.

>[!info] When the max depth is just 1 the resulting tree is called a stump
>Which in boosting is good enough.

For **classification it is more complicated**:
- $B$ indicated the number of trees (*which CV can be used to find the best value*)
- $\lambda$ is the shrinkage parameter
- $d$ is the number of splits in each tree, controlling its complexity, also known as the interaction depth

But during **prediction**, we will pass the data into all the trees at the same time then we can compute the output using the <b><span style='color: #FFD700'>training average + the summation of the learning rate times the tree's output</span></b>.

>[!success] Flexibility to be weak learners
>We can do this by restricting the depth/size of the tree.

>[!success] Separate trees can be easily added to generate a prediction

>[!success] Trees can be generated very quickly
>Since individual trees can be directly aggregated, thus making them suitable for an additive modeling process.
# Boosting In R
---
To do boosting we can call the `gbm` function in the <b><span style='color: #DDA0DD'>gbm</span></b> package:

```R
library(gbm)
gbm (y_col ~ x_cols,
	data = df,
	distribution = "gaussian", # This is basically the loss function
	n.trees = 100,
	interaction.depth = 1,
	n.minobsinnode = 1,
	bag.fraction = 1,
	shrinkage = 0.1,
	keep.data = TRUE
)
```

**Alternatively** we can use the `train` function:

```R
# This is your grid search so change accordingly
tunegrid <- expand.grid (
	n.trees = seq(50, 200, by = 50), # Number of trees to fit so 100 = 100 iter of trained trees
	interaction.depth = c(1, 3), # Maximum depth of each tree
	n.minobsinnode = 10, # Min number of obs in the terminal nodes of the trees
	shrinkage = c(0.01, 0.1), # The learning rate
)

model <- train(y_col ~ x_cols,
	data = train,
	method = "gbm", # Or ada or xgbTree
	metric = "Accuracy",
	bag.fraction = 1, # Less than 1 is stochastic gradient boosting
	distribution = "gaussian", # Change to bernoulli for classification tasks
	tuneGrid = tunegrid,
	keep.data = TRUE,
	verbose = FALSE
)
```

>[!info] `bag.fraction` adds randomness
>So setting the value to 1 means you take the whole dataset to build the tree (*0.7 means 70% will be used to build the tree and so on*).

>[!note] Typically shrinkage and n.trees are used for hyper parameter tuning

You can do a prediction using a specific iteration tree using the `predict` function:

```R
predict(model, newdata = df) # Just change n.trees to the number
```
