---
Title: Introduction to Caret
Date Created: 14-January-2026
Last Updated: 23-April-2026
Tags:
  - DSA3362
  - ProgrammingLanguage/R/caret
---
# Caret
---
Caret (*Classification And REgression Training*) is strong package in R which provides simple functions to do:
- **Data splitting**
- **Data visualisation**
- **Feature selection**
- **Model tuning**
- **Variable important estimation**
- And many more

>[!info] To use it import the following library `library(caret)`.
## Visualisation

Caret provides a simple way to plot certain graphs which is `featurePlot`

**Sample usage**:
```R
featurePlot(
	x = df[,4:5], # The input variables
	y = df$default, # The output variable
	plot = "boxplot", # "pair", "ellipse", "density, "scatter". Only these 5 are supported
	auto.key = list(columns = 2), # legend
	scales = list( # This is to scale the x and y axis ranges
		x = list(relation = "free"),
		y = list(relation = "free")
	),
	layout = c(2,1),
	adjust = 1.5
)
```

>[!info] The density plot is good to figure out which variables are good in predicting
>For classification problems, if it overlaps then it is not a good variable to use since it cannot differentiate the Y value.

You can also **display certain data that you want on a table**:

```R
data.frame(col1 = c("row1 data for col 1", "row1 data for col 1"),
           col2 = c("row1 data for col 2", "row1 data for col 2") %>% kable()
# You do not need to pass into the kable function, you can just print the dataframe. But if you do use kable, import the kableExtra library.
```
## Data Aggregation

Though caret does not provide functions to do provide a summary of the data, there is another library called `tableone` which <b><span style='color: #FFD700'>creates a summary table</span></b> similarly to how the `summary` function works.

>[!info] To use it import the following library `library(tableone)` & `library(kableExtra)`

Firstly we need to **create the table**, we can do this by calling the `CreateTableOne` function.

**Example of using the `CreateTableOne` function**:
```R
y_col_name <- "default" 
x_col_names <- setdiff(names(df1), y_col_name) # Names gets the column names while set difference removes elements with the same value between the 2

tab1 <- CreateTableOne(
	vars = x_col_names, # vars is for the input variable col names
	strata = y_col_name, # strata is for the output variable name (if don't have no need to put)
	data = df, # The data source
	addOverall = TRUE # Adds an addiitonal column to the table to show all the data as 1
)
```

Next we need to **display the table**, we can do so by using the `kableone` function.

**Example of using the `kableone` function**:
```R
kableone(
	tab1,
	contDigits = 1,
	nonnormal = "balance" # Columns which have imbalanced output variable distributions
)
```

>[!question] What does nonnormal argument do?
> It is possible that for classification problems <b><span style='color: var(--mk-color-red)'>a input variable might have imbalanced distribution</span></b> with respect to the output variable.
> 
> So statistics like mean, standard deviation can be biased. Thus when indicating columns what are non normal, it will <b><span style='color: #FFD700'>use statistics like median and IQR</span></b>.
## Splitting the Data

Typically we will take <b><span style='color: #FFD700'>70 to 80% of the data as our training set</span></b> while the rest will be used for testing.

However we need to <b><span style='color: #FFD700'>pay attention to the proportion of the data</span></b>. We can do so with the following code:
```R
table(df$y_col) %>% proportions() %>% round(3)

summary(df$Purchase) %>% proportions() %>% round(4) # You can do this as well
```

When splitting the data we will want to <b><span style='color: #FFD700'>keep the proportion similar between test & train</span></b>. Caret does provide one function called `createDataPartition`.

**Example of using the `createDataPartition` function**:
```R
set.seed(987)
intrain <- createDataPartition( # This just return a list of indexes
	df$default, # The output variable column
	p = 0.8, # partition % of the data
	list = FALSE
)
training <- df[intrain, ] # Split the data using the partitioned indexes
testing <- df[-intrain, ]
```

>[!note] Note that `createDataPartition` has randomness
>It <b><span style='color: #FFD700'>does stratified sampling</span></b>. Use `set.seed()` to ensure results remain the same every time you run the code.
## Building a Model

Caret provides a simple function `train` which can <b><span style='color: #FFD700'>build multiple different types of models</span></b>:
- `lm`
- `glm` (*general linear models*), need to indicate family argument `binominal` or `poisson` (*for multi class*)
- `knn`
- `svm`
- and many more

**Example of using the `train` function**:
```R
set.seed(987)
ctl <- trainControl(method = "cv", number = 10) # CV is cross validation and number is the no of folds
met <- "Accuracy" # Regression use RSME or Rsquared, for classcification use Accuracy or Kappa

fit.glm <- train(default ~ . -X, # Transformed features use I, e.g. I(x1^2)
	data = training,
	method = "glm", # Model type
	family = "binomial", # Because we are making a log reg model
	preProcess = c("center", "scale"), # This is to scale the values used
	metric = met,
	trControl = ctl # To control how the model is optimised
)
```

>[!important] Metric is used to select the best model out of all the cross validated methods

