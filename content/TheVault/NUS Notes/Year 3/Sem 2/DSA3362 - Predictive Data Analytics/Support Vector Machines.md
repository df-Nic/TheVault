---
Title: Support Vector Machines
Date Created: 08-February-2026
Last Updated: 24-April-2026
Tags:
  - DSA3362
  - AI/ML/SVM
---
# Maximal Margin Classifier
---
Let's look at a more strict version of a support vector machine which is called a <b><span style='color: #87CEEB'>maximal margin classifier</span></b> which tries to find a <b><span style='color: #FFD700'>linear boundary</span></b> (*separating hyperplane*) which <b><span style='color: #FFD700'>separates 2 classes perfectly</span></b>.

>[!fail] It is strict because the model will fail completely if the data is not perfectly separable

So essentially if the predicted value is below this linear boundary it will be in a class & if it is above it will be in the other class.

However there are almost an infinite number of ways to form this **hyperplane** so how do we get the **best** one? The best one will be the <b><span style='color: #FFD700'>one with the largest margin between the closest data point from both classes</span></b>.

>[!abstract] Margin
>It is the <b><span style='color: #FFD700'>distance of the hyperplane to the closest data point of either class</span></b> (*perpendicular distance*).
>
>This margin on either side of the hyperplane <b><span style='color: #FFD700'>need not be the same</span></b>.

>[!question] Why take the largest?
>It is because we want our model to be <b><span style='color: #98FB98'>tolerant to local disturbances</span></b> (*more confident*).
>
>Think about it, if we **put the hyperplane at the data point** which separates the classes. Any <b><span style='color: #FFD700'>noise will cause the prediction to be incorrect</span></b>. By widening the margin we are <b><span style='color: #98FB98'>increasing the models confidence</span></b>.

Then the <b><span style='color: #FFD700'>closest point from this best margin / separator from all the classes</span></b> is known as the <b><span style='color: #87CEEB'>support vector</span></b>.

>[!abstract] Support vector
>These **supports the maximal margin hyperplane**, in a sense that if these <b><span style='color: #FFD700'>points were to move, the hyperplane & its boundary will move as well</span></b>.
>
>These support vectors <b><span style='color: #FFD700'>lie on or between</span></b> (*for SVC*) the <b><span style='color: #87CEEB'>margin boundary</span></b>. 
>
>Do note that any other points other than the support vector (*between the 2 margins*) has no effect on the maximal margin, unless they move closer than the 2 support vectors.

>[!info] Maximal margin classifier is a hard margin
>It means that <b><span style='color: #FFD700'>no datapoint can lie between the margin</span></b>.
## Mathematical Formulation

So given 2 classes, positive ($y = 1$) & negative ($y = -1$) to be able to **predict / correctly classify given a variable** we use the following inequality:
$$
y[i] (b + x[i]) \gt 0
$$
Where:
- $i$ is the data point / entry
- $y[i]$ is the ith data point's y column value (*either 1 or -1 in our case*)
- $x[i]$ is the ith data point's x column value
- $b$ is the decision point or our hyperplane

>[!question] Why this inequality holds?
>The main idea is multiplying by $y[i]$, if it is <span style='color: #FFD700'>negative we can multiply -1 on both sides which will flip the symbol</span> $\gt$ to $\lt$ thus the negative class will be on 1 side of the hyperplane and the positive side on the other.

If we **desire a hard margin** of size $M$ we can change the inequality to:
$$
y[i] (b + x[i]) \ge M
$$

Then for our maximal margin classifier we just want to find the largest $M$.

>[!important] This inequality must hold for all data points in the training data

### Solving The Maximisation Problem

To solve the inequality to find the maximum $M$, lets rewrite the inequality:
$$
y[i] (b + x[i]) \ge M = y[i] (\frac{b}{M} + (\frac{1}{M})x[i]) \ge 1
$$
Let:
- $\beta_{0}$ to be $b / M$
- $\beta_{1}$ to be $1 / M$ which can be converted into $M = 1 / \beta_{1}$

