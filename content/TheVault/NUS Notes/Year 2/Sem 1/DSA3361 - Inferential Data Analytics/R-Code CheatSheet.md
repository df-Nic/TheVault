---
title: R-Code CheatSheet
Date Created: 2024-11-19
Last Updated: 2025-09-28
tags:
  - DSA3361
  - R
---
# Packages Used Before
---
```R
library(tidyverse) # ggplot2
library(magrittr) # pipping
library(tinytex) # knit to pdf
library(readxl) # read excel files
library(ggplot2)
library(Hmisc) # impute()
library(dplyr)
library(stats) # lm models
library(eeptools) # To calculate age
library(lubridate) # Convert char to date time
library(e1071) # for skewness
library(caret) # For partiton function
library(skimr) #skim()
library(car) # data sets from car and the vif function
library(broom) # augment() for Cook's Distance
library(pROC) # for ROC plots
library(MASS) # for step AIC
library(sampling)
library(VGAM) # for vglm()
library(nnet) # multinom()
library(DescTools)
library(glmnet) # Ridge and Lasso
library(leaps) # regsubsets() for best subset
library(kableExtra) # kable() to present large table neatly
library(lubridate)
library(rstatix)
library(stringr)

# Extension to ggplot
library(ggridges)
library(GGally) # ggpairs()
library(ggpubr)
library(corrplot) # for correlation matrix
library(plotrix)
library(plotmo)

# Datasets
library(nycflights13) # data sets for flights and planes
library(resampledata) # data sets from Chihara and Hesterberg's book
library(tree) # data sets from Chihara and Hesterberg's book
```
# Shortcuts
---
`ctrl + shift + I` will <span style='color:var(--mk-color-yellow)'>input a new code</span> block in <span style='color:var(--mk-color-purple)'>R</span>.

`alt + -` will input the `<-`.

`ctrl + shift + M` will input the `%<%`. Which is a <span style='color:var(--mk-color-yellow)'>symbol for input</span>
# Basic Commands
---
## Import Dataset

We can import both <span style='color:var(--mk-color-purple)'>csv</span> or **any excel file format**. We will need the `readxl` library for this.
```R
library(readxl)

# This only works for .CSV files
df <- read.csv("Data/superstore.csv", stringsAsFactors = TRUE)

# For any other general excel file type like xls
df <- read_excel("<file path>/<file name>.<file type>")

# If you want to import a dataset on R
data("<Data set name>") # Like trees or mtcars
```

> Note that `stringAsFactors` is a **hyperparameter** for the `read.csv` function only and its <span style='color:var(--mk-color-red)'>default is false</span>. It will <span style='color:var(--mk-color-yellow)'>convert all categorical variables</span> (*non-integers*) <span style='color:var(--mk-color-yellow)'>into factors</span>.
### Functions to View the Dataset

There are some **useful functions** which can be used to <span style='color:var(--mk-color-yellow)'>understand the data we just imported</span>.
```R
head(df, n = 5) # View the first 5 rows in the dataset
tail(df) # Same as head but from the back, note that default n = 6
str(df)  # Shows the data types of each column
names(df) # Shows the column names in the dataset
count(df) # Get the number of rows in the dataset or nrow(df)
ncol(df) # Get the number of columns in the dataset
summary(df) # Get basic statistics of the data
sum(is.na(df)) # Count number of na values
sum(duplicated(df)) # Number of duplicates
var(model) # Variance, if you want bias is the average of (actual - predicted)

# Cosmetic
options(scipen=999) # Do not show scientific notation

# Sequence
x <- 10^seq(-6, 2, length = 100) # seq makes a sequence from -6 to 2 with 100 intervals

# Calculate DOB
df$age <- as.period(interval(start=df$birth_date, end=Sys.Date()))
```
## `select()` - Select Columns

Take some <span style='color:var(--mk-color-yellow)'>subset of columns</span> from the dataset by using `select`.
```R
df_subset <- df %>% select(<col name>, <col name>, ...) # Column names don't need to be in ""
# Can also sclise using [] like in python
df_subset <- df[,1:2] # This means take the 1st and 2nd column and all the rows, 
```

If there is some <span style='color:var(--mk-color-red)'>error</span> saying <span style='color:var(--mk-color-orange)'>unused argument</span>, try using `dplyr::select()`.
## `filter()` - Filter Rows

We can <span style='color:var(--mk-color-yellow)'>filter out rows</span> based on certain conditions.
```R
df_filtered <- df %>% filter(<col name> == <condition>, <col name> == <condition>)
```