>[!note] Note that `trainControl` and using the method `cv` has randomness
>So use `set.seed()` to ensure results remain the same every time you run the code.
## Evaluating the Model

For a **regression model** we can use the functions inside the <b><span style='color: #DDA0DD'>Metrics</span></b> library.

>[!info] You will need to import the `Metrics` library

```R
mse(actual, prediction) # Mean square error
rmse(actual, prediction) # Root mean square error
mae(actual, prediction) # Root absolute error
# There is also mape
```

We can use the normal `summary` function which R provides, but **for classification models** Caret provides a `confusionMatrix` function.

**Example of using the `confusionMatrix` function**:
```R
# Get our predictions
pred.glm <- predict(fit.glm, newdata = testing)
# Note: For log reg, you can add type = "response" to get the probability instead of log odds

confusionMatrix(
	data = pred.glm, # Our models predictions
	reference = testing$default, # The correct labels to compare
	positive = "Yes", # Change the positive label / class
	mode = "everything" # Include all matrices
)
```

The output will contain some additional matrices:
- **No information rate** (*NIR*): Which tells us the <b><span style='color: #FFD700'>probability to get the prediction correct if we always predict the majority class</span></b> (*We want our accuracy to be higher than this*).
- **P-Value \[Acc > NIR\]**: A **high value** means that accuracy is higher than NIR meaning we can <b><span style='color: #FFD700'>reject H0 or the null hypothesis</span></b> and this means that the model is reasonable
- **Kappa**: The closer to <b><span style='color: var(--mk-color-red)'>0 or lower it is just as good or worse than just doing random guessing</span></b>
- **Sensitivity**: Also known as [[Year 3/Sem 2/DSA3362 - Predictive Data Analytics/Supervised Learning.md#For Classification Model|recall]] which tells us <b><span style='color: #FFD700'>how accurate the model is in predicting the positive class</span></b>
- **Specificity**: Also known as [[Year 3/Sem 2/DSA3362 - Predictive Data Analytics/Supervised Learning.md#For Classification Model|TNR]] which tells us <b><span style='color: #FFD700'>how accurate the model is in predicting the negative class</span></b>
- **Balanced accuracy**: Which is the average of sensitivity & specificity. It <b><span style='color: #98FB98'>gives a more balanced outlook</span></b> since there can be an imbalanced in the majority group

>[!info] Formula to compute the Kappa score
>$$
\frac{\text{Probability observed} - \text{Probability expected}}{1 - \text{Probability expected}}
> $$
> Where:
> - Observed probability are the **probability of predictions that are predicted correctly**
> - Expected probability is the **probability of the positive class** times the **probability of prediction of the positive class** plus the **probability negative class** times the **probability of prediction of the negative class**

>[!important] High accuracy does not always mean the model is good
>Due to data disproportion, it might be good at <b><span style='color: var(--mk-color-red)'>predicting the majority class but not for the minority class</span></b>.

If we have <b><span style='color: #FFD700'>multiple models</span></b> & we want to <b><span style='color: #FFD700'>compare</span></b> them we can use the `resamples` function:
```R
# Is from the caret package you can omit the caret:: if there is no conflict
# Just add the models you built into the list
results <- caret::resamples(list(logreg = glm.fit, knn = knn.fit))
summary(results)
```

With the results you can also plot a dot plot using the `dotplot` function
```R
dotplot(results)
```

**Sample dot plot graph**:
![[Dot Plot Graph Example.png|center]]

The <b><span style='color: #98FB98'>better the model the more to the right the dots should be</span></b>.

We can also use a function `binom.text(x, n, p, alternative = "greater")` to **compute the p-value** for classification problems.

Where:
- `x` is the number of correct predications
- `n` is the total number of predictions
- `p` is the probability of a data point being in the majority class
## Getting the Important Variables

Caret provides a function to get the <b><span style='color: #FFD700'>t-statistics of each variable</span></b> through the `varImp` function (*for this course use this*). These values are the <b><span style='color: #FFD700'>absolute values of the z-value</span></b> found when doing `summary`.

>[!question] What is the t-statistics?
> It is also known as the t-score, which indicates <b><span style='color: #FFD700'>how many standard errors</span></b> the sample mean is away from the population mean.
> 
> The larger the value suggests that the observed difference is not due to random chance.

**Example of using the ``varImp`` function**:
```R
imp.var <- varImp(model, scale = FALSE)
```

>[!warning] If the model is not compatible with the `varImp` function then we have to use `vip`
>```R
>vip(model, geom = "col") + theme_classic()
>```

There is also a `filterVarImp` function to get the most important features (*variables*) as well:
```R
filterVarImp(x = df[,c_cols], y = df$y_col) %>% arrange(desc(Overall))
```

This will <b><span style='color: #FFD700'>arrange the variables from most important to least</span></b>. Then to select the variables you want, use the `select` function
```R
df <- df %>% select(x_col_1, x_col_2, y_col) # Add more cols based on the problem
```

>[!question] How to compute variable importance?
>![[How to Compute Importance.png|center]]