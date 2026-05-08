---
title: Foundations of Large Language Model
Date Created: 2025-08-14
Last Updated: 2025-09-28
tags:
  - CS6101
  - AI/ML/NN/LLM
---
# Overview of LLMs
---
>[!question] What is a LLM
>
>LMM or <b><span style='color:var(--mk-color-turquoise)'>large language model</span></b>. Is a large model with possibly more than millions of parameters.
>
>It <b><span style='color:var(--mk-color-yellow)'>operates on conditional probability</span></b>, taking a set of tokens (*set of words*) and outputting the most probable next token. 

There are 3 steps to making a LLM model:
1) Pre-training
2) Supervised fine-tuning
3) Post training

>[!important] Between these 3 steps, the implementation details are important
>
>From the data, to the architecture & the fine-tuning, there are <b><span style='color:var(--mk-color-yellow)'>many techniques but it will affect the LLM</span></b>.
>
>How does it affect?:
>- Text Coherence & Translation Ability
>- Long-Context Performance
>- Memorization Capacity
>- Factual Accuracy
>- Ability to Call the Appropriate Tools
## Pre-Training

At this stage we are **collecting a large training dataset** which is known as a <b><span style='color:var(--mk-color-turquoise)'>corpus</span></b> & train a model with it (*seq2seq training*).

>[!warning] A typical corpus for LMMs are massive, requiring a few terabytes of storage
>
>Since it is massive, people <b><span style='color:var(--mk-color-red)'>do not vet or curate the data</span></b>, they just use it.

The model now trains through <b><span style='color:var(--mk-color-yellow)'>self-supervision</span></b> to predict the next token, learning rules & patterns to understand the world.

>[!info] Self-supervised learning
>
>Essentially the model will be <b><span style='color:var(--mk-color-yellow)'>tested based on the given corpus</span></b>.
>
>It can be through **autoregressive inputs**, like given a sentence <b><span style='color:var(--mk-color-yellow)'>predict the next word</span></b>.
>
>Or it can through a **masked input**, where we mask some words in a sentence and ask the model to <b><span style='color:var(--mk-color-yellow)'>predict the masked words</span></b>.
## Supervised Fine-Tuning

Now with a base LLM, it does <b><span style='color:var(--mk-color-red)'>not really specialize in a particular task</span></b> as its just have general knowledge based on the corpus.

