---
Title: Correspondence Analysis
Date Created: 31-March-2026
Last Updated: 24-April-2026
Tags:
  - DSA3362
  - AI/ML/DimensionalityReduction/CA
---
# Correspondence Analysis
---
In [[Year 3/Sem 2/DSA3362 - Predictive Data Analytics/Principle Component Analysis.md|PCA]] we were able to reduce dimensionality for continuous variables only, so <b><span style='color: #87CEEB'>correspondence analysis</span></b> (*CA*), is <b><span style='color: #FFD700'>used for datasets with categorical variables only</span></b>.

CA is a <b><span style='color: #FFD700'>technique for graphically displaying</span></b> a <b><span style='color: #87CEEB'>contingency table</span></b> by <b><span style='color: #FFD700'>representing its rows & columns in a low-dimensional space</span></b> (*preferably in a 2-D plane*), allowing for more <b><span style='color: #98FB98'>rapid interpretation & understanding of the data</span></b>.

>[!important] CA is a visualisation tool to show how the different categories deviate from the variance
>Essentially it shows how they are related to one another.

>[!abstract] Contingency table
>Displays the <b><span style='color: #FFD700'>frequency distribution of two categorical variables</span></b>, providing a basic picture of interrelation between them.
>
>It is essentially the count of the number of rows with some category for variable 1 and some cateogry for variable 2.

Both CA & PCA, aim to reduce dimensionality, while keeping as much information as possible, but **how is it used is different**:

|                PCA                |                             CA                             |
| :-------------------------------: | :--------------------------------------------------------: |
| Continuous variables (*raw data*) |        Categorical variables (*contingency table*)         |
|        Variables in column        |              Variables in both rows & columns              |
|   Reducing number of variables    |           Reducing number of levels of variables           |
|         Keeping variance          | Keeping <b><span style='color: #87CEEB'>inertia</span></b> |
>[!tldr] Level
>A level is just the <b><span style='color: #FFD700'>values in which this variable can take</span></b>.
>
>Thus for a categorical variable the levels are essentially the different category values for that specific category.
# Terminologies & Concepts
---
## Chi-Square Test Of Independence

Denoted as $X^{2}$-test of independence, it just <b><span style='color: #FFD700'>test whether two categorical variables are independent or not</span></b>.

Essentially we will be using the [[Year 2/Sem 1/DSA3361 - Inferential Data Analytics/Data Analysis.md#Hypothesis Testing|null hypothesis]] (*the 2 variables are independent*), set a <b><span style='color: #FFD700'>level of significance</span></b> ($\alpha$ *& is typically 0.05*) and the compute the $X^{2}$-statistic & <b><span style='color: #FFD700'>compute the p-value</span></b>.

If the <b><span style='color: #FFD700'>p-value is lower than the level of significance then reject the null hypothesis</span></b> (*& accept the alternative hypothesis which is they are not independent*).

To **compute the chi-square statistic** we need 2 things:
1) **Observed frequency**
2) **Expected frequency**

Then with the 2 frequencies computed we can **compute the chi-square statistic** using the following formula:
$$
X^{2} = \sqrt{\sum_{\text{row}} \sum_{\text{col}} \frac{(\text{observed} - \text{expected})^{2}}{\text{expected}}}
$$