Here are the <span style='color:var(--mk-color-orange)'>supported operations</span>:
- $\gt$, $\lt$, $\ge$, $\le$
- ==
- ! - <span style='color:var(--mk-color-red)'>Not</span>

For **multiple conditions**, if like in the above example it has a `,` then in <span style='color:var(--mk-color-purple)'>R</span> it will be an <span style='color:var(--mk-color-yellow)'>AND operator</span> (*or can use &*) for an <span style='color:var(--mk-color-yellow)'>OR operation</span> use the `|` symbol.

We can also use a list `c(<items>)` and we will use the operation `%in%` instead.
## `mutate()` - Augment Columns or Add New Columns

We can <span style='color:var(--mk-color-yellow)'>transform data</span> into an **existing column or a new one** using the `mutate` function.

```R
df_mutated <- df %>% mutate(<col name> = <Assignment>)
# Example if you want profit then in the () put Profit = Sales - Cost
df_mutated <- df %>% mutate(<col name> = case_when(
    <col name> == 1 ~ "Something 1",
    <col name> == 2 ~ "Something 2")) # Add more if needed
# If we want to rename values based on past values
```
## `arrange()` - Rearrange the Dataset

We can <span style='color:var(--mk-color-yellow)'>sort the rows</span> using the `arrange()` function. But if you want to <span style='color:var(--mk-color-yellow)'>move columns</span> use the `relocate` function.
```R
# Sort Columns
df_arrange <- df %>% arrange(desc(<col name>))

# Rearrange columns
df %>% relocate(<col name 1>, .before = <col name 2>) # You can use .after also
```
## `group_by()` - Grouping Data

We can also <span style='color:var(--mk-color-yellow)'>group all rows</span> with the same value of a particular column using the `group_by` function. This is also paired with the `summary` function.
```R
df_grouped <- df %>% group_by(<col name>) %>%
	summarise(<new col> = <statistic>, ...)
```

For `summarise`, here are some **functions** which can be used to give a <span style='color:var(--mk-color-yellow)'>summary of the individual groups</span>:
- `mean()`
- `median()`
- `mode()`
- `sd()`
- `n()` - The count of a particular group
- `IQR()`
##  `inner_join()` - Joining 2 Datasets

Just like in a database we can **combine 2 datasets into 1** if, the <span style='color:var(--mk-color-yellow)'>number of rows is the same</span> and there is a <span style='color:var(--mk-color-yellow)'>common column</span>.
```R
df_join <- inner_join(df1, df2, by = c("<column name>" = "<column name>"))
```
## `impute()` - Replace Null Values

We can <span style='color:var(--mk-color-yellow)'>replace null values</span> in the dataset with the `impute` function.
```R
df$<col name> <- impute(df$<same col name>, fun = <what to replace by>)
```
We can replace with many different statistics such as:
- `mode`
- `mean`
## `replicate()` - Do Something Multiple Times

We can **execute a function** or create an array with some value $x$ time using the `replicate` function.
```R
fn <- function(input1) {} # Assume this does something
result <- replicate(n = 1000, fn(<variable input>)) # Repreat the function 1000 times
# Result will be an array of size 1000 based on the output of the function
```
## Categorise Data

If when imparting the dataset and `StringsAsFactors = TRUE`, then we do not need to do this since **R does it for you**.  But if you want <span style='color:var(--mk-color-yellow)'>your own categories</span> you can use either `ifelse` or `recode` (*need the dplyr library*).

```R
# For binary categories
df <- df %>% mutate(<col name> = ifelse(<col name> <condition>, "<value if true>", "<value if false>"))

# For many categories
df$<col name> <- recode(df$<col name>,
	"0" = "Single",
	"1" = "Married",
	"2" = "Separated",
	"3" = "Divorced",
	"4" = "Widowed")
# This is just an example where the LHS is the values in the original dataset

# If you want to refactor the values do this
factor(df$<variable>, level = c("value1", "value2", "value3")) # This will follow 1, 2 ,3, ...
```
## Functions

In <span style='color:var(--mk-color-purple)'>R</span> we can <span style='color:var(--mk-color-orange)'>create functions</span> as such
```R
fn_name <- function(input1, input2, ...) {
	# What does the function do
	return <Something>
}
```