This is where **supervised fine-tuning** comes in, it is essentially <b><span style='color:var(--mk-color-yellow)'>curated smaller datasets for the model to adapt to a specific task</span></b> (*Tailored  the response to the user's desired preference*).

>[!note] Leveraging structured examples
>
>These datasets may contain, **chain of thought traces** or **instruction output pairs**.

>[!example] Examples of additional seq2seq training
>
> - Instruction following SFT
> - Tool call SFT
> - Task-specific SFT
> - PEFT

If we do not do this, the <b><span style='color:var(--mk-color-red)'>knowledge it has is indiscriminately & probabilistically</span></b> baked into the mode.
- And it is very <b><span style='color:var(--mk-color-red)'>hard to under learn</span></b> (*forget*) and <b><span style='color:var(--mk-color-red)'>edit</span></b> the existing knowledge.
## Post-Training

In post training, we will have models which are proficient in generating text or caring out a specific task.

Our focus now is to <b><span style='color:var(--mk-color-yellow)'>align the model's behaviour with user expectations</span></b> (*Detailed response, reasoning, examples*).

>[!failure] This is the most methodologically diverse training stages

One popular method of post-training is <b><span style='color:var(--mk-color-yellow)'>reinforcement learning</span></b>, which can be done through:
- Human preferences or RLHF (*asking their response if its helpful, harmless, honest or which response is better*)
- Verifiable rewards or RLVR (*simple & effective*)

>[!abstract] Verifiable rewards
>
>It essentially a <b><span style='color:var(--mk-color-yellow)'>simple yes, no signal</span></b> to a response to check its accuracy or not.
>
>For instance it can use a external verifier to check math problems, if the output is correct the model will get a "yes" signal and if its wrong it will get a "no" signal in which the model will then correct itself.

>[!failure] Impacts on post-training
>
> - Increased hallucinations
> - Alignment tax (*AI safety*)
> - More effort in adapting models
# LLM Bottlenecks
---
## Prevalence of Factual Errors

When we talk about **factuality** in LLM, it is the <b><span style='color:var(--mk-color-yellow)'>generation of consistent content with factual & world information</span></b>.

>[!info] Hallucination
>
> When LLMs produce <b><span style='color:var(--mk-color-yellow)'>baseless or untruthful content</span></b> (*Not even back by any source*).

>[!info] Factuality Errors
>
>When a model <b><span style='color:var(--mk-color-yellow)'>fails to accurately learn & utilize factual knowledge</span></b>.
>
>You can think of this as, it was thought that 1 + 1 = 2 but it output 3.
>
>In multimodal LLMs there are:
>- Existence factuality (*Incorrect facts about images*)
>- Attribute factuality (*Describing facts wrongly on certain objects*)
>- Relationship factuality (*False descriptions of relationships between objects*)

>[!info] Factuality Hallucination
>
>A subset of hallucinations where the model, generates content that <b><span style='color:var(--mk-color-yellow)'>looks factual but is actually false</span></b>.

LLM's is found to have <b><span style='color:var(--mk-color-red)'>trouble with generating content</span></b> related to less well know information (*long tail knowledge*). 

>[!note] FACTSCORE
>
>It is a **factual evaluation metric** which takes a bunch of atomic facts (*just some factual question*) and check if its response is correct or not.

What causes these factual errors:
- Inaccurate or outdated training data
- Ambiguous prompts & lack of specificity
- Limitations in retrieval & knowledge retention
- Overgeneralisation with closest related patterns (*Co-occurrence bias: prefer frequently occurring words*)
- Errors in knowledge integration
### Improving Factuality

In general, to improve the model, we can always do fine tuning by adding more specialised data or through correcting outputs (*inference time correction*).

1) **Scaling the dataset**
Just <b><span style='color:var(--mk-color-yellow)'>collect more data or increase the diversity</span></b> of the dataset.

>[!warning] Model gains
>
>By doing this, do not expect the model to improve significantly.
>
>**More data** results in <b><span style='color:var(--mk-color-red)'>small accuracy gains</span></b> while more **diversity** might <b><span style='color:var(--mk-color-red)'>not improve</span></b> due to corelated sources.
  
2) **Scaling the model**
<b><span style='color:var(--mk-color-yellow)'>Increase the number of parameters</span></b> that the model uses.

>[!warning] Might be resource intensive
>
>Most **scaling only improves performance for questions with high popularity**.
>
>To improve on long-tail questions we might need $10^{9}$ parameters to have some levels of accuracy.
   
3) **Changing training objectives**
We can <b><span style='color:var(--mk-color-yellow)'>change how we train the model</span></b> on the dataset.

Instead of 1 epoch we can **run for several epochs** to <b><span style='color:var(--mk-color-green)'>allow the model to memorise as much as possible</span></b>.
  
4) **Retrieval augmented generation**
**Non-parametric** memories can <b><span style='color:var(--mk-color-red)'>impede</span></b> the models accuracy.

>[!info] Parametric & non-parametric memory
>
>**Non-parametric** memory is just <b><span style='color:var(--mk-color-yellow)'>data being stored in a databank</span></b>.
>
>**Parametric** memory, is where <b><span style='color:var(--mk-color-yellow)'>data is mapped to some set of parameters</span></b> which can be though of like indexing. If a topic requires information they can parse the input into an index and retrieve information using this index. 

But it is **not always the case to use parametric over non-parametric memory** (*there are tradeoffs*).

