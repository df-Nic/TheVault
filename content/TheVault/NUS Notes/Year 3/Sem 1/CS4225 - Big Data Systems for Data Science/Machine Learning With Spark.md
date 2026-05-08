---
title: Machine Learning With Spark
Date Created: 2025-10-15
Last Updated: 2025-10-17
tags:
  - CS4225
  - AI/ML
  - ApacheSpark/ML
---
# Introduction to Machine Learning
---
We use [[Year 2/Sem 1/CS2109S - Introduction to AI & Machine Learning/Introduction to Machine Learning & Decision Trees.md#Machine Learning|machine learning]] in various applications like:
- [[Year 2/Sem 1/CS2109S - Introduction to AI & Machine Learning/Logistic Regression.md#Classification|Classification]]
- [[Year 2/Sem 1/CS2109S - Introduction to AI & Machine Learning/Linear Regressions.md|Regression]]
- Object Recognition
- [[Year 2/Sem 1/CS2109S - Introduction to AI & Machine Learning/Introduction to Neural Networks.md|Neural networks]]

![[Typical ML Pipeline.png|center|500]]

>[!info] We will be focusing on classification & regression models

When we build a model we will spilt our data into 4 different categories
- **Features**, which is typically called $X_{train}$, is used to train the model
- **Labels**, which is typically called $Y_{train}$, is used to train the model
- **Testing data**, which is typically called $X_{test}$, is used to test the model to make predictions
- **Ground truth**, which is typically called $Y_{test}$, is used to compare the models predictions to evaluate how well fitted it is
## Data Preprocessing

But before training a model need to do something called <b><span style='color: #B0E0E6'>data preprocessing</span></b>. This is an important step since the **data is used to train the model** and thus it follows the concept of <b><span style='color: #F0E68C'>garbage in garbage out</span></b>.

>[!failure] Data preprocessing is the most time consuming part of the whole pipeline
>Because not only we need to clean the data we also need to understand the domain and business knowledge.
### Missing Values

Sometimes we might encounter **missing values**, so here are a few ways we can handle it:
- Remove rows with missing values
- Using mean or median for that attribute (*of the column*)
- Fitting a regression model to predict the missing attribute
- Adding a new column as a dummy variable to indicate of there are missing values or not
### Handling Categorical Data

Most machine learning models will <b><span style='color: var(--mk-color-red)'>not accept categorical data</span></b>, most specifically **strings/text**. So some things we can do is to:
- Convert categorical data into numbers (*mapping 1 number to 1 category*) called <b><span style='color: var(--mk-color-turquoise)'>categorical encoding</span></b>
- [[Year 2/Sem 1/CS2109S - Introduction to AI & Machine Learning/Neural Network on Sequential Data.md#One-hot Encoding|One hot encoding]]

>[!info] One hot encoding is useful if there is no ordinal relationship among categories
>Ordinal relationship means some ordering, for instance low, medium, high.

By **transforming it into numerical values**, it lets us <b><span style='color: #F0E68C'>apply algorithms which typically handle only numerical features</span></b>.
### Normalisation

The goal of normalisation is to <b><span style='color: #F0E68C'>scale down the range of values to a smaller range</span></b>.

There is a few ways of doing this:
1) **Clipping**
Which is just <b><span style='color: #F0E68C'>removing data outside the new range of values</span></b>.

>[!example] Example of clipping
>Lets say our dataset has a range of 0 to 1000 for a given feature (*column*).
>
>We cant to clip it so it will be between ranges 250 to 750. Then all the rows who's given feature value is 0 to 249 or 751 to 1000 will be removed.

2) **Log transformation**
$$
log(1 + x)
$$

3) **Standard scaler**
$$
\frac{x - mean(x)}{std(x)}
$$

Where: 
- $std$ is the standard deviation

4) **Max min normalisation**
$$
\frac{x - min(x)}{max(x) - min(x)}
$$
# Training A Model
---
Here we will use the  [[Year 2/Sem 1/CS2109S - Introduction to AI & Machine Learning/Logistic Regression.md#Classification|logistic regression model]] as an example to show how **build a model**.

In a logistic regression model it uses the <b><span style='color: #87CEEB'>sigmoid function</span></b> to <b><span style='color: #F0E68C'>calculate the probability</span></b> that the input data is in this category or not.

$$
\sigma(x) = \frac{1}{1 + e^{-x}}
$$
So typically anything that is **0.5 and above is considered as the data being in this category** else it is not.

For each feature the model will have **parameters** for it and this is called <b><span style='color: #B0E0E6'>weights</span></b> and a special one called <b><span style='color: #B0E0E6'>bias</span></b>.
<div style="page-break-after: always;"></div>

>[!info] These parameters are used to compute the prediction based on a given input
>The **formula to make a prediction** in a logistic model is:
>$$
> \hat{y} = \sigma (x \cdot w + b)
>$$
>Where:
>- $x$ and $w$ are vectors, $x$ are the inputs and $w$ are the weights
>- $\cdot$ is to denote matrix multiplciation
>
>So assuming we have 2 weights and the bias is -5. If we have a input of 5 and 2 then $\hat{y} = \sigma(5 \times 2 + 2 \times 2 - 5) = 1/1+e^{-4} = 0.982$
## Gradient Descent

So where do these weights and biases come from? The model uses a <b><span style='color: #B0E0E6'>loss / cost function</span></b>, which our **logistic regression uses** the [[Year 2/Sem 1/CS2109S - Introduction to AI & Machine Learning/Logistic Regression.md#Cross Entropy|cross entropy loss]]

So the model during training here is what the model does:
- It will predict a set of values
- They will compare the values with the labels in the training data
- From here they can <b><span style='color: #F0E68C'>compute the loss score based on this comparison</span></b>

>[!info] So the goal is to minimise the score that you get from the loss function
>
>The <b><span style='color: #98FB98'>lower the score the more accurate</span></b> it is.

To reach this minimum we do [[Year 2/Sem 1/CS2109S - Introduction to AI & Machine Learning/Linear Regressions.md#Gradient Descent|gradient descent]]. We <b><span style='color: #F0E68C'>start at an arbitrary point and by calculating the gradient</span></b> we can follow it (*repeat the process*) until the **minimum is reached** or the **change in our change in our weights is minimal**.

**This is the update rule**
$$
w_{new} = w_{old} - \alpha \nabla J(w_{old})
$$
Where:
- $w$ is the vector of all the weights
- $\alpha$ is the step size which determines how much you want to reduce
- $\nabla$ is the gradient or slope

Then **to update the weights vector in a logistic regression**
$$
w_{old} = w_{new} - \alpha \sum_{j = 1}^{n} [\sigma(x^{(j)} \cdot w_{old} ) - y^{(j)}]x^{(j)}
$$
Where:
- $n$ is the number of training samples

So since we are doing this **gradient descent continuously**, **Spark** can be useful since we can <b><span style='color: #F0E68C'>cache training data</span></b> and the <b><span style='color: #F0E68C'>weights will be broadcasted to the workers</span></b>.

So now the <b><span style='color: #98FB98'>gradient descent can be done in parallel</span></b> (*parallel gradient descent*).
- Each worker can compute the loss function $[\sigma(x^{(j)} \cdot w_{old} ) - y^{(j)}]x^{(j)}$ for a subset of the training data, this is the `map`
- Then for `reduce` we can just sum the results from the map step
## Evaluation

### For A Classification Model

![[Images/CS2109S Images/Confusion Matrix.png|center]]

>[!note] F1 score is the harmonic mean of precision and recall
### For A Regression Model

We have a few ways to evaluate, the <b><span style='color: #98FB98'>lower the better</span></b>:

1) **Mean square error**
$$
\text{Mean Squared Error} = \frac{1}{N} \sum^{N}_{i = i} (\hat{y_{i}} - y_{i})^{2}
$$
Where:
- $\hat{y}$ is the predicted $y$ value

2) **Root mean square error**
Just take the square root of mean square error.

3) **Mean absolute error**
$$
\text{Mean Absolute Error} = \frac{1}{N} \sum^{N}_{i = i} \vert\hat{y_{i}} - y_{i}\vert
$$

4) **R square value**
$$
R^{2} = 1 - \frac{\text{RSS}}{\text{TSS}}
$$

$$
\text{RSS} = \sum^{n}_{i = 1} (Y_{i} - \hat{Y}_{i})^{2}
$$

$$
\text{TSS} = \sum^{n}_{i = 1} (Y_{i} - \bar{Y})^{2}
$$
Where:
-  $\bar{Y}$ is the **mean** of the actual Y

The [[Year 2/Sem 1/DSA3361 - Inferential Data Analytics/Linear Regression.md#Step 3 - Getting model coefficients|value is between 0 to 1]].

>[!important] Only for R square value the higher the better

# Machine Learning Pipeline
---
We want to build a complex pipeline out of **simple building blocks** like, encoding, normalisation, feature transformation and model fitting. <b><span style='color: #F0E68C'>Without a pipeline, most of the code will be repeated</span></b>.

>[!success] Better code reuse in different stages of the model building

>[!success] Easier to perform cross validation & hyperparameter tuning
## Transformers

In our pipeline a transformer is to transform or <b><span style='color: #F0E68C'>map one data frame to another</span></b>. This is usually **used in data pre-processing**.

>[!example] Examples of transformers
>- One-hot encoding
>- Tokenisation
>- Or some object which has the `transform()` function which performs it
>  
>  So in our **logistic regression model example**, lets say we have our model already then:
>- We will convert raw text into words first using a tokenizer
>- Then we will use HashingTF to convert words to feature vectors
>- Then lastly we will use our model to convert the feature vectors to predictions

Generally these transformers output a new data frame and <b><span style='color: #F0E68C'>append it to the original data frame</span></b>.

>[!info] A fitted model is a transformer
>It basically takes a data frame and transform it into a set of predictions and appends it with the training data.
## Estimator

It is an <b><span style='color: #F0E68C'>algorithm which takes in data and outputs a fitter model</span></b>. We can tell what model we want Spark to train then just provide the data and Spark will return us a trained model.

We can do it as such:
```python
from pyspark.ml.classification import LogisticRegression
training = spark.read.format("libsvm").load("some data")
lr = LogisticRegression(maxIter=10)
lrModel = lr.fit(training) # This returns a transformer
```

So the `fit()` function **initiates the training** and in return it will return back a transformer which is our fitted model.
<div style="page-break-after: always;"></div>
## Putting Together In Training Time

![[Estimator Pipeline for ML.png|center]]

When we **first make the pipeline**, it will be an <b><span style='color: #B0E0E6'>estimator pipeline</span></b>. Because during train time we are transforming the data and fitting our model.

This essentially happens when the command `pipeline.fit()` is executed.

![[Transformer Pipeline in ML.png|center]]

After the fitting phase, the `pipeline.fit()` function will not only **return** the fitted model but the <b><span style='color: #F0E68C'>whole pipeline with a series of transformer blocks and the fitted model</span></b>, this is known as a <b><span style='color: #B0E0E6'>transformer pipeline</span></b>.

The return type is of type `PipelineModel`.

From here you can see how pipeline can <b><span style='color: #98FB98'>help reuse code</span></b>, as now we can <b><span style='color: #F0E68C'>use this pipeline and input data to make predictions</span></b>, which can be done by executing the `pipelineModel.transform()` which calls each stages `transform()`.

