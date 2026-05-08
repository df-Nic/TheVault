---
title: DL, NN & ML
Date Created: 2023-11-19
tags:
  - IS2238
  - AI
---
# Machine Learning (ML)
---
The idea of <span style='color:#0fb9b1'>ML</span> is to train using 

These <span style='color:#f7b731'>rules</span> are based on statistical methods or math

Process:
Big Data -> Learn from input data (<span style='color:#0fb9b1'>Feature Engineering</span>) -> Construct Model (Rules) -> Run the model (<span style='color:#0fb9b1'>Tuning</span>)

**Feature Engineering**
> Or feature extraction is the art of <span style='color:#f7b731'>formulating useful features from existing data</span> following the target to be learned and the machine learning model used

**Tuning**
> <span style='color:#f7b731'>Testing and setting the best parameters</span> (weight, value, coefficient) to define the model architecture

**Learning**
> Process of <span style='color:#f7b731'>determining a model that describes the data</span> and <span style='color:#0fb9b1'>optimising</span> that model

**Optimisation**
> <span style='color:#f7b731'>Reduce the error</span> between the predicted value and the actual value

The building of the <span style='color:#20bf6b'>analytical model is automated</span>, but one down side is that it is <span style='color:#eb3b5a'>unable to explain the logical reasoning behind its output</span> and the model <span style='color:#eb3b5a'>aims for accuracy rather than mathematical rigor</span>
## Types of Learning

### Supervised Learning

A machine learning approach that builds its model <mark class="hltr-orange">based on input and output data which is labeled</mark>

These labeled datasets are designed to train algorithms into <span style='color:#0fb9b1'>classifying</span> or <span style='color:#0fb9b1'>predicting</span> models. In addition, with labeled datasets the model <span style='color:#f7b731'>can measure its accuracy and learn overtime</span>

Types of <span style='color:#0fb9b1'>classification algorithms</span>: 
1) Linear Classifiers
2) Support Vector Machines
3) Decision Trees
4) Random Forest

<span style='color:#0fb9b1'>Prediction Algorithms</span>, for example the <span style='color:#f7b731'>regression algorithm</span>, understand the relationship between dependent and independent variables, and thus are <span style='color:#f7b731'>helpful for predictions on numerical values</span>

**Advantages & Disadvantages**
Labeled datasets are <span style='color:#eb3b5a'>expensive and requires effort to get</span>. It also has <span style='color:#eb3b5a'>very little responsiveness to new data</span> (Not effective). Also it <span style='color:#eb3b5a'>needs a lot of security</span> as input data is well-known and is labelled. However, the results from supervised learning are <span style='color:#20bf6b'>more accurate and reliable</span> because the data is well-known and labeled
### Unsupervised Learning

A machine learning approach that builds its model by <mark class="hltr-orange">analyzing, clustering and interpreting data based in its input only which is unlabeled</mark>

These types of algorithms <span style='color:#f7b731'>discover hidden patterns</span> or <span style='color:#f7b731'>inherent structure</span> in unlabeled data without human intervention (Validation of outputs still requires human intervention for improvements)

The process is known as <span style='color:#0fb9b1'>clustering</span> which is a <span style='color:#f7b731'>data mining technique for grouping unlabeled data</span> based on similarities or differences, which is <span style='color:#f7b731'>helpful for market segmentation or image compression</span>

**Advantages & Disadvantages**
Unlabeled datasets requires <span style='color:#20bf6b'>less effort to get</span>, can be <span style='color:#20bf6b'>adapted to new unlabeled datasets</span> however, the <span style='color:#eb3b5a'>results are less accurate and reliable</span> when compared to supervised learning unless there is some form of human validation. Also its <span style='color:#eb3b5a'>computationally complex</span> because they need a large training set to produce intended outcomes
### Semi-supervised Learning

It uses both the advantages of <span style='color:#0fb9b1'>supervised</span> and <span style='color:#0fb9b1'>unsupervised</span> learning by using a <span style='color:#f7b731'>small amount of labeled data with a large amount of unlabeled data</span> for training. This is known as <span style='color:#0fb9b1'>week supervision</span>

It combines the 2 data sets into a new dataset consisting on <span style='color:#f7b731'>pesudo-lable</span>

It <span style='color:#20bf6b'>reduces data acquisition costs</span> and also <span style='color:#20bf6b'>improves on the learning accuracy</span> as compared to unsupervised learning
### Reinforcement Learning

It is a method based on <span style='color:#f7b731'>rewarding desired behaviours or punishing undesired ones</span>

In general, a reinforcement learning agent is able to perceive and interpret its environment, take actions and learn through trial and error 

<span style='color:#0fb9b1'>Supervised learning</span> uses labeled data; <span style='color:#0fb9b1'>Reinforcement learning</span> uses reward (<span style='color:#f7b731'>action behavior</span>) data from the action of the agent in the given environment

Example: Alpha Go model is trained by playing games of Go multiple times (Trial and Error)

# Neural Network (NN)
---

Artificial neural network or ANN is a structure model <span style='color:#f7b731'>mimicking a neural network</span> in the brain

Currently there is no full understanding on how it mimics and the operation principle of each neutron is not known as it approximates the general <span style='color:#0fb9b1'>cognitive process</span>

The computer processes <span style='color:#0fb9b1'>cognitive processes</span> by using mathematical representations like weights or vectors for
more straightforward computation
# Deep Learning (DL)
---

It uses a <span style='color:#f7b731'>sufficiently deep artificial network</span> also known as <span style='color:#0fb9b1'>deep neural network</span> or DNN

It <span style='color:#f7b731'>leverages data by</span> multiple neural network layers and finds the best learning method

A <span style='color:#0fb9b1'>DNN</span> consists of
1) Input Layer
	  Assigns corresponding weights
