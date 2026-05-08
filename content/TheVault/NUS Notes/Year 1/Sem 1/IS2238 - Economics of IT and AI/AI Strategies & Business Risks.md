---
title: AI Strategies & Business Risks
Date Created: 2023-11-20
tags:
  - IS2238
  - Economics
  - AI
---
# Algorithm Economy
---
**Algorithm**
> A <span style='color:#f7b731'>step by step procedure or rules</span>, to be followed in calculations or problem-solving operations, often used by computers

**Algorithm Economy**
> The evolving state of businesses where <span style='color:#0fb9b1'>algorithms</span> are at the <span style='color:#f7b731'>core of value creation</span>

Companies design, build and leverage algorithms to 
1) <span style='color:#f7b731'>Differentiate</span> themselves
2) Make business processes <span style='color:#f7b731'>more efficient</span>
3) <span style='color:#f7b731'>Create new</span> products or services
4) Deliver <span style='color:#f7b731'>better customer experience</span>
5) Enhances<span style='color:#f7b731'> response speed and efficiency</span>
6) <span style='color:#f7b731'>Creation </span>of business value

Companies using AI can lead to a <span style='color:#20bf6b'>reduction in transaction cost</span> and <span style='color:#20bf6b'>enhancement of welfare for suppliers and consumers</span>

Currently global companies are <span style='color:#f7b731'>creating value</span> through the usage if AI algorithms. Those who do not can find themselves having a competitive disadvantage in the long run

**Types of AI companies**
1) Horizontal AI
	  Refers to AI solutions designed to provide <span style='color:#f7b731'>generalized capabilities across multiples industries or domains</span> (General purpose chatbots)
2) Vertical AI
	  AI solutions which are designed for a <span style='color:#f7b731'>specific industry or task</span>
3) Service Base
	  Providing Services to their customers
4) Tech Base
	  Owns their own IT solutions

Example: 
- Amazon's Inferentia which is a ML inference chip to <span style='color:#20bf6b'>deliver high performance at low costs</span> for applications which requires several ML operations. Applications like snapchat and Airbnb are using it
- Amazon's SageMaker, which is a studio to use purpose-built tools to perform ML

# Risks of Using AI
---
## Data Acquisition 

It is <span style='color:#eb3b5a'>difficult to get labeled datasets</span> and it is also hard to get experts and collect data. <span style='color:#f7b731'>Statistical measurement</span> of quality<span style='color:#eb3b5a'> requires huge cost</span> to <span style='color:#f7b731'>determine the right data</span> set and <span style='color:#f7b731'>preventing bias problem</span>

**Ways to resolve this issue**
- Use <span style='color:#f7b731'>reinforcement learning</span>, allowing AI to self-learn to maximise cumulative rewards based on desired actions through trial an error
- <span style='color:#0fb9b1'>Transfer learning</span>, where a <span style='color:#f7b731'>trained model is transferred to another similar domain</span>

How does <span style='color:#0fb9b1'>transfer learning</span> work;
- Uses a already <span style='color:#f7b731'>pre-trained model that is similar in characteristics</span>
- Usually only the first few layers are extracted as the <span style='color:#f7b731'>first few layers are trained to identify general features</span>, and the final layers are more specific

**Strategies for Transfer Learning**
1) <span style='color:#f7b731'>Using only the architecture</span> of the pre-trained model. It is essentially using the model and training it on a new dataset, thus a <span style='color:#eb3b5a'>large dataset is needed</span> and a <span style='color:#eb3b5a'>good computational capabilities</span> (Train the entire model)
2)  <span style='color:#f7b731'>Using only general layers</span> (First few) and regenerate specific layers, it can work if the <span style='color:#eb3b5a'>problem is similar with little differences</span> and requires <span style='color:#eb3b5a'>caution reguarding the learning rate</span> (Train some and leave the other frozen)
3) <span style='color:#f7b731'>Only the classifier is used</span>, this can be used when the <span style='color:#f7b731'>dataset is small or computational resources is limited</span>. This will work if the <span style='color:#eb3b5a'>problem is very similar</span> to the dataset the pre-trained model was trained on (Freeze the convolution base)

## Lack of Explainability

Adding more data and using a variety of algorithms can <span style='color:#f7b731'>hinder explainability</span> (reason for the AI result) and <span style='color:#f7b731'>introduce biasness </span>

Explainable artificial intelligence (XAI), is a set of processes and methods <span style='color:#f7b731'>allowing humans to comprehend and trusts the results</span> from ML. XAI can also be <span style='color:#f7b731'>used</span> to <span style='color:#f7b731'>describe am AI model</span> and its <span style='color:#f7b731'>expected impact and potential biases</span>

An AI model that is explainable can <span style='color:#f7b731'>distinguish between meaningful and safe prediction strategies</span>

The <span style='color:#2d98da'>black box problem</span>, where a sophisticated model is unexplainable, which <span style='color:#f7b731'>limits the applicability of AI models</span> especially when it can lead to a serious problem

<span style='color:#2d98da'>LIME</span> (Local Interpretable Model - Agonistic Explanations). It is where each features is given a unique weight and is then retrained to check for the outcomes

## Consumer Reactions

It is the attribution of <span style='color:#f7b731'>human-like qualities on nonhuman entities</span>. Another word for this is <span style='color:#0fb9b1'>anthropomorphism</span>

Consumers react differently to AI in different contexts

The <span style='color:#0fb9b1'>uncanny valley </span> is used to <span style='color:#f7b731'>describe robots that appear more humanlike</span> they become more appealing <span style='color:#f7b731'>up till a certain point</span>. Anything <span style='color:#f7b731'>beyond this point, people will start to have a negative reaction</span> to these life like robots

In other terms, it is the hypothesized relation between an <span style='color:#f7b731'>object's degree of resemblance to a human</span> being and the <span style='color:#f7b731'>emotional response to the object</span>

Designers or developers may make certain characteristics more realistic or exaggerate them to avoid <span style='color:#0fb9b1'>uncanny valley</span>. Height as well is important where shorter robots are more appropriate (Avg 105cm is good, 158cm is bad)

<span style='color:#f7b731'>Not knowing</span> that something is <span style='color:#f7b731'>a robot</span> can <span style='color:#f7b731'>affect a humans decision making</span>. This is because, humans perceive robots as <span style='color:#f7b731'>less knowledgeable and less empathetic</span>

<span style='color:#f7b731'>On the contrary</span> a fully human-like chatbot without disclosure was perceived to be significantly less likeable (79.7%) than the same chatbot incorporating disclosure

In this context, users can very <span style='color:#f7b731'>quickly deduce that the agent is not human</span>, based on its conversational behavior (even without disclosure).

Thus, when the chatbot initially <span style='color:#f7b731'>presents a human name,</span> this may <span style='color:#f7b731'>create an expectation of human interaction</span>, only to be let down shortly thereafter when the customer perceives that responses are automated.