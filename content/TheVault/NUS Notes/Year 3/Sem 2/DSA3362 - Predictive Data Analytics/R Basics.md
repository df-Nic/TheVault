---
Title: R Basics
Date Created: 14-January-2026
Last Updated: 23-April-2026
Tags:
  - DSA3362
  - ProgrammingLanguage/R
---
# Data Handling
---
We can **load a CSV file** into R Studio using the following code:
```R
df <- read.csv("file_path", stringsAsFactors = TRUE) # Data will be loaded as a  data frame object
```

>[!warning] Do check if it actually converts to factors
>Sometimes this does not change a column to a factor. If that is the case use `col <- as.factor(col)`.

To get the **dimensions** we can use`dim`, `nrow`, `ncol`.

To **drop a column** we can use the `subset` function:
```R
# Replace it wil the col name without the "" just the text itself
subset(df, select = -c(col_1, col_2)) 
# Can us subset to filter also
subset(df, col == "condition")
```

After loading in the data we can get a **summary of the data** using the `summary` function:
```R
summary(df)
```

We can **determine the relationship** (*corelation*) between 2 variables using the `cor` function:
```R
cor(df$col_1, df$col_2)
```

If we want to convert categorical values into factors (*essentially encoding them into numbers*) we can use the `as.factor` function:
```R
df$col <- as.factor(df$col)
```

To **know what you can call with a variable** you can do `str(var_name)`.

Then we can **split the data frame using indexes** (`df[rows, cols]`):
```R
df[,1:5] # Means we want columns 1 to 5 same can be used for rows
df[c(1,3),] # Means we want rows 1 and 5 same can be used for cols
df[, c('col1', 'col2')] # Here we want to keep columns based on the name
df[df$Age > 18, ] # Here we can filter rows using a condition
```

>[!note] R uses 1-based indexing meaning the first element is index 1

# Miscellaneous
---
## Model Performance

We can get the **performance of the fitted model** using the same `summary` function.

```R
 summary(fitted_model)
```

Or we can just use `model$results` to extract some metrices like RMSE, R squared and MAE.

This will give an output like this:
![[Sample Model Summary Output.png|center]]

>[!abstract] The p-value is used for the null hypothesis
>The null hypothesis is a <b><span style='color: #FFD700'>default assumption that there is no significant effect and is just random chance</span></b>. A <b><span style='color: #98FB98'>p-value of less than 0.05 is a strong indication that the null hypothesis is false</span></b>.
>
>For the **variables**, the null hypothesis states that the <b><span style='color: #FFD700'>coefficient is 0</span></b>.
>
>For the **F-statistic**, the null hypothesis states that a <b><span style='color: #FFD700'>model with no input variables</span></b> (*intercept only model*) <b><span style='color: #FFD700'>fits better than the fitted model</span></b> (*model under consideration*).

>[!abstract] We can also find the coefficients using the matrix method
>We can use the `solve` function to get the coefficients once we formulate the X and Y matrixes:
>```R
solve(t(X) %*% X) %*% t(X) %*% Y
>```
>
>Where:
>- `%*%` is R's syntax for matrix multiplication
>- `t(x)` is a function to transpose a matrix
### Handling Multicollinearity

To detect multicollinearity we can **compute the variance inflation factors** (*VIFs*) using the `vif` function

```R
vif(model)
```

>[!note] VIF of 5 and above indicates multicollinearity exist