# Computing Statistics
---
## Confidence Interval
The formula to <span style='color:var(--mk-color-orange)'>calculate margin of error</span> is:
$$
\text{Margin of Error} = Z_{\text{Confidence interval}} \times \frac{\sigma}{\sqrt{n}}
$$
```R
# Example to compute a 90% confidence interval
n <- length (X) # Get the number of entries, this is when X is not a dataframe but a matrix/list
lower_limit <- mean (X) + qnorm (0.05)* sd(X)/ sqrt (n) # 0.05 to take away the 2 ends of the curve
upper_limit <- mean (X) - qnorm (0.05)* sd(X)/ sqrt (n)

# sd(X)/ sqrt (n), this is called standard error

# If we used the t.test() function we can also get the confidence interval by
variable_name$conf.int
```
## Critical Value

This value will be used to <span style='color:var(--mk-color-yellow)'>calculate the confidence interval</span>.
```R
# Assume a 95% confidence interval, then because of its 2 tail, we need to divide 5% by 2
qt(0.975 ,df = <Degree of freedom>)
```

## Test Statistic & P-Value

We can **calculate the test statistic and p-value** against 2 variables
```R
# Doing a 2 sample t-test is for 2 variables only
t.test(outcome~treatment , alternative = "two.sided", paired = FALSE,
		var.equal=TRUE, data = df)

# Another way of calculating P-value (If we doing permutation test)
# This is 1 tail, most of the time the question will want 2 tail to just times 2
pvalue <- mean(abs(<permutation samples>) >= abs(<orginal test statistic>))

# 1-Tail P-value
(sum(result >= obs) + 1) / (N + 1) # +1 because in the event of 0/N+1
# 2-Tail P-Value, which is more accurate
2*((sum(result >= obs) + 1) / (N + 1))
```
For `alternative` being `two.sided` means the it is a <span style='color:var(--mk-color-yellow)'>2 tailed p-value</span> and not one. `paired` and `var.equal` is true, if the data <span style='color:var(--mk-color-yellow)'>is independent</span>.
## General Statistics

```R
mse <- mean((actual-predicted )^2) # Mean squared error (MSE)
mae <- mean(abs(actual - predicted)) # Mean absolute error (MAE) 
rmse <- sqrt(mse_data) # Root mean square error (RMSE) 
mape <- mean(abs((actual - predicted)/actual))*100 # Mean absolute percentage error (MAPE)

variance <- var(model)

# For R square
RSS <- sum((predict - actual)^2)
TSS <- sum((actual - mean(actual))^2)
R_square <- 1 - (RSS / TSS)

# Or use MSE(pred, true), same for MAE, RMSE, MAPE, R2 also
```
# Sampling
---
## Taking a Random Sample

We can choose to take a sample <span style='color:var(--mk-color-yellow)'>with or without replacement</span>.
```R
population_data <- c(1,2,3,4,5,6,7) # Creates a list/1D matrix
# To take 1 sample with no replacement
samp <- sample(x = population_data, size = <How big is the sample>, replace = FALSE)

# With replacement
samp <- sample(x = population_data, size = <How big is the sample>, replace = TRUE)
```
## Permutation Testing

We can **do permutation testing** by using <span style='color:var(--mk-color-turquoise)'>permutation sampling</span>.

**Permutation Sampling**
```R
set.seed(123) # Depends on the question
N <- 1000 # Depends on the question (Number of samples)
perm_sample_mean <- rep(0, N) # Creates a list of size with all values to be 0

test_statistic <- mean(<group A>) - mean(<group B>) # See the question

outcome <- df$y_variable # Usually is the Y column
groups <- df$groups # Get the group column

for (i in 1:N){
	perm <- sample(groups, size = nrow(df), replace = FALSE)
	# The test statistic calculated below is based on the question
	perm_sample_mean[i] <- mean(outcome[perm == <group A>]) - mean(outcome[perm == <group B>])
}
```
## Bootstrap Sampling

We can <span style='color:var(--mk-color-orange)'>carry out bootstrap sampling</span> as follows:
```R
var <- df$<variable>
n <- length(var)
N <- 10ˆ4 # How many times to sample
weight.boot <- numeric(N) # Store the results from the bootstrapping
for (i in 1:N) {
	samp <- sample(var, size = n, replace = TRUE) # draw resample
	weight.boot[i] <- mean(samp) # compute mean and store it (Can be another matrix also)
}

# We can also get the bootstrap confidence interval of the true mean
quantile(weight.boot, c(0.025,0.975)) # 95% confidence interval
```
# Data Analysis
---
## Check Skewedness