Thus <b><span style='color:var(--mk-color-turquoise)'>adaptive retrieval</span></b> can be used, where its just a classifier on when to use parametric over non-parametric memory.
## Difficulty of Verification

>[!question] Why is verification important?
>
>The main idea is that it <b><span style='color:var(--mk-color-green)'>prevents misinformation & ensuring reliable deployment</span></b>.
>
>It can also prevent harmful, biased or dangerous content from being spread.
### Black Box Problem

As you have seen in papers an LLM model is <b><span style='color:var(--mk-color-yellow)'>modeled as a black box</span></b>. And it is also probabilistic, meaning it is <b><span style='color:var(--mk-color-red)'>non-deterministic</span></b>.

>[!info] Non-deterministic
>
> It means given the <b><span style='color:var(--mk-color-yellow)'>same input, it might return a different result</span></b>. 

This it is <b><span style='color:var(--mk-color-red)'>hard to make a validation system</span></b> due to the ever changing responses by LLMs.

Due to it being a black box, it makes it <b><span style='color:var(--mk-color-red)'>hard to understand the internal working and reason about its correctness</span></b>:
- Debugging is also hard
- Understanding the source of hallucinations is hard
### Dynamic Nature of Truth

It essentially targets the fact that some **information** is not static and will <b><span style='color:var(--mk-color-yellow)'>change over time</span></b>.

>[!example] One example will be the prime minister of Singapore, it will change as time passes

The LLM <b><span style='color:var(--mk-color-yellow)'>knowledge base is quite static</span></b> and this leads to a number of <b><span style='color:var(--mk-color-red)'>issues</span></b> like:
- Outdated information
- Lack of real-time or recent information
- Sources are not available
### Contextual Understanding & Domain Knowledge

To get a good response, the model must first understand the query and also know what information is relevant.

The issue with most LLMs is the <b><span style='color:var(--mk-color-red)'>understanding of the context of the query</span></b>.

And even if the model understands the query it must have <b><span style='color:var(--mk-color-red)'>specialised knowledge of the domain</span></b>, if not it will never output accurate results.
### Ethics & Biases

A LLM model gets its output from the dataset it was trained on, thus it is possible that there can be some biases.

>[!success] Verification methods can perpetuate these biases, creating systematic blind spots in what gets validated as the truth

Even with verification systems, they do face <b><span style='color:var(--mk-color-red)'>difficulties</span></b>:
- Systemic bias propagation (*Systems can favour some perspectives, viewpoints, demographics*)
- Cultural & linguistic hegemony (*Devalue sources from other cultures or demographics*)
- Historical bias perpetuation (*Validate claims based on historical data which can be harmful or discriminatory*)
- Marginalised voiced suppression (*Claims from less well known communities can be flagged as unverifiable*)
## Difficulty of Data Opt-Out

The capabilities of an LLM can be associated with <b><span style='color:var(--mk-color-yellow)'>scaling</span></b>. A <b><span style='color:var(--mk-color-green)'>high performing model</span></b> requires a <b><span style='color:var(--mk-color-red)'>large training corpora</span></b>.

>[!info] Scaling through a larger dataset or more parameters

We can also **improve** the LLM's ability to **memorise training data** by:
- Having a larger model
- More frequent examples (*or data*) will be more likely to be remembered
- The ability to extract memorised text increases with the number of tokens in the context

Most of the **data used** to train the model is through <b><span style='color:var(--mk-color-yellow)'>web-scrapping</span></b> (*from websites, forums, codebases, etc*).

>[!warning] LLMs can memorise undesirable content
>
>From web-scrapping, we can <b><span style='color:var(--mk-color-red)'>unintendedly get unwanted data</span></b> like generalisation, toxic content, private data, copyrighted context.

How can we "unlearn" these data, we first **need to know what needs to be unlearned** and then we can <b><span style='color:var(--mk-color-yellow)'>add a punishment</span></b> for the model if it uses it.