2) Hidden Layers
	  As it traverses the many layers, connections with higher weights have more influence on the next layer of connections
3) Output Layer
	  This is the last layer where it compiles the weighted input to produce an output

<span style='color:#f7b731'>Sophistically of the problem</span> determines the <span style='color:#f7b731'>number of hidden layers</span>. A algorithm can have 1 hidden layer and it still a seep learning 

**Advantages**
- <span style='color:#20bf6b'>Elimination</span> of the need for data labeling
- <span style='color:#20bf6b'>Optimised</span> and has a very <span style='color:#20bf6b'>high accuracy</span>

**Disadvantages**
- Required a <span style='color:#eb3b5a'>very large dataset</span>
- Requires <span style='color:#eb3b5a'>computing ability</span> and data storage
- <span style='color:#eb3b5a'>Black box issue</span>
	 <span style='color:#f7b731'>Impossible</span> to look inside of it to <span style='color:#f7b731'>see how it works</span>, the reasoning of a neural network is embedded in the behaviour of its simulated neurons
## Recurrent Neural Network (RNN)

It uses a <span style='color:#f7b731'>recurrent structure</span> that takes its previous state as input and outputs it, <span style='color:#f7b731'>conveying information from a previous step to a current one utilising past data</span>

Application:
- Sentence Generation
- Machine Translation
- Well-suited for data with a <span style='color:#f7b731'>temporal flow</span>

However RNN struggles to <span style='color:#eb3b5a'>retain information over a long sequence</span> and it <span style='color:#eb3b5a'>can use a lot of memory</span>, thus variants like <span style='color:#0fb9b1'>LSTM</span> (Long short term memory) is developed to address this issue.

**LSTM**
> Distinguish between long-term and short-term memories, recoding them separately
## Convolution Neural Network (CNN)

Applies a convolutional <span style='color:#f7b731'>kernel</span> to input data to <span style='color:#f7b731'>extract features from images</span>, which is then proceeded through multiple neural networks and summarised for output

How the model <span style='color:#f7b731'>understands spatial structures</span> through operations like <span style='color:#f7b731'>convolution</span> and <span style='color:#f7b731'>pooling</span>, leveraging image features for accurate predictions

Application:
- Image Processing
# Recent Trends in DL Research and Applications
---
## Transformer

It is another ML architecture which is preferred because of its <span style='color:#20bf6b'>flexibility</span>, <span style='color:#20bf6b'>scalability</span> and <span style='color:#20bf6b'>performance</span>, which is mainly used to language translation

In a <span style='color:#0fb9b1'>transformer</span>, there is a <span style='color:#0fb9b1'>context vector</span> and a <span style='color:#0fb9b1'>fixed-length context vector</span>

**Context Vector**
> A <span style='color:#0fb9b1'>fixed length vector</span> that comes from the <span style='color:#f7b731'>last state of the encoder</span>, which aims to <span style='color:#f7b731'>represent a compressed form of the source sentence</span>

**Fixed-length context vector**
> It is limited in capturing all the information of the source sentences (Longer ones), it <span style='color:#f7b731'>encompasses all its complexities and nuances</span>

One downside to this is that there can be a <span style='color:#eb3b5a'>bottleneck</span> because the <span style='color:#0fb9b1'>context vector</span> needs to pass all the information through it, <span style='color:#eb3b5a'>deteriorating performace</span>. <span style='color:#f7b731'>One way is to use the source sentence as input with the help of parallel processing</span>. This allows the <span style='color:#f7b731'>words to be weighted</span>, giving them more attention to, enhancing performance

Unlike existing NN where its dependent on previous steps, <span style='color:#0fb9b1'>transformers</span> allow <span style='color:#f7b731'>parallel processing</span> of the entire sequence, leading to <span style='color:#20bf6b'>faster training times</span> with the help of modern GPUs. It <span style='color:#f7b731'>self-attention mechanism</span> allows the model to <span style='color:#20bf6b'>focus on different parts</span>, capturing long-ranged dependencies without the need of a recurrent layer

Thus this leads to <span style='color:#20bf6b'>higher accuracy</span> and <span style='color:#20bf6b'>faster training times</span>

## Generative AI

It is a model that focuses on <span style='color:#f7b731'>generating new data which shares the same characteristics</span> as existing data. They produce content (Text, images, music, videos) through existing datasets where its <span style='color:#f7b731'>output is novel</span>

In pre-training, it uses a lot of data and parameters and it is <mark class="hltr-orange">using unsupervised learning</mark>

**Discriminative Model**
> Used to <span style='color:#f7b731'>classify or predict</span> labels for data points where it is typically <span style='color:#f7b731'>trained on datasets with labels</span> and it <span style='color:#f7b731'>learns the relationship between the features of the data points and their labels</span>

**Generative Model**
> The generative model creates new data instances based on the <span style='color:#f7b731'>learned probability distribution of existing data</span>. Therefore, the generative model. <span style='color:#f7b731'>Creating new content</span>

Some drawbacks is that, <span style='color:#eb3b5a'>there is a limit</span> to the <span style='color:#f7b731'>number of tokens</span> (words) they <span style='color:#f7b731'>can process</span> at once. Also they <span style='color:#eb3b5a'>lack domain specific knowledge and understanding</span> for individual industry problems because they are built on general-purpose models. Thus <span style='color:#f7b731'>fine-tuning comes into play</span>

In summary, AI models especially Generative AI's, <span style='color:#f7b731'>learn from past data</span> where its <span style='color:#f7b731'>output is not always predictable</span>. With ample <span style='color:#f7b731'>learning</span> and <span style='color:#f7b731'>repetition</span>, its <span style='color:#f7b731'>performance will improve</span>.