We can check how <span style='color:var(--mk-color-yellow)'>distributed a specific variable</span> is in a dataset.
```R
library(e1071) # For the swedness function
skewness(df$<column name>)
```

1) Between **-0.5 and 0.5**, the distribution is approximately <span style='color:var(--mk-color-yellow)'>symmetric</span>
2) Between **-0.5 and -1** or **0.5 and 1**, the distribution is <span style='color:var(--mk-color-yellow)'>moderately skewed</span>
3) Beyond **-1 or 1**, the distribution is <span style='color:var(--mk-color-yellow)'>highly skewed</span>
## Checking Corelation

We can check the r**relationship between 2 variables** which <b><mark style='background:var(--mk-color-yellow)'>must be numeric</mark></b>. If they <span style='color:var(--mk-color-orange)'>want magnitude</span>, then take the <span style='color:var(--mk-color-yellow)'>absolute value of the corelation</span>.
```R
library(stats) # For the cor function
cor (df$<col one>, df$<col two>, use="complete.obs") # The use is in case of NA values

# You can also do it for multiple numerical variables instead of just 2
cor(df[, 1:3]) # Change 1 and 3 with the actual columns you want to use
# Can also use c(<numbers>)

# For 2 categorical variables (Y and X are 2 categorical variables, ususally log regression)
chisq.test(df$<var>, df$<var>) # 0.05 and below is significant
```

**If the value of `cor` is**:
1) Between **-1 and -0.7** or **0.7 and 1**, the corelation is <span style='color:var(--mk-color-green)'>strong</span>
2) Between **-0.7 and -0.3** or **0.3 and 0.7**, the corelation is <span style='color:var(--mk-color-orange)'>moderate</span>
3) Between **-0.3 and -0.0** or **0 and 0.3**, the corelation is <span style='color:var(--mk-color-red)'>weak</span>
## Finding Influential Points

Here we are<span style='color:var(--mk-color-orange)'> finding influential points</span> which are a **special group of outliers**, using <span style='color:var(--mk-color-blue)'>cooks distance</span>.
```R
cooksD <- cooks.distance(model) # Get cooks distance for all points
# Find those that exceed the threshold
influential <- cooksD [(cooksD > (3 * mean(cooksD, na.rm = TRUE)))]
```

General rule of thumb to <span style='color:var(--mk-color-orange)'>identify these points</span> (*influential points*):
- A Cook’s Distance of more than <span style='color:var(--mk-color-yellow)'>3 times the mean</span> (μ).
- Alternatively a Cook’s Distance of <span style='color:var(--mk-color-yellow)'>more than 4/n</span>, where **n is the number of observations**.
- Others suggests that Cook’s distance value of <span style='color:var(--mk-color-yellow)'>more 1 indicates an influential point</span>, and those **above 0.5** should be investigated.
## Model Building
---
## Partitioning into Train & Test

We can **partition the data** into training and validation/testing dataset using either `sample` or `createDataPartition` function.
```R
set.seed (10) # Ensure same results when running again
partition <- sort(sample(data = nrow(df), size = row(df)*.8))
train <- df. advert [partition ,]
test <- df. advert [-partition ,] # This - is every number thats not in partition

library(caret) # For partiton function
partition <- createDataPartition(df$<response variable>, p = .8,
								  list = FALSE, times = 1)
# Then we can use partition the same as before

data <- na.omit(data) # If we need to remove NA values
data <- unique(data) # If we need to remove duplicate rows
```
## Building a Linear Regression Model

With the `stats` library we can build a <span style='color:var(--mk-color-blue)'>linear regression model</span> as such using the `lm` function:
```R
model <- lm(Y ~ X1 + X2 + ... , train_df)
# Get residuals or predicted values
train_predicted <- resid(model) # To get the predited values on the training dataset
summary(model) # To see the goodness of the model
```

For categorical variables, the <span style='color:var(--mk-color-yellow)'>reference will be based of the factor number 1</span>, thus if you want to change the reference using `factor`. Or you can use `relevel(df$<column>, ref = "<Value you want it to be a reference of>")`

When <span style='color:var(--mk-color-orange)'>choosing the variables</span>:
- If you want to **use every single variable** then do `Y ~ .`
- If you want to <span style='color:var(--mk-color-red)'>not use a variable</span> then do `Y ~ . - variable1`
- To <span style='color:var(--mk-color-green)'>add a variable</span> do `Y ~ variable1 + variable2`
- For an <span style='color:var(--mk-color-yellow)'>interaction term</span> do `Y ~ variable1 * variable2`
- For a higher polynomial variable do `Y ~ I(<variable1>^i`, where $i$ is the degree of the polynomial.

