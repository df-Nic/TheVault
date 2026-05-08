---
Title: Factor Analysis
Date Created: 07-April-2026
Last Updated: 24-April-2026
Tags:
  - DSA3362
---
# Factor Analysis
---
Factor analysis seeks to <b><span style='color: #FFD700'>describe</span></b>, if possible, the <b><span style='color: #FFD700'>covariance relationships among many variables</span></b> <b><span style='color: #FFD700'>in terms of</span></b> a few underlying, but <b><span style='color: #FFD700'>unobservable</span></b> (*non measurable or latent*), random quantities called <b><span style='color: #87CEEB'>factors</span></b> ($F$).

It **assumes** that variables can be <b><span style='color: #FFD700'>expressed in terms of some linear dependence on some latent factors</span></b>.

>[!important] But these factors must not be corelated to other factors
>We try not too but they can be corelated.

>[!example] A high level example
>Test scores for math, science, language suggests an underlying intelligence factor, while things like physical fitness scores might correspond to another factor.

>[!question] PCA vs FA
>In [[Year 3/Sem 2/DSA3362 - Predictive Data Analytics/Principle Component Analysis.md|PCA]] each principle components is a linear combination of existing variables.
>
>In FA, we are <b><span style='color: #FFD700'>expressing existing variables as linear combinations of latent factors</span></b> & are <b><span style='color: #FFD700'>based on some assumptions</span></b>.
>
>However **they are similar** in the fact that:
>- Both manage to <b><span style='color: #FFD700'>reduce the number of variables</span></b>, from p to m ($m \lt p$)
>- Both <b><span style='color: #FFD700'>require orthogonality of PCs/factors</span></b>
>- Both are tacked from the <b><span style='color: #FFD700'>eigen-decomposition of the covariance/correlation matrix</span></b>
## Factor Analysis Terms

So given a variable $X_{1}$ and some 2 latent variables $F_{1}$ and $F_{2}$ we can express $X_{1}$ as:
$$
X_{1} - \mu_{1} = l_{11}F_{1} +l_{12}F_{2} + \epsilon_{1}
$$
Where:
- $F$ is known as the <b><span style='color: #87CEEB'>latent variables</span></b> (*if we have only 1 of them it is also known as a common factor*)
- $\mu$ is the <b><span style='color: #FFD700'>mean of the variable</span></b>
- $\epsilon$ is known as <b><span style='color: #87CEEB'>errors</span></b> or <b><span style='color: #87CEEB'>specific factors</span></b>
- $l$ is known as <b><span style='color: #87CEEB'>loadings</span></b>

All these <b><span style='color: #FFD700'>values/terms are unique to the specific variable except the latent variable</span></b> (*sometimes the latent variables is negligible which we can ignore*).

But to <b><span style='color: #FFD700'>find the number of factors</span></b> we can use the <b><span style='color: #87CEEB'>Kaiser criterion</span></b>, which is the <b><span style='color: #FFD700'>number of eigenvalues in the dataset that is greater than 1</span></b>.

```R
# Which you can do easily with this 2 lines of code
eigen_values <- eigen(df)$values
num_factors <- sum(eigen_values > 1)
```

>[!fail] But the value for loadings changes depending on the number of latent variables you want to use

This is for 1 variable we can **generalise it to any number of variables** my using matrices. It will still take on this form:
$$
X - \mu = LF + \epsilon
$$
But we <b><span style='color: #FFD700'>put all the values in a matrix</span></b>. This is known as the <b><span style='color: #87CEEB'>orthogonal factor model</span></b>.

For **term** $L$:
$$
\begin{bmatrix}
l_{11} & \dots & l{1n}\\
\vdots & \dots & \vdots\\
l_{m1} & \dots & l{mn} \\
\end{bmatrix}
$$
Where:
- $m$ is the <b><span style='color: #FFD700'>number of original variables</span></b> in the dataset
- $n$ is the <b><span style='color: #FFD700'>number of latent variables</span></b>. 

For **terms** $X$, $\mu$ and $\epsilon$ they are all <b><span style='color: #FFD700'>just a m by 1 matrix</span></b>:
$$
\text{$X$ or $\mu$ or $\epsilon$} =
\begin{bmatrix}
a_{1} \\
\vdots \\
a_{m}
\end{bmatrix}
$$

As for the **latent variables**
$$
F= 
\begin{bmatrix}
F_{1} \\
\vdots \\
F_{n}
\end{bmatrix}
$$

## Assumptions In Factor Analysis

When we do factor analysis we need to have some **assumptions for the latent variables & specific factors**.

And if <b><span style='color: #FFD700'>all the assumptions are true then the following equation holds</span></b>:
$$
cov(X) = \Sigma = LL^{T} + \Psi
$$
This is the **sum** of the <b><span style='color: #FFD700'>variance shared via the common factors</span></b> also known as <b><span style='color: #87CEEB'>communality</span></b> & the <b><span style='color: #FFD700'>unique variance</span></b>.

