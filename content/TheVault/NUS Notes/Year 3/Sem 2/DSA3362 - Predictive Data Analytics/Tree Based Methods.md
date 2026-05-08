---
Title: Tree Based Methods
Date Created: 26-January-2026
Last Updated: 23-April-2026
Tags:
  - DSA3362
  - AI/ML/DecisionTrees
---
# Decision Trees
---
It is similar to a [[Year 1/Sem 2/CS2040S - Data Structures and Algorithms/Trees.md|tree data structure]], where there is a root node, branches & leaf nodes.

![[Decision Trees.png|center|500]]

>[!info] Root node
>It represents the <b><span style='color: #FFD700'>most important predictor</span></b>.

>[!info] Branches
>It represents the <b><span style='color: #FFD700'>decision rules</span></b>.

>[!info] Leaf Node
>It represents the terminal nodes which represents the <b><span style='color: #FFD700'>predicted outcomes</span></b>.

>[!question] Why tree-based models?
> - Generate a set of conditions that are <b><span style='color: #98FB98'>highly interpretable & easy to implement</span></b>
> - <b><span style='color: #98FB98'>Effectively handle many types of predictors without the need to pre-process</span></b> them due to the logic of their construction
> - <b><span style='color: #98FB98'>Does not require the user to specify the form of the predictors relations to the response</span></b>
> - They can <b><span style='color: #98FB98'>handle missing data</span></b> & <b><span style='color: #98FB98'>implicitly conduct feature selection</span></b>

>[!fail] Model instability / high variance
>**Slight changes in the data** can <b><span style='color: var(--mk-color-red)'>change the structure & interpretation</span></b> of the tree.

>[!fail] Less than optimal predictive performance
> Due to the model defining the rectangular regions that contains more homogeneous outcome values.
> 
> Essentially if the <b><span style='color: var(--mk-color-red)'>predictors & response cannot be defined by the rectangular subspaces</span></b>, then it will have worse performances.
>
>>[!note] To combat this we can use ensemble methods that combine many trees into 1 model 
# Types of Tree Models
---
>[!important] All trees do a binary split
>So if we split by a categorical column that has more than 3 classes we still do a binary split.
## Regression Tree

The idea behind a regression tree is simple, given a dataset, <b><span style='color: #FFD700'>pick a mid point between 2 variables to make our decision, then split the dataset into 2 sets using this binary split</span></b>, to predict some quantitative response.

>[!info] We are just trying to split the data on the chosen variable based on some threshold

Then **repeat** the process with multiple different thresholds (*or cut point*) to <b><span style='color: #FFD700'>minimise the overall sum of squares error</span></b> (*this is how the model splits the data*).

$$
\text{SSE} = \sum_{i \in S_{1}} (y_{i} - \bar{y_{1}})^{2} + \sum_{j \in S_{2}} (y_{j} - \bar{y_{2}})^{2}
$$
Where:
- $S_{1}$ and $S_{2}$ are the 2 sets after dividing the dataset
- $\bar{y_{1}}$ and $\bar{y_{2}}$ are the <b><span style='color: #FFD700'>averages of the training set within sets 1 & 2 respectively</span></b> (*this is how they predict*)

**After finding the best cut point**, it will <b><span style='color: #FFD700'>recursively split</span></b> any of the sets to repeat the whole process again.

>[!warning] The model does an exhaustive search so if we have many unique values then we have a lot of cut offs to iterate through

>[!abstract] Complexity parameter
>We can think of this as a <b><span style='color: #FFD700'>penalty which we can add to our SSE</span></b>. It <b><span style='color: #98FB98'>controls how the tree is growing</span></b>.
>
>This penalty is just the complexity parameter (*hyperparameter*) $\times$ <b><span style='color: #FFD700'>number of terminal nodes</span></b> (*the last nodes in the tree*).
>
>We can also use this for classification models where we add this to the misclassification rate.

**Example of a regression tree being built**:
![[Regression Tree.png|center|500]]

## Classification Tree