>For **categorical variables**, if there is a <span style='color:var(--mk-color-yellow)'>need to change focus</span> use `df$<col> <- relevel(df$<col>, ref = "<value>")`.
### Confidence Interval for Coefficients

We can get the **confidence interval for all coefficients** in the model to <span style='color:var(--mk-color-yellow)'>determine the accuracy of the model</span>.
```R
# For a 95% confidence interval
confint(model, level =0.95)
```

Thus if we get a **smaller interval**, it means that the <span style='color:var(--mk-color-green)'>model has a more accurate coefficient estimate</span>.
### Confidence & Prediction Interval of the Y Variable

```ad-summary
title: What is the difference
collapse: open

When calculating <b><span style='color:var(--mk-color-blue)'>confidence intervals</span></b> using **prediction values**. This means that 95/100 samples, their true values (Y) will fall within this range.

When calculating <b><span style='color:var(--mk-color-blue)'>prediction intervals</span></b> using **prediction values**. This means that 95/100 predictions will fall within this range. And this range is ususally bigger than CI (*Single point*).
```

```R
new_data <- data.frame(<X variable> = <value>, <X variavle> = ...)
predict(model, new_data, interval = "prediction") # Prediction interval, and normal predictions (fit)
predict(model, new_data, interval = "confidence") # Confidence interval
```
### Detecting Multicollinearity

We need to **check if all variables used** <span style='color:var(--mk-color-red)'>have some corelation with one another</span> before fitting a linear model.
```R
library(car) # For the vif function
model <- lm(Y ~ ., data = train) # Fit a model first
vif(model)
```

Using the `vif` function from the <span style='color:var(--mk-color-purple)'>car R package</span> to get the value:
- If the **value is 1** it means the <span style='color:var(--mk-color-green)'>variable is uncorrelated</span> to all other variables
- If the **value is above 5** then there is <span style='color:var(--mk-color-red)'>high multicolinearity</span>
### Anova F-Test

We can also do a <span style='color:var(--mk-color-yellow)'>f-test on the model </span>using the `anova` function
```R
anova(model,<model2>) # Model 2 if you need to do a partial f-test.
# If p-value < 0.05 and f value is larger than 1, then the model 2 is better
fstatistic <- (<sum of coefficients>) / <num of variables>) / <Residual MSE> # All from anova
f.pvalue <- pf(fstatistic, df1 = <number of variables>, df2 = <df of residuals>, lower.tail = FALSE))
```

![[Anova Example.png|center]]
## Building a Logistic Regression Model