>[!important] Unique variance does not give us that much information

This <b><span style='color: #FFD700'>does not have to be equal as sometimes it does not hold so generally an estimate</span></b> will do.

>[!success] This is important as it simplifies the finding of the loading matrix L & the diagonal matrix $\Psi$
### Assumptions For Latent Variables

The **expected value** for the latent variable:
$$ E(F) = 
\begin{bmatrix}
0\\
\vdots \\
0 \\
\end{bmatrix}
$$
Where:
- The size of the matrix is $n \times 1$

The **covariance** will be:
$$
 cov(F) = 
\begin{bmatrix}
1 & 0 & \dots & 0 \\
0 & 1 & \dots & 0 \\
\vdots & \ddots & \dots & 0\\
0 & \dots & \dots & 1
\end{bmatrix}
$$
Where:
- The size of the matrix is $n \times n$

>[!info] Essentially the diagonals are all 1 or in other words a identity matrix

### Assumptions For Specific Factors

As for the specific factors, the **expected value**:
$$
 E(\epsilon) = 
\begin{bmatrix}
0\\
\vdots \\
0 \\
\end{bmatrix}
$$
Where:
- The size of the matrix is $m \times 1$

The **covariance**:
$$
 cov(\epsilon) = = E(\epsilon\epsilon^{T}) 
\begin{bmatrix}
\psi{1} & 0 & \dots & 0 \\
0 & \psi{2} & \dots & 0 \\
\vdots & \ddots & \dots & 0\\
0 & \dots & \dots & \psi{m}
\end{bmatrix} = \Psi
$$
Where:
- The size of the matrix is $m \times m$ and the diagonals are all values of $\psi$

### Assumptions For Specific Factors & Latent Variables

Lastly between the latent variables and specific factors, the **covariance**:
$$
cov(\epsilon, F) = E(\epsilon F^{T})
\begin{bmatrix}
0 & 0 & \dots & 0 \\
0 & 0 & \dots & 0 \\
\vdots & \ddots & \dots & 0\\
0 & \dots & \dots & 0
\end{bmatrix}
$$
Where:
- The size of the matrix is $m \times n$
>[!info] The whole matrix is just a zero matrix
## Principal Component Method

Recall that in [[Year 3/Sem 2/DSA3362 - Predictive Data Analytics/Principle Component Analysis.md|PCA]] we compute the eigenvalues and eigenvectors then we **drop the lowest eigenvalues to reduce dimension**.

The <b><span style='color: #FFD700'>remaining eigenvalues and eigenvectors can now form our loading matrix</span></b>, all we need to do is take the <b><span style='color: #FFD700'>square root of the eigenvalue times the corresponding eigenvector pair</span></b>.

>[!info] So we do PCA first then we compute the factor loadings

>[!important] Then to get $\Psi$ we just take the $\Sigma - LL^{T}$
> But we <b><span style='color: #FFD700'>only take the values in the diagonal</span></b>. Because if you look at $\Psi$ the matrix is a diagonal matrix.

Now if we take $\Sigma - (LL^{T} + \Psi)$ the <b><span style='color: #FFD700'>sum of squares for the entries is no greater than the sum of squares</span></b> of the <b><span style='color: #FFD700'>eigenvalues that were dropped</span></b> (*this means that the discarded eigenvalues the error of our approximation is small*).