>[!abstract] Chi-square distance
>It is a <b><span style='color: #FFD700'>weighted Euclidean distance</span></b> where the weight is the inverse of the respective average profile element (*[[Year 3/Sem 2/DSA3362 - Predictive Data Analytics/Correspondence Analysis.md#Average Profiles|centroid]]*). In other words, <b><span style='color: #FFD700'>categories with few observations contribute relatively more to the inter-point distances than categories with more observations</span></b>.
>
>To to calculate the Chi-square distance for a particular row / column:
>$$
> d = \sqrt{\sum_{j} \frac{(a_{ij} - a_{\cdot j})^{2}}{a_{\cdot j}}}
>$$
>Where:
>- $i$ is any row or column in your contingency table
>- $a{ij}$ is your row or column [[Year 3/Sem 2/DSA3362 - Predictive Data Analytics/Correspondence Analysis.md#Profiles|profile]] for cell $i$, $j$ (*row chi-square distance then its the row profile*)
>- $a_{\cdot j}$, if you are computing the row chi-square distance then this is the column mass (*and vice versa*)
### Observed Frequency

This is just <b><span style='color: #FFD700'>what you observed in the dataset or in your contingency table</span></b>.

But this table will have **additional rows & columns**, namely:
- Row masses (*proportion of the row category with respect to the dataset*)
- Column masses (*proportion of the col category with respect to the dataset*)
- Totals, which known as <b><span style='color: #87CEEB'>marginal distribution</span></b> for row/columns

>[!abstract] Masses
>It is the <b><span style='color: #FFD700'>proportions of frequencies with respect the grand total</span></b> and this is for a <b><span style='color: #FFD700'>single cell / value</span></b>.

>[!example] Putting all of this together
>|                     | Glance | Fairly thorough | Very thorough |  Total  | Row masses |
| :-----------------: | :----: | :-------------: | :-----------: | :-----: | :--------: |
|    Some Primary     |   5    |        7        |       2       |   14    |   0.045    |
|  Primary Completed  |   18   |       46        |      20       |   84    |   0.269    |
|   Some Secondary    |   19   |       29        |      39       |   87    |   0.279    |
| Secondary Completed |   12   |       40        |      49       |   101   |   0.324    |
|    Some Tertiary    |   3    |        7        |      16       |   26    |   0.083    |
|        Total        |   57   |       129       |      126      | **312** |            |
|    Column Masses    | 0.183  |      0.413      |     0.404     |         |            |
>
> So the masses are the <b><span style='color: #87CEEB'>observed proportions</span></b>, which is just the <b><span style='color: #FFD700'>value divided by the row/col total for the given mass</span></b>.
### Expected Frequency

Also known as <b><span style='color: #87CEEB'>theoretical samples</span></b>. We need the **contingency table** from the observed frequency to compute the expected frequency. When we talk about <b><span style='color: #FFD700'>expected it is under the null hypothesis</span></b> (*they are independent*).

We need to <b><span style='color: #FFD700'>row and column mass to compute the expected frequency</span></b>:
$$
\text{Expected frequency of row $x$ \& col $y$} = \text{Total} \times \text{Row mass for row $x$} \times \text{Col mass for col $y$}
$$
Or you can do this also:
$$
\text{Expected frequency of row $x$ \& col $y$} = \text{Row total for row $x$} \times \text{Col total for col $y$} \div \text{Grand total}
$$

>[!example] Putting all of this together
>Using the same contingency table in the observed frequency example,
>
>|                     | Glance | Fairly thorough | Very thorough |  Total  | Row masses |
| :-----------------: | :----: | :-------------: | :-----------: | :-----: | :--------: |
|    Some Primary     |  2.56  |      **5.78**       |     5.66      |   14    |   0.045    |
|  Primary Completed  | 15.37  |      34.69      |     33.94     |   84    |   0.269    |
|   Some Secondary    | 15.92  |      35.93      |     35.15     |   87    |   0.279    |
| Secondary Completed | 18.48  |      41.71      |     40.80     |   101   |   0.324    |
|    Some Tertiary    |  4.76  |      10.74      |     10.50     |   26    |   0.083    |
|        Total        |   57   |       129       |      126      | **312** |            |
|    Column Masses    | 0.183  |      0.413      |     0.404     |         |            |
>
>The expected frequency for some primary & fairly thorough is $312 \times 0.045 \times 0.413 = 5.78$.
>
>For <b><span style='color: #FFD700'>row or column masses its just that row or column total divide by the grand total</span></b>.

>[!abstract] Expected & Observed Frequency Comparison
>If the **expected frequency is larger than the observed frequency** then it means that the <b><span style='color: #FFD700'>2 levels repeal each other</span></b>.
>
>If the **expected frequency is equal or lower than the observed frequency** then it means that the <b><span style='color: #FFD700'>2 levels attract each other</span></b> (*1 goes up the other will go up*). 
## Inertia

But recall we want to reduce the number of variables but knowing if <b><span style='color: var(--mk-color-red)'>2 variables are correlated does not help</span></b>, we need to <b><span style='color: #FFD700'>know if the levels are correlated</span></b>.

So inertia is the <b><span style='color: #FFD700'>a measure of variance in the contingency table that accounts for sample size</span></b>. And to **compute total inertia**:
$$
\text{Total Intertia} = \frac{\text{$x^{2}$-stastic}}{N}
$$
Where:
- $N$ is total number of data points

Then to **compute inertia for a particular mass** (*be it row or column*):
$$
\text{Inertia} = (\text{i-th mass}) \sum_{i} (\text{$X^{2}$ distance from i-th profile to the centroid})^{2}
$$
Where:
- If you are computing the i-th row inertia, then you need the i-th row mass and its chi-square distance

>[!important] If you compute the total row or col inertia it will be the same value

When the **inertia is low**, the rows (*or columns*) are close to each other, and there is <b><span style='color: #FFD700'>low association</span></b> between rows and columns.

The **higher the inertia**, the <b><span style='color: #FFD700'>greater is the association</span></b> between rows and columns, displayed by higher dispersion.

>[!tldr] Between-group inertia & within-group inertia
>When we do CA, we will then group certain categories together (*you can use any clustering technique*). Then when we <b><span style='color: #FFD700'>compute the inertia on the modified dataset</span></b> (*after we group*). we will get <b><span style='color: #87CEEB'>between-group inertia</span></b>.
>
>Then for <b><span style='color: #87CEEB'>within-group inertia</span></b>:
>$$
>\text{Within-group inertia} = \text{Total inertia} - \text{Between-group inertia}
>$$
>
>Then essentially we can see how good our clustering is. We still want to <b><span style='color: #98FB98'>maximise between-group inertia & minimise within-group inertia</span></b>.
## Profiles

A <b><span style='color: #87CEEB'>profile</span></b> is representing a <b><span style='color: #FFD700'>row as some dimensional vector based on the number of columns </span></b> (*and vice versa if we represent a column*).

We can then **scale the profile by the masses**, so for a <b><span style='color: #FFD700'>row profile, scale it by the corresponding column masses</span></b> (*& vice versa*).

>[!note] So scaling the i-th element will be divided by the square root of the i-th column mass
### Row Profiles

For <b><span style='color: #87CEEB'>row profiles</span></b>, we are taking each row and representing it as a $c$ dimension vector where the <b><span style='color: #FFD700'>values are the observed frequency divided by the row total</span></b>.

>[!example] Take the "Some Primary" row as an example
>The row profile for "Some Primary" is:
>
>|              | Glance | Fairly thorough | Very thorough | Total | Row masses |
| :----------: | :----: | :-------------: | :-----------: | :---: | :--------: |
| Some Primary |  5/14  |      7/14       |     2/14      |  14   |   0.045    |
>
>And each row profile for this example is a 3 dimensional vector.

>[!info] The row profile vector sum to 1
### Column Profiles

For <b><span style='color: #87CEEB'>col profiles</span></b>, we are taking each col and representing it as a $r$ dimension vector where the <b><span style='color: #FFD700'>values are the observed frequency divided by the column total</span></b>.

>[!example] Take the "Glance" column as an example
>The column profile for "Glance" is:
>
>|                     | Glance |
| :-----------------: | :----: |
|    Some Primary     |  5/57  |
|  Primary Completed  | 18/57  |
|   Some Secondary    | 19/57  |
| Secondary Completed | 12/57  |
|    Some Tertiary    |  3/57  |
|        Total        |   57   |
|    Column Masses    | 0.183  |
>
>And each column profile for this example is a 5 dimensional vector.

>[!info] The column profile vector sum to 1
### Average Profiles

This **applies for both column and row profiles**. It is the <b><span style='color: #FFD700'>total count in the different row or column divided by the total sum</span></b> , and is the weighted average of profiles.

What it means is that for a particular column, we take the total for that column and divide it by the number of all data points (*for column profile we take the row total divide by the total*).

>[!note] Doesn't matter if the average profile is based on the row or column, this point is called the centroid
# Carrying Out Correspondence Analysis
---
Essentially how CA works is that first we need to **compute the inertia**, which is the <b><span style='color: #FFD700'>average weighted sum of squares distances from row profiles to average profile</span></b> (*or the column profiles to the average*).

Then we will <b><span style='color: #FFD700'>rotate axes such that the first axis contains as much inertia as possible, while the second axis contains the rest of inertia</span></b> and so on.

So to carry our CA:
1) **Preprocessing the contingency table**

So given a matrix $C$ with a total of $n$ data points in the dataset:
1) <b><span style='color: #FFD700'>Find the masses</span></b>
- Divide each element in $C$ by $n$, obtaining $P$ ($P = (1/n) C$)

```R
grand_total <- sum(C)
P <- C / grand_total
```

- Calculate the sum of each row (*row masses*), and assign it to vector r , and the sum of each column (*column masses*), assign it to vector c. (*now we have gotten our contingency table*)

```R
P1 <- P %>% addmargins()
```

- For each element of $P$ in the i-th row and j-th column, subtract from it the product of the i-th row mass and the j-th column mass, obtaining a double centered matrix $Q$ (*the sums of each row & column in Q is all zero*)

```R
row_masses <- as.matrix(P1[1:3,4]) # Change the indexes
col_masses <- as.matrix(P1[4,1:3])
Q <- P - (row_masses %*% t(col_masses)) # %*% is matrix multiplication
```

- For each element in $Q$ divide the i-th row and j-th column by the square root of the product of the i-th row and j-th column masses to obtain $S$ (*S is your standardized masses*)

```R
d_row <- diag(as.vector(sqrt(row_masses)^(-1)))
d_col <- diag(as.vector(sqrt(col_masses)^(-1)))
S <- d_row %*% Q %*% d_col
```

>[!note] The sum of square of all elements in S is identical to the intertia

2) **Calculate** the [[Diagonalisation#Single Value Decomposition|singular value decomposition]] of **S**

Just note that in SVD, it does $U\Sigma V^{T}$, where the diagonals of $\Sigma$ are denoted as $\sigma_{i}$ (*the eigen values!*), the <b><span style='color: #FFD700'>sum of all</span></b> $\color{#FFD700}{\sigma^{2}_{i}}$ <b><span style='color: #FFD700'>is identical the the inertia</span></b>.

```R
# t is called transpose & if we take the eigen values from both they are the same
sst <- S %*% t(S) # The eigenvectors give U (Row)
sts <- t(S) %*% S # The eigenvectors give V (Column)

sst_eigen <- eigen(sst) # Use $values for eigenvalues & $vectors for the vectors
```

But <b><span style='color: #FFD700'>before we do SVD we need to find the eigen values</span></b> for $S$, meaning we need to solve $det(SS^{T} - \lambda I) = 0$.

Then we only keep the first $k$ terms in our singular value decomposition, this <b><span style='color: #98FB98'>retains as much of the inertia as possible</span></b>.

3) **Compute the coordinates of rows or columns in the lower-dimensional space**

>[!note] The row profiles in a lower-dimensional space are called principal coordinate for the rows and the columns are standard coordinates (*the opposite for column profiles*)

So if we are interested in comparing **row profile**, then we <b><span style='color: #FFD700'>reduce the number of columns</span></b>:
- The principal coordinates of rows are, $D_{r}^{-1/2}U_{k}\Sigma_{k}$
- The standard coordinates of columns are, $D_{c}^{-1/2}V_{k}$

So if we are interested in comparing **column profile**, then we <b><span style='color: #FFD700'>reduce the number of rows</span></b>:
- The principal coordinates of columns are, $D_{c}^{-1/2}V_{k}\Sigma_{k}$
- The standard coordinates of rows are, $D_{r}^{-1/2}U_{k}$

```R
# This is for column profile
eu <- d_row %*% sst_eigen$vectors # This gives the standard coordinates
ev <- d_col %*% sts_eigen$vectors %*% sts_eigen$values # This is prinsipal
```
# CA In R
---
## Getting The Contingency Table

To **get the contingency table** between 2 categorical variables we can use the `table` function:

```R
c <- table(df$col_1, df$col_2)
```

## Compute the Chi-Square Statistic

To **compute the chi-square statistic between 2 variables**, we can use the `chisq.test` function:

```R
chisq.test(df$col_1, df$col_2)
# You can also pass in a table as well so just chisq.test(c)
```
## Executing Correspondence Analysis

>[!note] You need to import the `ca` library

To **carry out CA**, we use the `ca` function:

```R
ca(contingency_table)
```

The **output** from `ca` tells us some stuff:
- It will show the various row and column statistics (*mass, chi square, inertia*)
- Inertia will show the variance explained by this level
- It also gives the principal inertia
- Dimensions (*where they sit on the dimension, so the closer the more corelated they are*)

>[!note] An average level be it row or col is one where the dimensions are close to the point (0, 0)

You can also get a summary of the CA using the `summary` function:

```R
summary(ca(contingency_table))
```

>[!note] The column `cum%` shows if we take the first n dimensions how much inertia it accounts for
>Same for **principal inertias** or the eigenvalues when printing `ca`, we just need to sum it up if we use this because this <b><span style='color: #FFD700'>gives the individual inertia</span></b> not cumulative.

Then we can **plot the principle coordinates & standard coordinates** using the `plot` function:

```R
plot(ca(contingency_table), map = 'rowprincipal') # Change to colPrinciple for principal coordinates as columns
# Without map, the the rows & col will be the principle coordinates
```

This plot is called a <b><span style='color: #87CEEB'>Biplot</span></b>. And now how to we **interpret it**:

![[Biplot Example.png|center]]

>[!note] This centroid though is some value but on the plot it will always be places at point (0, 0)

We want **points that are far apart from the centroid** as it tell us that <b><span style='color: #FFD700'>this category does not fit the average profile</span></b>.

The **distance between points** <b><span style='color: #FFD700'>tells us how similar they are</span></b>. For instance points A and B are similar to one another and Point B is more likely to see point Y as compared to point A (*but this is quite weak as A and B itself are close to each other meaning they are not that different*).

If they **are on the other side of the average profile** the <b><span style='color: #FFD700'>points are different based on the profile of that dimension</span></b>. So based on the first dimension, point A is different or repels point B.

If the **point is on average profile** then that <b><span style='color: #FFD700'>category does not give more information than the others</span></b>.

>[!warning] The plot does not show association
>Having <b><span style='color: var(--mk-color-red)'>2 points being close to each other does not mean that they have high association</span></b>.

## Merging Categories

You can do **merging of categories using clustering techniques** we just need to pass in the distance matrix:
```R
# Example of using hieratchical clustering
cluster <- hclust(dist(df), method = "complete")
plot(cluster, main = "Title", xlab = "x_label", ylab = "Distance")
```

Then we merge it as such:
```R
# An example replace the values based on the dataset
df_new <- data.frame(
  grp1 = colSums(df[c("Geol", "Phys", "Stat", "Math", "Engi"), ]),
  grp2 = colSums(df[c("Bioc", "Chem"), ]),
  grp3 = colSums(df[c("Zool", "Micr", "Bota"), ])
)
df_new <- as.data.frame(t(df_new))
```