It is similar to building a [[#Building a Linear Regression Model|linear regression model]], but instead we will need to use `glm` instead (*for binary classification*).
```R
model <- glm(Y ~ X1 + X2 + ...,
			data = train,
			family = binomial)
summary(model) # The model will show us log odds and not odds

fitted(model) # This is to get the fitted models on the training dataset
model$fitted.values # Also works the same as the above
```

> It is important that `family` <b><mark style='background:var(--mk-color-yellow)'>must be binomial</mark></b>.

If we have <span style='color:var(--mk-color-orange)'>more than 2 classes</span> when we have to use the `vglm` function instead and set a reference
```R
ml <- vglm(y ~ x1 + x2 + ..., family = multinomial(refLevel = "<Category Name>"),
			data = data)
# Check the factor number assigned to the value
levels(factor(df$<variable>))
# Get the model coefficients
coef(model, matrix = TRUE, ynames = TRUE)

# Get the fitted values and place them in a dataframe
probs <- fitted(model)
# Follow the levels
pd1 <- data %>% select(<variables>) %>% mutate(catrogy_1 = probs[,1], category_2 = probs[,2],...)
# Convert the prediciton to a class (Using the highest one)
pd1 <- pd1 %>% mutate(predicted = colnames(probs)[apply(probs, 1, which.max)])
```

The **reference level is based on the question**.
### Akaike Information Criterion

The <span style='color:var(--mk-color-orange)'>evaluation</span> of a logistic regression model will be done based on the AIC metric which can be retrieved by:
```R
AIC(model) # This will give us the AIC value, the lower the better
```
### Step AIC

Find the best model parameters to get the lowest AIC value
```R
base_model <- glm(chd ~ 1,
				   data = df,
				   family = binomial)
				   
bestfit <- stepAIC(base_model,
					scope = list(upper = ~<Interaction between all variables>,lower = ~1))
# Upper can also depend on the question
```

### Finding the Deviance

The `glm` function has <span style='color:var(--mk-color-orange)'>2 deviances</span>, one is the <span style='color:var(--mk-color-blue)'>null deviance</span> and the other is the <span style='color:var(--mk-color-blue)'>residual deviance</span>.
```R
nullD <- summary(model)$null.deviance # Null deviance
Dm2 <- summary(model)$deviance # Redisual Deviance for the entire training dataset
```

If you want to calculate the **deviance residual of 1 row**, then do, `rediduals(model, type = "deviance")`.
#### Overall Significance Test

We need to <span style='color:var(--mk-color-orange)'>calculate 2 values</span> $D^{2}_{o} - D^{2}$ and $X^{2}_{p, \alpha}$. And this is just like an <span style='color:var(--mk-color-blue)'>F-test</span>.
```R
nullD - Dm2 # The code to get these 2 values are directly above

# To calculate the second value (X term)
qchisq(p = 0.05, df = <based on the model>, lower.tail = FALSE) # P is based on the question
```

For `df` we can **get the values** from the `summary` function by taking <span style='color:var(--mk-color-yellow)'>degrees of freedom from null deviance minus degrees of freedom from residual deviance</span>.

Then we just need to check if $D^{2}_{o} - D^{2} \gt X^{2}_{p, \alpha}$, if <span style='color:var(--mk-color-green)'>yes then we can reject </span>$H_{o}$.
### Predicting with a Logistic Model

Unlike a linear regression model, we need to<span style='color:var(--mk-color-yellow)'> set the type</span> to be `response`
```R
new_data <- data.frame(<X variable> = <value>, <X variavle> = ...)
pred <- predict(model, newdata = new_data, type = "response") # The type is very important

# Convert based on threshold
pred <- pred %>% mutate(y_pred = ifelse(y_prob > <threshold>, "Yes", "No"))
```
### Confusion Matrix

After our predictions we can <span style='color:var(--mk-color-orange)'>generate a confusion matrix</span>:
```R
df$true_value <- factor(df$true_value, levels = c("Yes", "No")) # 0 = Yes, 1 = No change if needed
df$y_pred <- factor(df$y_pred, levels = c("Yes", "No"))

# addmargins() adds a sum column
coefficient_matrix <- table(df$true_value, df$y_pred, deparse.level = 0) %>% addmargins()

# If there are more than 2 class then you can do this
table(actual = df$actual, predict = df$predict)

colnames(coefficient_matrix) <- c("y_pred = Yes", "y_pred = No")
rownames(coefficient_matrix) <- c("true_value = Yes", "true_value = No")

TP <- coefficient_matrix[1,1]
TN <- coefficient_matrix[2,2]
FP <- coefficient_matrix[2,1]
FN <- coefficient_matrix[1,2]
```
#### Calculating Evaluation Matrix

```R
# Following the same naming convention as above
accuracy <- (TP + TN)/nrow(df)
sensitivity <- TP/(TP + FN)
specificity <- TN/(TN + FP)
precision <- (TP)/(TP + FP)
f1 <- (2 * precision * sensitivity)/(precision + sensitivity)

# For multinomial models we can only use the classification rate
mean(df$actual == df$predicted)
```
### Getting Optimal Threshold

This is based on the ROC curve and **which one will give the largest area under the curve**:
```R
library(pROC) # Need this library
y_true <- df$true_y
y_probs <- predict(model, newdata = data, type = "response")
plot.roc(
	y_true,
	y_probs,
	print.auc = TRUE,
	thresholds = "best",
	print.thres = "best"
)
```

This is based on AUC, if you want it based on some other matrix you need to do it another way you can use this for the best AUC also
```R
roc_curve <- roc(response = <y variable>,
				predictor = <model fitted values>,
				plot = TRUE,
				percent = TRUE,
				ci = TRUE,
				legacy.axes = TRUE, # change the x-axis to 1-Specificity
				#xlab = "False Positive Percentage",
				#ylab = "True Positive Percentage",
				print.auc = TRUE,
				print.auc.pattern = "%.2f (%.2f-%.2f)")

# Get a list of thresholds
th <- data.frame(TPR = roc_curve$sensitivities,
				Specificity = roc_curve$specificities,
				FPR = 1 - roc_curve$specificities
				Threshold = roc_curve$thresholds)
	
thresholds <- roc_curve$thresholds

# The example is based on finding the best F1 Score
fn <- function(threshold) { # create a function with the name my_function
	df <- df_past_pred %>% mutate(predict = ifelse(prob > threshold, 1, 0))
	coeff_matrix <- table(df$churn, df$predict, deparse.level = 0)
	TP <- coeff_matrix[2, 2]
	FP <- coeff_matrix[1, 2]
	FN <- coeff_matrix[2, 1]
	f1_score <- TP / (TP + 0.5 * (FP + FN))
	return(f1_score)
}

th$F1_Score <- sapply(th$Threshold, fn)
# Sort the F1 score
th <- th %>% arrange(desc(F1_Score))
```

## Regularised Models

We can **build a ridge, LASSO, or elastic net model** using the following code:
```R
library(glmnet) # Need this library

# glmnet() only accepts matrix
train_x <- model.matrix(Y ~ ., data = train_df)[,-1] # Exclude Y which is ususally at the end
train_y <- train_df[,ncol(train_df)] # Or do train_df$y_variable
test_x <- model.matrix(Y ~ ., data = test_df)[,-1] # Exclude Y
test_y <- test_df[,ncol(test_df)]

model <- glmnet(train_x, train_y, alpha = 0, lambda = L)

# Summary does not work thus we need to use coef function
coef(model) # Get coefficients

# To predict we can do
predict(model, train_x)
```
**Where:**
- `x` is the data matrix of variables (*use* `model.matrix()` in <span style='color:var(--mk-color-purple)'>R</span>)
- `alpha` is the <span style='color:var(--mk-color-turquoise)'>mixing parameter</span> between 0 and 1
	1) **0 is for ridge regression**
	2) **1 is for LASSO regression**
	3) **Strictly between 0 and 1 is for elastic net regression**
