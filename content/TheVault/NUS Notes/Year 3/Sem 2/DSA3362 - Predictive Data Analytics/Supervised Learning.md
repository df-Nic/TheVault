---
Title: Supervised Learning
Date Created: 13-January-2026
Last Updated: 08-March-2026
Tags:
  - DSA3362
  - AI/ML
---
# Supervised & Unsupervised Learning
---
In machine learning a **model can learn in 1 of 2 ways**:
1) **Unsupervised**: Data is <b><span style='color: #FFD700'>not labelled</span></b> & the model requires to understand patterns / underlying structure of the data
2) **Supervised**: Data <b><span style='color: #FFD700'>is labelled</span></b> & the model is looking for relationships between input & output variables (*labelled*)
## Supervised Learning

As mentioned previously, the model looks for relationships between input & output variables.

>[!note] Input variables are also known as the following
>Predictor variables, independent variables or features.

>[!note] Output variables are also known as the following
>Response variables, dependent variables or label.

Depending on the **nature of the output variable** supervised learning can be subdivided into:
1) **Regression**: The output variable is <b><span style='color: #FFD700'>continuous</span></b>
2) **Classification**: The output variable is <b><span style='color: #FFD700'>categorical</span></b>

>[!info] There are 2 types of classifier for classification models
>1) **Soft** classifier are those that <b><span style='color: #FFD700'>gives probability</span></b> for this label
>2) **Hard** classifier are those that <b><span style='color: #FFD700'>tells you what label it is</span></b>
### Parametric & Nonparametric Models

Depending on **how the model expresses the relationship** between input & output variables it can be divided into:
1) **Parametric**: Expresses the relationship within a <b><span style='color: #FFD700'>fixed set of parameters</span></b>
2) **Nonparametric**: It <b><span style='color: #FFD700'>estimates the relationship based on the data itself</span></b>

>[!warning] Parametric models tend to exhibit more bias than nonparametric models
>This is because the <b><span style='color: var(--mk-color-red)'>expressed relationship may not be the same as the true relationship</span></b>.

>[!warning] Nonparametric models tend to exhibit more variance
>
>This is because <b><span style='color: var(--mk-color-red)'>output varies from dataset</span></b> to dataset.
# Evaluation Metrics
---
## For Regression Models

Given our predicted values for $Y$ which we denote as $\hat{y}$. We need to **gauge the performance** of the model.

First we need to compute what is known as <b><span style='color: #87CEEB'>residual</span></b> (*or error*):
$$
\text{Residual} = y_{n} - \hat{y_{n}}
$$
With this we can compute various evaluation metrics:
$$
\text{Residual sum of squares (RSS)} = \sum^{n}_{i = 1} (y_{i} - \hat{y_{i}})^{2}
$$
$$
\text{Mean squared error (MSE)} = \frac{1}{n} \sum^{n}_{i = 1} (y_{i} - \hat{y_{i}})^{2}
$$
$$
\text{Root mean squared error (RMSE)} = \sqrt{\frac{1}{n} \sum^{n}_{i = 1} (y_{i} - \hat{y_{i}})^{2}}
$$
$$
\text{Mean absolute error (MAE)} = \frac{1}{n} \sum^{n}_{i = 1}  \vert y_{i} - \hat{y_{i}} \vert
$$
$$
\text{Mean absolute percentage error (MAPE)} = \frac{1}{n} \sum^{n}_{i = 1}  \vert \frac{y_{i} - \hat{y_{i}} }{y_{i}}\vert
$$
>[!success] For all of these metrics the lower the better
## For Classification Model

Since the output is categorical, the concept of residuals does not exist. Thus given $n$ categories we can have a $n$ by $n$ <b><span style='color: #87CEEB'>confusion matrix</span></b>.

**Example of a confusion matrix with 2 categories**:

![[Images/DSA3362 Images/Confusion Matrix.png|center|300]]

With this we can compute various evaluation metrics:
$$
\text{Accuracy} = \frac{TP + TN}{TP + TN + FP + FN}
$$
>[!success] The closer accuracy is to 1 the better the classification model

$$
\text{Recall} = \frac{TP}{TP + FN}
$$
For **recall** we are interested to see the predictions, <b><span style='color: #FFD700'>condition on the true label</span></b> (*correct category*) <b><span style='color: #FFD700'>being positive against all the predicted labels that are positive</span></b>.

>[!info] Recall is also known as sensitivity or true positive rate (TPR)

$$
\text{Precision} = \frac{TP}{TP + FP}
$$
For **precision** we are interested to see the predictions, <b><span style='color: #FFD700'>condition on the predicted label being positive</span></b> and see which of these are <b><span style='color: #FFD700'>predicted correctly</span></b>.

>[!info] Precision is also known as positive predicted value (PPV)

$$
\text{Specificity} = \frac{TN}{TN + FP}
$$

For **specificity** we are interested to see the predications <b><span style='color: #FFD700'>condition on the true label being negative against all the predicted labels that are negative</span></b>. 

>[!info] Precision is also known as the true negative rate (TNR)

$$
\text{F1 Score} = 2 \times \frac{\text{Precision} \times \text{Recall}}{\text{Precision} + \text{Recall}}
$$
>[!info] For F1 score to be 1 precision and recall must be close to 1
>This <b><span style='color: #98FB98'>balances precision & recall</span></b>, as typically <b><span style='color: #FFD700'>one affects the other</span></b>.


