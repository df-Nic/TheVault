---
Title: Principle Component Analysis
Date Created: 20-March-2026
Last Updated: 25-March-2026
Tags:
  - DSA3362
  - AI/ML/DimensionalityReduction/PCA
---
# How Does PCA Reduce Dimensions?
---
First we need to understand what does **"information"** means, in PCA it is measured in term of the <b><span style='color: #FFD700'>variability in the data</span></b>.

**Dimensionality reduction is achieved** by selecting the <b><span style='color: #FFD700'>first few principle components that explain sufficiently the variability</span></b> in the original data.

>[!note] In PCA when we talk about information we are actually referring to variability

>[!important] We are not removing variables but how can we apply some sort of linear combination to make new dimensions

>[!important] PCA ONLY WORKS on continuous data
>For datasets with **only categorical variables** use [[Year 3/Sem 2/DSA3362 - Predictive Data Analytics/Correspondence Analysis.md|correspondence analysis]].

So essentially:
1) The first PC is the linear combination of the original p dimensions that explains the most variation
2) The second PC is the linear combination that explains the second most variation, that is orthogonal to the first PC.
3) ...
4) The p-th PC is the linear combination that explains the least variation, that is orthogonal to all other PCs.

>[!question] What are principle components?
>They are essentially <b><span style='color: #FFD700'>new dimensions</span></b> which are a <b><span style='color: #FFD700'>combination of all the existing variables</span></b> (*some linear combination*) that explains the most variation.
>
>A **simple formula for variance is the sample variance** which is:
>
>$$
>\frac{1}{n}\sum^{n}_{i = 1} (x_{i,d})^{2}
>$$
>Where:
>- $n$ is the total number of data points
>- $d$ is the d-th dimension of the datapoint (*1st, 2nd, 3rd etc*) 

So typically we are <b><span style='color: #FFD700'>rotating the coordinate axes to find one that gives the largest possible variance</span></b>.

>[!important] Scaling the data affects the results of PCA
> **Without scaling**, PCA will <b><span style='color: #FFD700'>emphasis more on variables with larger variances</span></b>.
> 
> So scaling depends on the problem, domain expertise & context:
> - **Don't scale** if we want to give more weight to variables with larger variances & keep working on the raw data
> - **To scale** if we want to weigh all variables equally

>[!example] Example of PCA in a 2-dimension space
>We can rotate the axes by moving the axis at some angle such $(\cos \theta, \sqrt{1 - \cos^{2} \theta})$.
>
>So computing the the projection of $(a, b)$ onto this new axis, it will be $a \cos \theta + b \sqrt{1 - \cos^{2} \theta}$, which converts our points into 1 dimension.
>
>So we just need to tune for $\theta$ using the sample variance formula.

Interestingly all this is **linked to our variance-covariance matrix**, where its:
- <b><span style='color: #FFD700'>Eigenvectors are directions of the PCs</span></b>
- <b><span style='color: #FFD700'>Eigenvalues are equal to the variances explained by the PCs</span></b> (*or the eigenvectors*)

So to **find the number of PCs** to use we can <b><span style='color: #FFD700'>use the elbow method</span></b> (*at some point the variance of will be small*).

When doing **PCA here are some properties**:
- <b><span style='color: #FFD700'>PCs will always preserve the original variance</span></b> from the original variables
- <b><span style='color: #FFD700'>Successive components</span></b> (*PCs*) will be <b><span style='color: #FFD700'>orthogonal</span></b> to one another, meaning they will never correlate
- The <b><span style='color: #FFD700'>sum of squared loadings for each PC will be 1</span></b> (*if not then the variance of a component is unbounded*)

>[!success] PCA allows us to understand behaviors of different variables
>If 1 variable goes up will it affect the others.

>[!abstract] Formal theorem of PCA
>**Formally** this is PCA, let $\Sigma$ be the variance-covariance matrix associated with the variables $[X_{1}, \dots, X_{p}]$. $\Sigma$ also contains the eigenvalue-eigenvector pairs denoted as $(\lambda_{x}, e{x})$ where $\lambda_{1} \ge \lambda_{2} \ge \dots \ge \lambda_{p} \ge 0$.
>
>The i-th PC is given by:
>$$
>Y_{i} = e_{i1}X_{1} + \dots e_{ip}X_{p}
>$$
>And with these choice:
> - $\text{Variance}(Y_{i}) = \lambda_{i}$
> - $\text{Covariance}(Y_{i}, Y_{j}) = 0$ where $i \neq j$
# PCA In R
---
## Covariance Matrix

To **get the covariance matrix** (*sometimes known as correlation*) we can use the `cov` function:

```R
A <- cov(df)
```

This matrix the:
- **Diagonals** are your variances (*so sum them up foe the total variance*)
- The **other values** are the covariance

>[!important] If our variables are all not corelated then it is not worth while to do PCA
>We can check this using the <b><span style='color: #87CEEB'>null hypothesis for Bartlett’s</span></b>, which checks that he <b><span style='color: #FFD700'>correlation matrix is not an identity matrix</span></b>.
>
>```R
>cortest.bartlett(as.matrix(df), n = 10) # n is the length of the df
># This returns the p-value which we can reject the null hypothesis
>```

## Perform PCA

>[!note] You need to import the `stats` library

To **do PCA** we can use the `prcomp` function:

```R
res.pca <- prcomp(x = df, scale = FALSE) # You can toggle scale to be true
# Using scale = TRUE amounts to using the correlation matrix
# This scale is for SD = 1 and not mean to be 0 as center to be 0 is automatically done by the function
```

This function will <b><span style='color: #FFD700'>compute the variance-covariance matrix & the eigen-decomposition</span></b>.

>[!note] PCA will generate as many PCs as number of variables / dimensions
>But we hope that majority of the variance can be explained in the first few PCs.

## Extracting Information From PCA

We can get the **standard deviations** or the square root of the eigenvalues **for each principle components**:

```R
res.pca$sdev

# OR you can square it to get the eigenvalues / variance
res.pca$sdev ^2

# If you want to display the eigenvalues are a proportion (% our of 100 of the total variance)
res.pca$sdev^2 / sum(res.pca$sdev^2)
```

We can also extract the **eigenvectors** (*also called loadings*) or the principle components:

```R
res.pca$rotation # The weights to transform our datapoint into the different PCs
```

Then to get the **sum of squared loadings**, just square the loadings for the PC and sum them up.

To get the **projections** on the principal components:

```R
res.pca$x
```

And to **get the dimensionality reduction** to some dimension $d$:

```R
res.pca$x[, d] # Change d to some value you want to redice to typically 1
# This can be useful if you want to see the transformed values to a particular d-th PC
# You can use c(1,2) to choose multiple PCs 
dat <- as.data.frame(res.pca$x[, 1:4]) # So typically you do this to build your model
```

If you do a **summary** you will get the following:
- Standard deviation (*Square it to get the variance or your eigenvalue for that PC*)
- Proportion of variance (*percentage of the total variance explained by that PC*)
- Cumulative proportion (*percentage of the total variance explained by all PC's up till that point*)

## Determining the Number Of Principle Components

>[!note] You need to import the `factoextra` library

We can plot the **screen plot** to determine the number of PCs using the `fviz_eig` function:

```R
fviz_eig(X = res.pca, choice = "eigenvalue") # You can change to variance
```

So here we **look at the elbow**.