**Similar** to our [[Year 3/Sem 2/DSA3362 - Predictive Data Analytics/Tree Based Methods.md#Regression Tree|regression tree]], but it <b><span style='color: #FFD700'>predicts qualitative response</span></b> (*yes or no*) instead of a quantitative one.

For a classification tree, its aim is to partition the data into <b><span style='color: #FFD700'>smaller & more homogeneous groups</span></b>. By <b><span style='color: #FFD700'>maximising accuracy or equivalently by minimising misclassification errors</span></b> (*by partitioning & not predicting*).

>[!info] Homogeneity in this context means that the node splits are purer
>A <b><span style='color: #87CEEB'>pure split</span></b> means that the resulting spitted sets will <b><span style='color: #FFD700'>contain more of a single class than the parent node</span></b>.
>
>So generally as we go down the tree we want it to be more pure. And this is how the model splits the data.

>[!info] Pure node
>It means that this <b><span style='color: #FFD700'>node only has 1 class and no more</span></b>.
### Computing Impurity

#### Gini Index

A way of **computing impurity** is through the <b><span style='color: #87CEEB'>Gini index</span></b>. For a **2 class problem** we can compute it using the following formula:
$$
p_{1}(1 - p_{1}) + p_{2}(1 - p_{2}) = 2 \times p_{1} \times p_{2}
$$
Where:
- $p_{1}$ and $p_{2}$ are the probability of class 1 & 2 within a group after the split

>[!note] We can simplify the formula because $p_{1} + p_{2} = 1$

**Another way to write the formula for Gini index** is:
$$
\sum^{K}_{k = 1} P_{mk}(1 - P_{mk})
$$
Where:
-  $m$ is the partitioned group or in other words one of the subgroups. So if we split by gender then we have 2 subgroups so $m$ can be male, female
- $k$ is the $k^{th}$ class, so if we have 2 classes yes or no that is what $k$ will be
- $P_{mk}$ is the proportion of the of the observations in group $m$ & are in class $k$

If the Gini index is **minimised** it mean a <b><span style='color: #98FB98'>purer node</span></b>. This is because the probability of one class will be close to 0. And similarly the Gini index is **maximised** it means a <b><span style='color: var(--mk-color-red)'>less purer node</span></b>.

>[!info] Overall Gini index
>It is a weighted purity value by the <b><span style='color: #FFD700'>proportion of samples in the node relative to the total number of samples in the parent node after splitting</span></b>.
>
>This is used to <b><span style='color: #FFD700'>find the optimal split point</span></b> where it results in the lowest Gini index.

>[!example] Example of computing the Gini index
>
|  Age   | Class "No" | Class "Yes" | Total: |
| :----: | :--------: | :---------: | :----: |
|  > 33  |     5      |      2      |   7    |
| <= 33  |     0      |      3      |   3    |
| Total: |     5      |      5      |   10   |
>
> For customers **above 33** years old, the Gini index is $2 \times 5/7 \times 2/7 = 0.408$.
> 
> For the **other group** the Gini index is $2 \times 0/3 \times 3/3 = 0$.
> 
> The **overall Gini index** (*weighted*) is $7/10 \times 0.408 + 3/10 \times 0 = 0.286$.
> 
> For the **parent node** it will just be $2 \times 5/10 \times 5/10 = 0.5$
#### Cross Entropy

Another way to compute the impurity is <b><span style='color: #87CEEB'>cross entropy</span></b> and the **formula** is:
$$
- \sum^{K}_{k = 1} P_{mk}(log(P_{mk}))
$$
Where:
- $m$ is the partitioned group or in other words one of the subgroups. So if we split by gender then we have 2 subgroups so $m$ can be male, female
- $k$ is the $k^{th}$ class, so if we have 2 classes yes or no that is what $k$ will be
- $P_{mk}$ is the proportion of the of the observations in group $m$ & are in class $k$

We can **convert** this formula into a <b><span style='color: #87CEEB'>weight cross entropy</span></b> by using this formula:
$$
- \sum^{K}_{k = 1} P_{m}[P_{mk}(log(P_{mk}))]
$$
Where:
- $P_{m}$ is the proportion of split criteria $m$ against the total number of data points before splitting into groups

And similarly, the **smaller the cross entropy**, the <b><span style='color: #98FB98'>purer the group</span></b>.
### Information Gain

To determine which attribute to use to split the data it calculates something called <b><span style='color: #87CEEB'>information gain</span></b>.

>[!note] It will pick the attribute that gives the highest information gain as the variable to split the data

To **compute the information gain**, we use the following formula:
$$
\text{Information Gain (IG)} = \text{Entropy of Parent} - \text{Entropy of Children}
$$
Where:
- Entropy of the parent is the base cross entropy before doing the split
- Entropy of the children is the **weighted sum of the cross entropy** for all $m$ where m is all possible subgroups after division, this is known as the <b><span style='color: #87CEEB'>conditional entropy for the variable</span></b>.

>[!important] We can also use the Gini index of the parent minus the Gini index of the child as well

>[!note] When computing IG we are computing the purity of the node

In <b><span style='color: #DDA0DD'>Caret</span></b>, it computes something called <b><span style='color: #87CEEB'>improve score</span></b>, which is just $IG \times \text{number of data in the parent}$.

>[!question] What if all splits give the same IG?
>It will still take one splits but <b><span style='color: #FFD700'>keep all but one as a surrogate split</span></b> (*which produces surrogate trees, trees with same performance but different splits*).

>[!example] A full example of computing information gain
> | contact / subscribed | Class "Yes" | Class "No" | Total: |
| :------------------: | :---------: | :--------: | :----: |
|       Cellular       |     180     |    1107    |  1287  |
|      Telephone       |     11      |    125     |  136   |
|       Unknown        |     20      |    557     |  577   |
|        Total         |     211     |    1789    |  2000  |
> Assuming we are splitting by contact type, our $m$ will be cellular, telephone & unknown while $k$ is yes or no.
> 
> Calculating the base entropy of the parent node is $-((211/2000)*log_{2}(211/2000) + (1789/2000)*log_{2}(1789/2000))$.
> 
> Calculating the weighted cross entropy for each of the children, meaning each different contact type: 
> - $0.6435 × (0.1399 log_{2}(0.1399) + 0.8601 log_{2}(0.8601)$ (*cellular*)
> - $0.0680 × (0.0809 log_{2}(0.0809) + 0.9191 log_{2}(0.9191)$ (*telephone*)
> - $0.2885 × (0.0347 log_{2}(0.0347) + 0.9653 log_{2}(0.9653)$ (*unknown*)
>  
>  Then we take the sum of all of these and negate the value.
>  
>  Then we subtract the entropy of the parent with the children, $0.4862 − 0.4661 = 0.0201$

Tree which are constructed to have the **maximum depth** (*deep tree*) are more likely to be <b><span style='color: #FFD700'>overfitted</span></b>. A <b><span style='color: #98FB98'>more generalisable</span></b> tree is the **pruned** version <b><span style='color: #FFD700'>determined by cost-complexity tuning</span></b>.

The <b><span style='color: #87CEEB'>cost-complexity factor</span></b> is called the <b><span style='color: #87CEEB'>complexity parameter</span></b> & can be incorporated into the
tuning process to <b><span style='color: #FFD700'>estimate an optimal value</span></b>.

>[!success] Highly interpretable / commutable

>[!success] Can handle many types of predictors & missing data
>Only <b><span style='color: #FFD700'>non-missing information samples will be used to create the split</span></b>. As for <b><span style='color: #FFD700'>prediction, surrogate splits</span></b> can be used for missing data.

>[!fail] Suffer from model instability

>[!fail] May not produce optimal predictive performance
# Tree Based Models in R
---
Before building the model, we can first do [[Year 3/Sem 2/DSA3362 - Predictive Data Analytics/Introduction to Caret.md#Getting the Important Variables|feature selection]] using the `filterVarImp` function to reduce the number of variables & then [[Year 3/Sem 2/DSA3362 - Predictive Data Analytics/Introduction to Caret.md#Splitting the Data|split into a train & test set]] using the `createDataPartition` function.
## Regression Tree

To build a regression tree we can use the `train` function from <b><span style='color: #DDA0DD'>Caret</span></b>. For a regression tree the `method = "rpart"`.

>[!important] Metric used to train tree models is for the final model selection the underlying rpart library will still minimise SSE

```R
tree_model <- train(y_col ~ .,
	data = trainSet,
	method = "rpart", # Or rpart2 which optimised maxdepth for you
	trControl = trainControl(method= "cv", number = 5),
	control = tree_specs
	metric = "RMSE")
```
## Classification Tree

It is the same as building a regression tree in R but we need to change `metric = "Accuracy"`.
```R
tree_model <- train(y_col ~ .,
	data = trainSet,
	method = "rpart", # Or rpart2
	trControl = trainControl(method= "cv", number = 5),
	metric = "Accuracy")
```

Then to get the confusion matrix we can do the [[Year 3/Sem 2/DSA3362 - Predictive Data Analytics/Introduction to Caret.md#Evaluating the Model|same as before]] by using the `predict` & `confusionMatrix` functions.

For **both** tree types we can also use the underlying function in the rpart library, `rpart`:
```R
rpart(y_col ~ .,
	data = trainSet,
	method = "class", # Class for classification, anova for regression
	# cp, is the complexity
	# minsbucket, min number of data within the bucket
	# maxdepth is how many splits at max, not how deep the tree is
	# There is also minsplit to ensure how many split the tree must have
	control = rpart.control(minsbucket = 50, maxdepth = 3),
	parms = list(split = "information") # Can be gini
)
```
## Visualising the Tree

To visualise the decision tree that was trained use the `rpart.plot` function:
```R
rpart.plot(tree_model$finalModel, type = 3, digits = -3)
```

The plot will show some figures in the leaf nodes, to interpret it:
- The 1st is the predicted value (*quantitative which is just the average or qualitative*)
- The 2nd is the proportion per group:
	- **Regression trees** it is the <b><span style='color: #FFD700'>proportion of the data within the set</span></b> in %
	- **Classification tree** is the <b><span style='color: #FFD700'>proportion of the positive class</span></b> in the set in %
- The 3rd which **only shows for classification tree** is the <b><span style='color: #FFD700'>proportion of the data within the set</span></b> in %

>[!note] Do note that if we do `varImp` the important variables might be rank lower than what was used in the tree

>[!question] How does the algorithm know which side of the split to split again
>Essentially we will compute the matric (*SSE or Information Gain*) within the respective groups (*or splits*). Then we compare the best matric value within these respective subgroups and split it.
>
> >[!example] So lets say a regression tree we already did 1 split so we compute the lowest SSE within the 2 subgroups. Then we compare the 2 lowest SSE's & split the group further for the one with the lowest SSE.
> 