- `lambda` is the regularisation parameter which can be a constant value or a sequence of values. The <span style='color:var(--mk-color-orange)'>default</span> will be <span style='color:var(--mk-color-yellow)'>a sequence of values</span> by <span style='color:var(--mk-color-purple)'>R</span>.

There are other parameters as well like, **standardize** which <span style='color:var(--mk-color-yellow)'>by default is true</span>. Also `glmnet` <b><mark style='background:var(--mk-color-red)'>does not allow NA</mark></b> thus we need to remove it using `na.omit()` function in <span style='color:var(--mk-color-purple)'>R</span>.
### Best Lambda

We will use the function `cv.glmnet` to <span style='color:var(--mk-color-orange)'>get the best lambda</span>:
```R
set.seed (123) # Ensure reproducability
model_ridge <- cv.glmnet(train_x, train_y, alpha = 0, type.measure = "mse")
```

>`type.measure` can be "mse", "mae", "rsme" or any other metric.

The above function will <span style='color:var(--mk-color-orange)'>provide 2 values</span>:
1) `model_ridge$lambda.min` - Which is the lambda value at which the <span style='color:var(--mk-color-green)'>lowest MSE is achieved</span>
2) `model_ridge$lambda.1se` - Which is the **largest lambda** at which it is within <span style='color:var(--mk-color-yellow)'>1 standard error of the smallest MSE</span>
## Best Alpha

For elastic net we will **additionally** need to <span style='color:var(--mk-color-yellow)'>find the best alpha as well</span>.
```R
generate_cvmodels <- function (x) {
	set.seed (123)
	return(cv.glmnet(train.x, train.y, type.measure = "mse", alpha = x/10))
}
cv_models <- lapply (0:10 , generate_cvmodels) # Try all alpha from 0.1 to 1
```

Note that we **do not specify lambda** because <span style='color:var(--mk-color-green)'>each alpha has its own best lambda</span>.

We can <span style='color:var(--mk-color-orange)'>extract the best alpha</span> as follows:
```R
cv_error <- unlist(lapply(cv_models , function(x) x$cvm[x$lambda == x$lambda.min]))
(which(cv_error == min(cv_error)) -1)/10
```

A all in 1 function to **get the best parameters** is as follows:

```R
get_best_model <- function (models , errors) { # A list of models, and errors
	best_n <- which(errors == min(errors))
	return(
		data.frame(
			alpha = (best_n - 1)/10, # best_n = 1 refers to alpha = 0, and
				best_n = 11 refers to alpha = 1.
			lambda = models [[ best_n ]] $lambda.min ,
			CV_error = errors[best_n]
		)
	)
}
best_parameter <- get_best_model(cv_models , cv_error) # naming follows the codes above
```
## Best Subset Technique