So now to **maximise** $M = 1 / \beta{1}$ is the same as <b><span style='color: #FFD700'>minimising</span></b> $\color{#FFD700}{\beta_{1} \gt 0}$ (*cannot be 0 is not is a division by 0 problem*) or minimising $\color{#FFD700}{1/2 \beta_{1}^{2}}$.

So this is now a [[Year 2/Sem 1/CS2109S - Introduction to AI & Machine Learning/Support Vector Machines.md#Lagrange Function|convex optimisation problem]], why this is because we <b><span style='color: #FFD700'>have a quadratic equation</span></b> ($1/2 \beta_{1}^{2}$) with a <b><span style='color: #FFD700'>linear inequality constraint </span></b> ($y[i](\beta_{0} + \beta_{1}x[i]) \ge 1$).

We can **solve** this using <b><span style='color: #FFD700'>quadratic programming with Lagrange multipliers</span></b>. The **optimal values of the Lagrange multipliers** <b><span style='color: #FFD700'>corresponding to the support vectors are nonzero</span></b>.

>[!note] The number Lagrange multipliers depends on the number of data points in your dataset
>They are labelled as $\alpha_{1}, \dots \alpha_{n}$ each is associated with the datapoint. And the estimates values to solve our maximisation problem are denoted as, $\hat{\alpha_{1}}, \dots \hat{\alpha_{n}}$.

So with the nonzero Lagrange multipliers we can solve for $\hat{\beta_{1}}$ &$\hat{\beta_{2}}$ (*the optimal values for the 2* $\beta$)
- $\hat{\beta_{1}} = \sum {\alpha_{i} \times y[i] \times x[i]}$ (*for all i where the Lagrange multipliers are non zero*)
- $\hat{\beta_{0}} = y[i] - \hat{\beta{1}} \times x[i]$ (*where i is any nonzero Lagrange multiplier, any one will yield the same value*)

Now with the best beta values you can **solve for M & b**:
- $\hat{M} = 1 / \hat{\beta{1}}$
- $\hat{b} = \hat{\beta_{0}} \times \hat{M}$
# Support Vector Classifier
---
It is known to be one of the **best out of the box classifiers** as it can <b><span style='color: #98FB98'>perform well in multiple scenarios</span></b>.

>[!fail] Like with all SVMs they are bad with tall data, meaning it has many rows but very little columns

>[!fail] Unlike logistic regression it only produces class labels
>So they are are <b><span style='color: #FFD700'>hard classifier</span></b>, which means we will not know how confident the model is (*maybe it is 50.1%*).

Support vector classifier goal is to <b><span style='color: #FFD700'>classify</span></b> future observations based on observed values. The idea is to find a <b><span style='color: #87CEEB'>hyperplane</span></b> that <b><span style='color: #FFD700'>separates the data as optimally as possible while allowing for some level of violation</span></b> (*binary classification*). This <b><span style='color: #98FB98'>improves generalisability</span></b>.

>[!question] Then what is a support vector machine?
>SVMs are essentially an **extension** to a support vector classifier by <b><span style='color: #FFD700'>enlarging the feature space to accommodate non-linear boundary between classes</span></b>, using [[Year 2/Sem 1/CS2109S - Introduction to AI & Machine Learning/Support Vector Machines.md#Kernel Methods & Tricks|kernels]].

>[!tldr] Hyperplane
>It is a flat <b><span style='color: #FFD700'>subspace of dimension p - 1 where p is the number of input variables</span></b> in the feature space.
>
>>[!example] So given 2 input variable our hyperplane is a 1 dimension line which split the data

Unlike the maximal margin classifier, SVCs are able to <b><span style='color: #FFD700'>solve problems when the classes are linear inseparable</span></b> by using what is known as the <b><span style='color: #87CEEB'>soft margin</span></b>.

>[!abstract] Soft margin
> Essentially is the hyperplane where we <b><span style='color: #FFD700'>allow some observations to be on the incorrect side of the margin / hyperplane</span></b>.
> 
> But now our support vectors are the <b><span style='color: #FFD700'>closest point from this best margin / separator from all the classes that is correctly classified</span></b>.

We can **relax the constraints** of the hard margin to be a **soft margin**:
$$
y[i] (b + x[i]) \ge M \times (1 - \epsilon_{i})
$$
Where:
- $\epsilon_{i}$ is a <b><span style='color: #87CEEB'>non-negative slack variable</span></b> (*for a particular datapoint, so we will have n of these*)
	- If $\epsilon_{i} = 0$ then the **i-th observation** is on the <b><span style='color: #98FB98'>correct side of the margin</span></b>
	- If $\epsilon_{i} \gt 0$ then the **i-th observation** is on the incorrect side of the margin, namely it <b><span style='color: var(--mk-color-red)'>violated the margin</span></b>
	- If $\epsilon_{i} \gt 1$ then the **i-th observation** is on the incorrect side of the decision boundary, namely it <b><span style='color: var(--mk-color-red)'>has been misclassified</span></b>

So putting it all together:
![[SVM Example.png|center|500]]

So to **tell how much the model can misclassify** we will <b><span style='color: #FFD700'>impose a non-negative constraint</span></b> on the amount of margin that can be violated by the training observations, it is in the form of this inequality:
$$
\epsilon_{i} + \dots + \epsilon_{n} \le D
$$
Where:
- $n$ is the total number of data points in your dataset
- For $D$:
	- If $D = 0$ then there is <b><span style='color: #FFD700'>no room for violations</span></b>
	- If $D \gt 0$ then <b><span style='color: #FFD700'>no more than D observation</span></b> can be on the wrong side of the decision boundary.

>[!note] Relationship between $D$ & the margin
>As **D increases**, we become more tolerant of violations to the margin and so the <b><span style='color: #FFD700'>margin will widen</span></b>. This also results in <b><span style='color: var(--mk-color-red)'>bias bring higher</span></b> but <b><span style='color: #98FB98'>variance being lower</span></b>. Then we will have <b><span style='color: #98FB98'>more support vectors which our hyperplane will support more on making it more stable</span></b>.
>
>Conversely, as **D decreases**, we become less tolerant of violations to the margin and so the <b><span style='color: #FFD700'>margin will narrow</span></b>.
## Finding The Soft Margin

It almost similar to how we [[Year 3/Sem 2/DSA3362 - Predictive Data Analytics/Support Vector Machines.md#Mathematical Formulation|solve for the maximal margin]]. We are **maximising** $M$ subjected to these conditions:
$$
y[i] (b + x[i]) \ge M \times (1 - \epsilon_{i})
$$

And the following as well:
- $\epsilon_{i} \ge 0$
- $\epsilon_{i} + \dots + \epsilon_{n} \le D$

Which we can rewrite again into this inequality:
$$
y[i] (b + x[i]) \ge M(1 - \epsilon_{i}) = y[i] (\frac{b}{M} + (\frac{1}{M})x[i]) \ge 1 - \epsilon_{i}
$$
Let:
- $\beta_{0}$ to be $b / M$
- $\beta_{1}$ to be $1 / M$ which can be converted into $M = 1 / \beta_{1}$

So now to **maximise** $M = 1 / \beta{1}$ is the same as <b><span style='color: #FFD700'>minimising</span></b> $\color{#FFD700}{\beta_{1} \gt 0}$ (*cannot be 0 is not is a division by 0 problem*) or minimising $\color{#FFD700}{1/2 \beta_{1}^{2}}$.

Now conveniently we can **drop this constraint** $\epsilon_{i} + \dots + \epsilon_{n} \le D$ but <b><span style='color: #FFD700'>add a penalty term</span></b> which we will now me minimising $\color{#FFD700}{1/2 \beta_{1}^{2}} + C \times (\epsilon_{1} + \dots + \epsilon{n})$, subjected to:
- $\epsilon_{i} \ge 0$
- $y[i](\beta_{0} + \beta_{1}x[i]) \ge 1 - \epsilon_{i}$

Here $C$ is known as <b><span style='color: #87CEEB'>cost</span></b> which is a <b><span style='color: #FFD700'>non-negative tuning parameter</span></b>.

>[!note] Relationship between $C$ & the margin
>As **C decreases**, we become more tolerant of violations to the margin and so the <b><span style='color: #FFD700'>margin will widen</span></b>.
>
>Conversely, as **C increases**, we become less tolerant of violations to the margin and so the <b><span style='color: #FFD700'>margin will narrow</span></b>.

>[!important] So as C increases, the model tends to have higher variance  & vice versa.

Now this is now a [[Year 2/Sem 1/CS2109S - Introduction to AI & Machine Learning/Support Vector Machines.md#Lagrange Function|convex optimisation problem]] which can be solved using <b><span style='color: #FFD700'>quadratic programming with Lagrange multipliers</span></b> (*same as before*). But the chosen **hyper parameter C** will <b><span style='color: #FFD700'>determine which support vectors are obtained</span></b>.

# Support Vector Machines In R
---
## Maximal Margin Classifier

To **fit a maximal margin classifier** we can use the `svm()` function.

>[!info] We need the `e1071` package

```R
svm_model <- svm(formula = y_col ~ ., data = df, scale = FALSE, kernel = "linear")
```

Where:
- `scale` is a logical vector indicating whether the variables will be scaled
- `kernal` the one used in fitting & predicting
- `cost` if not specified the value will be 1 by default

>[!info] By default the variables are scaled with to have 0 mean & unit variance

Then you can use the `pred` & `confusionMatrix` function to evaluate the maximal margin classifier from the [[Year 3/Sem 2/DSA3362 - Predictive Data Analytics/Introduction to Caret.md|Caret package]].
## Support Vector Classifier

To **fit a support vector classifier** we can use the same function `svm()`:

```R
svm_model <- svm(formula = y_col ~ ., 
	data = df,
	scale = FALSE,
	kernel = "linear",
	cost = 1
)
```
Where:
- `cost` is $C$ which is our tuning parameter

We can do this as well using the function `train()` in the <b><span style='color: #DDA0DD'>caret</span></b> package:

```R
svm_model <- train(form = y ~ .,
	data = df2 ,
	method = "svmLinear2", # This uses the linear kernal, use svmRadial for the radial kernel (non-linear decision boundaries)
	scale = FALSE, # To scale the data or not
	metric = "Accuracy", # Can be kappa, ROC
	trControl = trainControl (method = "cv", number = 5)
)

svm_model # To display the information about the model
```

The parameters are the same as using the `svm` function.
## Obtaining Key Components From SVM Models

With our trained model, if we used the `svm` function, we can get some **key components of the model**.
- To **get the support vectors**, we can use `svm_model$index` which gives us the index of the support vectors in the data frame (*multiple ones for SVM models*)
- To **get the x values of the support vector** use `svm_model$SV`
- To **get the values of the non-zero Lagrange multipliers** use `svm_model$coefs`
	- For this we usually <b><span style='color: #FFD700'>take the absolute</span></b> values & compare them with $C$ our cost parameter
- To get the **best value of beta 0**, use `svm_model$rho`

With the indexes & the Lagrange multipliers you can then compute $\hat{\beta_{0}}$ & $\hat{\beta_{1}}$ then you can compute $\hat{M}$ & $\hat{b}$.

>[!important] For a SVM problem there might be additional values
>For a **SVM problem**, <b><span style='color: #FFD700'>take the Lagrange multipliers that does not violate the margin</span></b> (*smaller than C*).

But using the `train` function we can get a few things about the model:
- To get the **final best model** (*with cost & number of support vectors*) after CV use `svm_model$finalModel`
- To get the **results from multiple cost value** (*trying different cost values*) use `svm_model$results`