>[!abstract] SILO language models
>
> We initially train the model using publicly available data from credible and licenced sources, then for our test-time, the data store can contain all the external information allowing us to unlearn if needed.  
## Adaption & Un-Adaption

For a LLM to expand its knowledge we can use the following methods:
1) **Continual learning**
2) **Model editing**
3) **Retrieval-based methods** (*This is RAG which will not be covered*)
### Continuous Learning

Instead of retraining the large mode, we can just <b><span style='color:var(--mk-color-yellow)'>fine-tune the model only on the new set of data</span></b>.

>[!success] Maintains model's generalisation while updating facts

This is useful in:
- Domain adaptation
- Temporal updates (*New information that just came into light*)
- Learn a new skill or language

However this will cause <b><span style='color:var(--mk-color-red)'>catastrophic forgetting</span></b>.

>[!failure] Catastrophic forgetting
>
>When **fine-tuning on new data**, the model will often <b><span style='color:var(--mk-color-red)'>lose prior knowledge</span></b>.
>
>This requires a <b><span style='color:var(--mk-color-yellow)'>retaining on the old data</span></b> to preserve it, which <b><span style='color:var(--mk-color-red)'>increases training volume & computing cost</span></b>.

To solve this issue we can <b><span style='color:var(--mk-color-green)'>add parts of the original data</span></b> into the fine-tuning dataset.

>[!info] Self-synthesized rehearsal (SSR)
>
>Instead of fetching the original data, we can <b><span style='color:var(--mk-color-yellow)'>use the model to generate data</span></b>.
>
>But this <b><span style='color:var(--mk-color-red)'>adds extra compute during data generation & re-training</span></b>.
### Model Editing

Instead of editing the whole model, why not <b><span style='color:var(--mk-color-yellow)'>target a small segments of the model</span></b> to alter the facts and its behaviour.

Some ways it can be done is through
- **Gradient based editing** (*Training a small auxiliary network*)
- **Locate-and-update methods** (*Finds layers or neuron clusters that encode a specific fact , then applies low-rank updates in those targeted regions*)

>[!warning] These techniques does not mean it uses less computing power
>
>Yes in some cases since we are targeting a few layers or weights, the computing power needed is lesser.
>
>But scaling that for a larger model, it will still be costly.

>[!failure] Unknowingly alter other knowledge in the model 

>[!failure] General capabilities can be eroded

>[!failure] May create internal knowledge conflicts

>[!failure] Issues arise with more & more facts
## Prohibitively Large Model Size

**Scaling** the model lead to <b><span style='color:var(--mk-color-green)'>improved performance</span></b> as compared to algorithmic advances.

**Scaling laws**
- The "Kaplan" scaling law states that as pre-training budget increases the model size should be scaled more than the data
- The "Chinchilla" scaling law states that the model size & tokens should scale linearly (*1:1*), if not it will be to expensive

However it is shown & proven that performance can be improved with a significantly more tokens per parameter.

>[!info] With a larger model size the more VRAM is required during test-time

>[!note] There are improvement to models using algorithmic advances through ensemble learning techniques
>
>It is not always scaling.

Instead of scaling the model, we can **scale the test-time compute**, we can do this through:
- Sampling multiple responses
- Tree search
- Chain-of-though with verification
- External tools

However this will still require <b><span style='color:var(--mk-color-red)'>more computing power</span></b> (*More FLOPs*).

>[!info] FLOPs
>
> It stands for <b><span style='color:var(--mk-color-turquoise)'>floating point operations per second</span></b>.
> 
> It <b><span style='color:var(--mk-color-yellow)'>measures the raw computational speed</span></b> of a computer (*number of math operations which can be done in 1 second*).
> 
> This is relevant for LLMs since they **rely heavily on matrix multiplications** to predict the next word.