>[!note] If our variables are not commensurate then we scale them
>This also means that we are [[Year 3/Sem 2/DSA3362 - Predictive Data Analytics/Principle Component Analysis.md#Perform PCA|using the correlation matrix]] instead of the covariance matrix.

>[!note] Then to select the optimal number of PCs we use the [[Year 3/Sem 2/DSA3362 - Predictive Data Analytics/Principle Component Analysis.md#Determining the Number Of Principle Components|screen plot]] AND a combination of domain expertise
## Factor Rotation

A <b><span style='color: #87CEEB'>factor rotation</span></b> is an <b><span style='color: #FFD700'>orthogonal transformation of factor loadings</span></b> where:
$$
L^{*} = LT
$$
Where:
- $T$ is some orthogonal matrix where $TT^{T} = T^{T}T = I$

This **rotation** will result in the <b><span style='color: #FFD700'>estimated covariance or correlation matrix to be unchanged</span></b>:
$$
L^{*}(L^{*})^{T} + \Psi = LTT^{T}L^{T} + \Psi = LL^{T} + \Psi
$$

>[!warning] There are an infinite number of factor rotations, or orthogonal transformations, that explain the original data equally well
>
>So typically people use a provides a <b><span style='color: #87CEEB'>“simple structure”</span></b>: a pattern of loadings such that each observed variable has a <b><span style='color: #FFD700'>high loading on one factor and small-to-moderate loadings on other factors</span></b>. But this <b><span style='color: var(--mk-color-red)'>does not always exist</span></b>.

But generally there are **2 types of rotations**:
- Orthogonal rotation (*make factors uncorrelated an example is the varimax rotation*)
- Oblique rotation (*make factors corelate*)
### Varimax Criterion

The <b><span style='color: #87CEEB'>varimax criterion</span></b> (*to find the right rotation*) seeks to <b><span style='color: #FFD700'>“spread out” squares of loadings on each factor</span></b> as much as possible by maximising:
$$
V \propto \sum^{m}_{j - 1} (\text{Variance of squares of (scaled) loadings for j-th factor})
$$
>[!note] There are other criterions as well such as quartimax, promax and oblimin

>[!goal] Maximise within-factor variance
## Factor Scores

So far we only estimate $L$ and $\Psi$ but what about $F$ and $\epsilon$, this is where <b><span style='color: #87CEEB'>factor scores</span></b> comes in.

Here are some methods that we can use:
- Ordinary least squares method
- Weighted least squares method
- Regression method
# Factor Analysis In R
---
Before we dive into the R code, there is a **guideline on how to do factor analysis**:

1) Perform a principal component factor analysis, and try a varimax rotation
2) Perform a maximum likelihood factor analysis, including a varimax rotation
3) Compare solutions from both factor analyses:
	- whether loadings group in the same manner
	- whether factor scores agree with each other
4) Repeat Steps 1-3 for other numbers of common factors: whether more factors contribute (*especially useful if the screen plot is ambiguous in step 1*)

If the **dataset is large**, further <b><span style='color: #FFD700'>split the dataset into two halves and perform a factor analysis on each half</span></b>, to check the stability.

If the **data has a temporal order**, split such that the <b><span style='color: #FFD700'>earlier observations are in the first half and the later observations are in the second half</span></b>, to reveal changes over time.
## Perform FA

>[!note] You need to import the `psych` library

To **do FA using the PC method** we can use the `principal` function:

```R
fa <- principal(r = df, nfactors = 1, rotate = "none", cor = "cov")
# r is the raw data frame
# nfactors is the number of factors to extract
# rotate is the possible rotations of the solution varimax, quartimax, promax, oblimin
# cor by default it uses the correlation matrix, use "cov" for covariance matrix
```

>[!important] By default use `principal` if nothing was stated

What it **prints out will be a table of values** 
- First there will be `PC*` (*this will be RC if we use some rotation*) which is our <b><span style='color: #FFD700'>factors extracted</span></b>. It is the square root of the eigenvalues times the eigenvector (*it is labeled as PC but it is not the principal component*).
- Then `h2` is the <b><span style='color: #FFD700'>communality of the observed variables</span></b> which is the sum of the squares of the factor loadings (*square of PC*)
- Then `u2` gives the <b><span style='color: #FFD700'>variance of the variable</span></b> (*1 - h2, also known as uniqueness*)
- Then we have `H2` and `U2` which is the <b><span style='color: #FFD700'>proportion of the variance</span></b> with respect to `h2` and `u2` with the total variance
- Then`SS loadings` is the <b><span style='color: #FFD700'>variance explained by the respective factor</span></b>
- Then `Porportion var` is the <b><span style='color: #FFD700'>variance of the respective factor but in proportion</span></b> (*variance or SS loadings divided by number of variables*)
- Then we have `Cumulative Var` which tells us <b><span style='color: #FFD700'>the sum of proportion of the variances was explained in total</span></b> based on the all the factors up till that column

If you need **more precision**:
- Communality use `$communality`
- Uniqueness use `$uniquenesses
- For variances use `$Vaccounted`

>[!tldr] Understanding the loadings
>If for factor 1 we see some variables are high (*0.7 or higher*) while the rest are low then you can consider factor 1 to be some relationship between the high loading variables.

>[!note] You need to import the `stats` library

To **do FA using the maximum likelihood method** we can use the `factanal` function:

```R
factanal(covmat = df, factors = 1, n.obs = 145, rotation = "none")
```

>[!important] To use this function we need at least 3 observed variables in the dataset

>[!tldr] Maximum likelihood method
>Is another way to estimate the loadings and the specific variances ($\Psi$) by maximising some likelihood of $X - \mu$ by assuming $F$ and $\epsilon$ are jointly normal.

`factanal` gives us some additional information as well:
- `Uniqueness` which is the <b><span style='color: #FFD700'>specific variances</span></b> for that variable (*unique variances which we can also computing using 1 - sum of squared loadings for that variable*)
- `p-value` so here the <b><span style='color: #FFD700'>null hypothesis is that k-factor is insufficient</span></b>. And if we reject the null hypothesis then we need to go back and then extract more factors (*We extracted too few*)
## Extracting The Factor Scores

To **extract the factor scores** using the following code:

```R
fa$scores
```

This will give us the <b><span style='color: #FFD700'>scores for each observation based on the factors</span></b>.