We can also **try all possible subsets** of variables and get the best one:
```R
fit.bestsub <- regsubsets(Y ~ ., data = df, nvmax = 16) # nvmax sets the maximum number of variables
# To view all the k-variable models and R2
result <- cbind(summary(fit.bestsub)$outmat, R2=round(summary(fit.bestsub)$rsq,3))

# See the results in a table
kable(result) %>% kable_classic() %>%
	kable_styling(font_size = 12) %>%
	row_spec(0, angle = 90)
```

# Standardisation
---
To <span style='color:var(--mk-color-orange)'>standardise all variables</span> in a dataset we can do the following:
```R
scaler <- apply(df , 2, sd) # sd is the standard deviation function
df_standardised <- as.data.frame(apply(df, 2, function (x) x/sd(x)))
```

This just **follows the standardisation formula** and to convert back into an unstandardised format we can do the following
```R
df[1 ,6] * scaler[6] # Change the numbers accordingly based on the variable position
```

# Plotting Graphs
---
## Bar Graph

```R
ggplot(data = df, mapping = aes(x = <x axis variable>, y = <y axis variable>,
								 fill = <grouping>)) +
	geom_bar(stat = "identity") +
	geom_text(aes(label = <value>, vjust = -0.5) + # This is for labels on the graph
	labs(x = "<X Label Header>", y = "<Y Label Header>", title = "<Graph title>"))
```
## Stacked Bar Plot

```R
ggplot(data = df) + 
		geom_bar(aes(x = <X axis variables>,
		fill = <Some other variable>), # Specify something other than x
		colour = "black")
```
## Line Graphs

```R
ggplot(data = df) +
geom_line(aes(x=<X axis variable>, y=<Y axis variable>, group=1)) +
geom_point(aes(x=<X axis variable>, y=<Y axis variable>)) + 
labs(x = "<X axis title>", title = "<Graph title>")
```
## Box Plot

```R
ggplot(df, aes(x = <x axis value>, y = <y axis value>, fill = <colour by variable>)) +
geom_boxplot() +
theme(axis.text.x = element_text(angle = 20, hjust = 1)) +
labs(x = "<X Label Header>", y = "<Y Label Header>",
		 title = "<Graph title>")
# If we use fill it will seperate based on groups
```
## Histogram

```R
ggplot(df, aes(x=<X axis variable>)) +
	geom_histogram(binwidth=5, fill="salmon", color = "black") +
	labs(Y = "<Y axis title>", title = "<Graph title>")
```
## Scatterplot

```R
ggplot(df, aes(x = <x axis value>, y = <y axis value>)) +
geom_point() +
geom_smooth(method="lm" , color="red", se=FALSE) +
ggtitle("Floor size against resale price") +
labs(X = "<X axis title>", Y = "<Y axis title>", title = "<Graph title>")
```
## GGPairs
```R
library(GGally)
ggpairs(df) # Corelation plots good if number of variables is small
```

If you do not want to see all variables you can `select` a subset of variables and use `ggpairs`.
## Corelation Plot

```R
library(corrplot)
corrplot(cor(df[c[<"index of columns in the df">]]),
method = "number", type = "upper",
tl.col = "black", tl.srt = 30)
```
## `Plot` Function

If we have build a model we can use the `plot` function to plot some graphs:
```r
Plot(model, which = <integer>)
```

**Where**
- 1 is for residual plot
- 2 is for the Q-Q plot
- 4 is for the cooks distance plot
## Display Data in a Table

The below is an example, replace with the data you want to show
```R
# Collect all of the required information into a single dataframe
summary_lambda_3models_train <- data.frame(
	Train_MSE = c(mseridgetrain,
				mselassotrain,
				mse4_train,
				mse_train_elasticNet))

summary_lambda_3models_test <- data.frame(
	Test_MSE = c(mseridgetest,
				mselassotest,
				mse4_test,
				mse_test_elasticNet))

# Label the rows of the data frame
row.names(summary_lambda_3models_train) <- c("Ridge Model",
											"LASSO Model",
											"Best Subset",
											"Elastic Net")
# Return the information
knitr::kable(cbind(summary_lambda_3models_train, summary_lambda_3models_test), digits = 3)
```