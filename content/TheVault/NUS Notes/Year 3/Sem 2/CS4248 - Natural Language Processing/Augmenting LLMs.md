---
Title: Augmenting LLMs
Date Created: 04-May-2026 00:00:00
Last Modified: 08-May-2026 12:32:50
Tags:
  - CS4248
  - AI/ML/NN/LLM/FineTuning
  - AI/ML/NN/LLM/Augmentation
---
# Fine-Tuning
---
## Motivation Of Fine-Tuning

### Task & Domain Adaptation

Often or not an <b><span style='color: #FFD700'>LLM is trained on no particular domain</span></b> (*trained on public general purpose data*). And it is just trained on text continuation.

LLMs might <b><span style='color: var(--mk-color-red)'>struggle with domain specific tasks</span></b> (*misaligned with what the user wants*) which requires a specialized vocabulary, reasoning or <b><span style='color: var(--mk-color-red)'>knowledge not represented in the pretraining data</span></b>.

>[!goal] We want to improve the LLM but on some specific task which we want it to do

A **common fine-tuning setup** is known as <b><span style='color: #87CEEB'>instruction-fine-tuning</span></b>.

>[!tldr] Instruction-fine-tuning
>Our training dataset includes **3 parts**:
>1) **Instruction**, this is more of <b><span style='color: #FFD700'>what the user wants</span></b>
>2) **Input** (*optional*), this is more of the <b><span style='color: #FFD700'>additional information from the user to do the task</span></b>
>3) **Response**
### Continual Learning Or Updating Knowledge

LLMs have a <b><span style='color: var(--mk-color-red)'>static knowledge cutoff</span></b> as it only <b><span style='color: #FFD700'>knows on things it was trained on</span></b>.

>[!failure] More hallucinations for tasks which requires up-to-date information

There are typically **3 main approaches**:
1) Periodic pretraining (*take your original model & continue training, resource-intensive*)
2) Fine-tuning (*targeted to a specific task, domain or style & often on a much smaller dataset*)
3) Retrieval-augmented generation (*RAG*)
### Style Or Tone Adaptation

Here instead of dealing with tasks we deal with <b><span style='color: #FFD700'>making the output more appealing</span></b>. We also want this style or tone to <b><span style='color: #FFD700'>adapt to the user</span></b>.

But typically LLMs are <b><span style='color: var(--mk-color-red)'>trained over factual, neutral sounding data</span></b> so the LLM's responses are typically neutral.

>[!example] Instruction fine-tuning for kid-friendly chatbot
### Bias Reduction Or Custom Alignment

Typically training data written by biased humans, meaning <b><span style='color: var(--mk-color-red)'>biased data which leads to a biased model</span></b> & biased responses.

Essentially we <b><span style='color: #FFD700'>do not want these stereotypes in our responses</span></b>.

>[!important] But we do not want to un-bias everything
>For example sister is for females only and that should be kept.

>[!example] Fine-turning dataset to prioritize genderneutral language 
## Challenges In Fine Tuning

### Data-Related Challenges

So now we <b><span style='color: var(--mk-color-red)'>no longer can do unsupervised training with unlabeled text</span></b>. We now need some sort of **labeled data** which tells us <b><span style='color: #FFD700'>given this task what is the output</span></b>.

This comes with a lot of non-trivial tasks to do:
- Data collection
- Data annotation
- Ensuing data quality (*cleaning, diverse, unbiased*)

>[!fail] Sometimes we might not even have access to the data which we need
>This makes data curation very long.
### Computational Challenges

Comparing periodic training & fine-tuning, <b><span style='color: #FFD700'>fine-tuning is not as resource intensive</span></b> than parodic pretraining. But there are <b><span style='color: #FFD700'>definitely hardware costs</span></b> (*GPUs/TPUs, memory*) and <b><span style='color: #FFD700'>training costs</span></b> (*time, energy*).

>[!important] All these computational challenges boils down to just data
>We need some way to <b><span style='color: #FFD700'>get the data</span></b> (*scrape*), then <b><span style='color: #FFD700'>filter</span></b> what data you need and also <b><span style='color: #FFD700'>check the quality of data</span></b>.
### Ethical & Safety

When fine-tuning we <b><span style='color: #FFD700'>sometimes lose general competency of the model</span></b>. This can also mean that we are <b><span style='color: var(--mk-color-red)'>weakening existing guardrails</span></b>.

Also it has a <b><span style='color: #FFD700'>low-entry barrier</span></b>, where people can <b><span style='color: var(--mk-color-red)'>fine-tune for misuse or malicious applications</span></b>.
### Other Difficulties In Fine-Training

Fine-tuning is **not a simple task**, we need to **handle optimisation challenges**  like:
- Catastrophic forgetting (*losing things the model learnt*) + overfitting & underfitting
- Task misalignment & conflicting objectives (*ensuring the model doesn't lie to do the task*)
- Hyperparameter sensitivity

And is not just during pre-training but **evaluating** the model as well:
- How can we check if fine-tuning is successful
- For custom tasks we require some custom benchmark dataset & evaluation metrics
## Parameter-Efficient Fine-Tuning

![[PEFT Methods.png|center|350]]

Also known as <b><span style='color: #87CEEB'>PEFT</span></b>. When we fine-tune we might have **very little data & a large parameter model**. So the tasks to fine-tune is <b><span style='color: var(--mk-color-red)'>resource intensive</span></b> (*due to the large parameters*) & we have a <b><span style='color: var(--mk-color-red)'>high risk of catastrophic forgetting or not generalising well with the new task</span></b>.

So the image above shows multiple methods to do PEFT but it all boils down to 2 basic ideas:
- Train/tune <b><span style='color: #FFD700'>only a subset of parameters</span></b>
- Use a <b><span style='color: #FFD700'>wide range of techniques proposed</span></b>
### Prompt Tuning

This fine-tuning method involves just <b><span style='color: #FFD700'>changing how we prompt the model</span></b>.

>[!idea] Optimise the prompt through different words or phrases to get the best response
>But this is <b><span style='color: var(--mk-color-red)'>impractical at scale</span></b>. But this is a high level overview of what we are doing.

So what we do is we <b><span style='color: #FFD700'>add an additional trainable context embedding</span></b> or <b><span style='color: #87CEEB'>soft prompts</span></b> (*seperate from the model during pre-training*).

![[Prompt Tuning Example.excalidraw.png|center|400]]

Then with this we can do supervised fine-tuning through gradient descent to tune the soft prompt parameters.

>[!important] The size of 1 token for the soft prompt must be the same as the hard prompt or else they cannot concatenate

>[!note] You can also tune both the LLM & the soft prompt embeddings

>[!question] Why not just add hard prompts?
>Using **hard prompts** we are <b><span style='color: var(--mk-color-red)'>restricted or limited</span></b>. So with **soft prompts** we are <b><span style='color: #98FB98'>unbounded in terms of expressiveness</span></b> as these are tunable.
>
>And even though soft prompts do not correspond to real words they <b><span style='color: #FFD700'>can still hold some information</span></b>.

>[!success] Number of trainable parameters is negligible compared to the main LLM
>This is because we only update the additional context embedding.

>[!success] Easy to train different soft prompt for different tasks
>And it is very <b><span style='color: #98FB98'>quick and easy to swap</span></b> during inference time.
#### Prefix Tuning

So instead of putting the context embedding during the prompting stage. We <b><span style='color: #FFD700'>put it inside the transformer of the model</span></b> known as a <b><span style='color: #87CEEB'>prefix</span></b>. So when we do <b><span style='color: #FFD700'>fine-tuning we only focus on this prefix block</span></b> (*the other parameters are frozen*).

And similar to **[[Year 3/Sem 2/CS4248 - Natural Language Processing/Augmenting LLMs.md#Prompt Tuning|prompt tuning]]** is very <b><span style='color: #98FB98'>quick and easy to swap</span></b> it out.

>[!important] The main difference is that this prefix block is added to every transformer block
>Typically this is done on the Keys and Values in all your encoders & decoders, where we just pre-append this tunable context embeddings.

>[!info] We can do prefix tuning along side prompt tuning
### LoRA

The problem with **prompt & prefix tuning is that we do not modify any of the model's weights**.

>[!fail] So if we were to use these methods but we need to tune the model's parameters for our tasks then we hit a deadend

So we have LoRA which is <b><span style='color: #87CEEB'>low rank adaptation</span></b>. It is low rank because we are <b><span style='color: #FFD700'>trying to approximate the entire network in some smaller resolution</span></b>.

![[LoRA.png|center|200]]

LoRA introduces something called a <b><span style='color: #87CEEB'>adapter</span></b>, which is a <b><span style='color: #FFD700'>small, trainable module added</span></b> to a pretrained network model. And it is <b><span style='color: #98FB98'>plug and play</span></b> since we can just swap out the adaptor for the task we are doing.

However, LoRA what it actually does it just **gives you a trainable vector of the same size as the original model**.  So how does it become low rank? The trick here is to <b><span style='color: #FFD700'>use 2 smaller matrices & do a matrix multiplication</span></b> to get an approximation of the original one.

>[!success] Flexibility to apply to all or some of the weight matrices
>As some weights might be redundant to tune as it is not important.

>[!success] Less trainable weights, meaning lower memory requirements & faster training

>[!success] Pretrained weights remain unchanged
>If anything is wrong with the adaptor the original model is the same.

>[!success] Merge LoRA weights with the pre-trained weights for zero inference latency

>[!fail] Increase complexity

>[!fail] LoRA might not perform as well as fine-tuning
>If the domain requires a whole update of the weights.
#### LoRA Under The Hood

![[LoRA In Depth.png|center|300]]

We have 2 matrices $A$ & $B$:
- $A$ is known as a <b><span style='color: #87CEEB'>downward projection</span></b>, <b><span style='color: #FFD700'>initialised to be some random number</span></b> (*or noise*)
- $B$ is known as a <b><span style='color: #87CEEB'>upward projection</span></b>, <b><span style='color: #FFD700'>initialised to be all 0</span></b>

>[!important] We can swap the 2 around but we can never let both start at 0 if not then the gradient will always be 0 & the parameters will never update

So now our **output** is:
$$
\text{Output} = xW + x\Delta W = xW + x(\frac{\alpha}{r}AB)
$$
Where:
- $\alpha$ is some scaling factor
- $r$ is called a rank where $r \ll min(d, k)$

>[!question] Why does this work
>Typically in large models <b><span style='color: #FFD700'>most of the weights are close to 0</span></b>. So we can do this compression through this low rank adaptation (*throw away the 0s*).
>
>And we know that with **[[Year 3/Sem 2/DSA3362 - Predictive Data Analytics/Principle Component Analysis.md|PCA]]** we can <b><span style='color: #98FB98'>significantly reduce the number of dimensions but preserve a lot of the variance</span></b> that the model originally has.

>[!warning] Setting the rank too low though we reduce the training parameters but the model's performance might not be good after tuning
### Adapters

![[Adaptor Architecture.png|center|150]]

They are different from the ones in LoRA as here we are <b><span style='color: #FFD700'>adding a small network module</span></b> (*LoRA there is no activation function*).

So during <b><span style='color: #FFD700'>fine-tuning only the modules are updated</span></b> the rest are frozen.

>[!success] More flexible than LoRA's adaptors

>[!fail] We cannot merge the weights with the models weights

Ways to **add adaptors**:
![[Different Ways To Add Adaptors.png|center|400]]

Note that **[[Year 3/Sem 2/CS4248 - Natural Language Processing/Augmenting LLMs.md#LoRA|LoRA]]** follows the parallel adaptor style (*and it cannot be anything else*).

>[!note] These adaptors are typically placed around the feed forward layer

These adaptors <b><span style='color: #FFD700'>can be task or domain adaptors</span></b> and we can also use both of them together.
# LLM Augmentation
---
## Reasoning LLMs

>[!question] What is reasoning?
> It is the <b><span style='color: #FFD700'>process of reaching to the final answer</span></b> (*the intermediate steps*).

To train a reasoning LLM we need to <b><span style='color: #FFD700'>change the training & compute allocation</span></b>.

>[!important] The architecture stays the same as a normal LLM

So instead of question & the direct answer we will now <b><span style='color: #FFD700'>give our query and then some number of intermediate steps and then the final answer</span></b> (*learn to reason*) during **training** (*SFT*). And doing **inference** (*ICL*) we can <b><span style='color: #FFD700'>ask for the intermediate steps since the history will be within the context</span></b>.

As for compute we will <b><span style='color: #FFD700'>need to increase the max token allocation</span></b> (*compute allocation*) because these intermediate steps does take up tokens.

>[!important] But remember to enforce some limit or else the model might just go on and on without giving a final answer
### Chain-Of-Thought Prompting

This is more on the **inference** side where we give it a prompt & then also <b><span style='color: #FFD700'>say how should you derive the answer or give some intermediate examples to similar questions</span></b> (*multi-shot prompting but with reasoning steps*).

And this <b><span style='color: #98FB98'>works very effectively</span></b> even with arithmetic, common sense or symbolic tasks.

>[!question] So why does it work?
>So in a high level sense we are essentially making the model <b><span style='color: #FFD700'>link up with all the relevant information is used in training</span></b> to get the final answer
### Tree Of Thought & Preference Learning

From chain-of-thought the reasoning is linear, basically a step by step approach but what if we want to **consider other alternatives**?

This is where <b><span style='color: #87CEEB'>Tree of Thought comes</span></b> in our **training** data we are given a prompt at <b><span style='color: #FFD700'>each iteration we will give multiple alternatives</span></b> & compute the loss based on the correct one.

So now the model knows to generate alternatives but now how does it **pick the correct one**? So here is where **[[Year 3/Sem 1/CS3263 - Foundations of Artificial Intelligence/Reinforcement Learning.md|reinforcement learning]]** comes in in order to do <b><span style='color: #87CEEB'>preference learning</span></b>, we can just <b><span style='color: #FFD700'>assign a reward for the good alternatives</span></b> (*& also a cost for the bad ones*).

>[!success] We can even go further by picking alternatives that the user wants
## Retrieval Augmented Generation (RAG)

![[RAG Overview.png|center|450]]

>[!question] Why RAG?
> We learn that why we do fine-tuning is because of **[[Year 3/Sem 2/CS4248 - Natural Language Processing/Augmenting LLMs.md#Continual Learning Or Updating Knowledge|knowledge cutoff]]**. But <b><span style='color: var(--mk-color-red)'>fine-tuning can be slow</span></b> if we have <b><span style='color: #FFD700'>time-dependent questions</span></b> (*financial data, or non static data*).

So RAG is a <b><span style='color: #FFD700'>knowledge based prompt engineering</span></b>. where we can **insert new context** information to the prompt <b><span style='color: #FFD700'>through retrieval from an external knowledge base</span></b>.

>[!success] We add grounding to the LLM's response based on providing factual data
>So it all depends on the data you provide, how clean is it.
>
>But can go beyond facts to have <b><span style='color: #FFD700'>rationales</span></b> (*reasoning behind the facts*).

>[!success] Simple integration for recent or domain specific data

>[!success] Improved transparency
>Because we know what information it is using

>[!success] High customisation & personalisation
### Knowledge Repository Creation

Now this is the **main & core part of RAG** which is <b><span style='color: #FFD700'>where does all the information come from</span></b>, this can be:
- Readily available data (*company internal documents*)
- Explicit data collection (*APIs or web scraping*)

The data can be in <b><span style='color: #FFD700'>many formats like text or those with markup</span></b> (*HTML, PDF, DOCX, Markdown*).

>[!important] Even with all the data we need to ensure data quality
>This is still the most important step as <b><span style='color: var(--mk-color-red)'>data on the web has a lot of noise</span></b> (*even internal documents sometimes*).
>
>So we need to do **data cleaning, conversion & deduplication** & we also have to consider the **bias** or the **ethical** aspects of the data
### Chunking

When we retrieved the information we **cannot just throw everything** to the LLM. <b><span style='color: #FFD700'>Not everything is important to our query & we also have to consider the token limit</span></b> (*more tokens more things to load into the LLM*).

So we need to find ways to **summarise information** & we can simply do this by <b><span style='color: #FFD700'>splitting it up</span></b> into parts called <b><span style='color: #87CEEB'>chunks</span></b> and there are many **strategies**:
- Fixed sized chunking (*naive splitting based on a specific length with or without overlap*)
- Recursive chunking (*top-down approach to keep paragraphs & sentences intact*)
- Document based chunking (*utilize document structure*)
- Semantic chunking (*based on sentences & their embedding similarities*)
- Agentic chunking (*let the LLM split*)
### Storing

So after retrieval and chunking we need to store the information somewhere. There are a **few ways of storing**, but ultimately we store things & there is a fast way to get what we want :
1)  <b><span style='color: #FFD700'>Traditional information retrieval</span></b>

Here we just store chunks as text documents & we <b><span style='color: #FFD700'>index them using the inverted word index</span></b> (*think of this as where the words are in the book*), this is to <b><span style='color: #98FB98'>speed up retrieval</span></b>.

Then we use a <b><span style='color: #FFD700'>prompt as text to query</span></b> the knowledge base & <b><span style='color: #FFD700'>return chunks that are similarity</span></b>.

2) <b><span style='color: #FFD700'>Vector database</span></b>

Here we <b><span style='color: #FFD700'>encode chunks as embeddings</span></b>, then store it as a vector. Then we can also <b><span style='color: #FFD700'>index the embeddings</span></b> to <b><span style='color: #98FB98'>speed up retrieval</span></b>.

Then we can **search for the nearest chunks based on the prompt** using <b><span style='color: #FFD700'>distances</span></b> like cosine similarity.
### Retrieval

As for **retrieval** we can categorises into **2 types**:
1) <b><span style='color: #FFD700'>Sparse retrieval</span></b>

**Query & documents** are converted to <b><span style='color: #FFD700'>V-dimensional sparse vectors</span></b> (*V is our vocabulary size*) with many 0 elements.

There are **2 main strategies**:
- Term matching sparse retrieval
- Neural based sparse retrieval

>[!example] Some examples of term matching sparse retrieval
>[[Year 3/Sem 2/CS4248 - Natural Language Processing/Text Classification.md#Term Frequency - Inverse Document Frequency|TF-IDF]], BM25

>[!success] Efficient retrieval with the use of an inverted index
>Approximately `O(1)` in terms of efficiency & it is <b><span style='color: #98FB98'>easily parallelised</span></b>.

>[!success] Strong term filtering ability
> We can filter by words, and their positioning since each dimension represents 1 word.

2) <b><span style='color: #FFD700'>Dense retrieval</span></b>

**Query & documents** are converted to <b><span style='color: #FFD700'>some dense representation</span></b> (*so we use a smaller vector space*).

There are **2 main strategies**:
- <b><span style='color: #FFD700'>Single vector</span></b> retrieval where passages are represented by a single embedding, via BERT’s `CLS` token)

So here all the <b><span style='color: #FFD700'>chunks in the document are averaged</span></b> out before we compute the similarity.

- <b><span style='color: #FFD700'>Multi-vector</span></b> retrieval (*watch token in a passage is represented by its own embedding*)

Here <b><span style='color: #FFD700'>each chunk is treated individually</span></b> when computing the similarity which we <b><span style='color: #98FB98'>can then take the relevant parts</span></b>. 

**Examples** of dense retrieval:
![[Examples of Dense Retrieval.png|center]]

>[!success] You use less space for your storage systems

>[!failure] Loses the filtering capabilities because now the dimensions does not represent a word
>But is alright because <b><span style='color: #98FB98'>typically humans do not want a exact match we just want something similar</span></b>.

But there are **many ways to do retrieval between these 2 types** & you can even use a transformer to do the retrieval if it can remember all the documents.
## Tool Use

We code all these functions to solve tasks that we do on a daily basis, so can we also <b><span style='color: #FFD700'>provide LLMs tools to solve certain problems</span></b>.

>[!goal] Typically tools are used to solve deterministic problems so by allowing LLMs to have tools we can sort of make it more deterministic.

So **typical tools are**:
- Search engines
- Custom tools through custom code

But know we need to know how can we encode tools into the LLM & also discover and create more tools.
### Training To Encode Tools

The most simplest way encode tools into the LLM is by <b><span style='color: #FFD700'>training it to annotate text with potential API calls</span></b>. So we will have a list of API calls (*tools*) & we will ask the model to <b><span style='color: #FFD700'>replace parts of the text with API calls and the arguments to pass into it</span></b>.

>[!important] Here the LLM does not execute any API call

>[!question] With training how do we compute the loss?
>In a sentence sample a position $i$ with an API call & their candidates then we will <b><span style='color: #FFD700'>execute the API call and then use the result to generate the rest of the text</span></b>. 
>
>From there we can compare the loss to the original text.
### Program Aided LMs (PAL)

>[!idea] Have the LLM generate code in any programming language to execute

So during reasoning the model will <b><span style='color: #FFD700'>output interleaved natural language and programming language</span></b>.

We then take the code it generated and use the corresponding <b><span style='color: #FFD700'>compiler to execute the code & use its response in its output</span></b>.

>[!note] LLMs (e.g., Codex) trained on large public codebase (*GitHub*) heavily use comments (*docstring*) and transparent variable names to ground what they refer to
### Tool-Augmented Reasoning framework for Tables (TART)

Here are are more <b><span style='color: #FFD700'>focused on structured data</span></b> (*tables*). And we want to <b><span style='color: #FFD700'>manipulate the data</span></b> to get the answer to our query.

>[!idea] To let the LLM decide on which tools are needed for the query
>These tools are functions to manipulate & query the tables.

>[!warning] Encode the specifics of the problem context & input data

>[!warning] Must deduplicate & generalize the toolset
>So there is this <b><span style='color: #87CEEB'>tool maker</span></b> which the <b><span style='color: #FFD700'>LLM can use to make its own tools</span></b>.
### Practical Function Calling

Here it is very simple, the <b><span style='color: #FFD700'>LLM will have a list of tools & their descriptions & parameters</span></b> & at any point requires to use these tools it will <b><span style='color: #FFD700'>call the developers system which will execute the tool</span></b> with the inputs as requested by the LLM (*typically through some sort of wrapper using a JSON output*).

>[!note] That the LLM will be under the assumption that the prompt contains all the sufficient information to identify all required arguments of the tools

The <b><span style='color: #FFD700'>output will then be fed back to the LLM</span></b> (*combine the initial prompt with the output*) which can call more tools or it will use it as the final output.

>[!question] So where does these functions run?
>Typically they can be on the <b><span style='color: #FFD700'>cloud</span></b> or sometimes <b><span style='color: #FFD700'>locally for some custom functions</span></b>.
## Routing

![[Query Router Example.png|center]]

<b><span style='color: #FFD700'>Not all queries require the same treatment</span></b>. Some requires tool calling, some requires just chain of thought. So this is what a **query router is used for** (*some LLM*), it <b><span style='color: #FFD700'>augments the query based on what it requires</span></b>.

>[!example] For a simple query we do not need to even use a tool or do any retrieval as doing so will just be overhead computation

And it is not just the augmentation , it <b><span style='color: #FFD700'>can also decide what LLM model to use</span></b>.

>[!example] Maybe for financial queries use this model & for simple queries use this smaller model or we can even use multiple models & combine their responses

# Data Augmentation
---
## Teacher-Generated Data

**Foundational LLMs** very <b><span style='color: #98FB98'>capable</span></b> but also <b><span style='color: var(--mk-color-red)'>very costly to run and slow</span></b>. Typically for <b><span style='color: #FFD700'>specialised tasks a smaller model is good enough</span></b>.

So this is where **[[Year 3/Sem 2/CS4248 - Natural Language Processing/Improving LLMs Efficiency.md#Distillation|distillation]]** comes in. The idea is to <b><span style='color: #FFD700'>transfer knowledge from the larger model to the smaller model</span></b> (*so teacher to student*).

>[!success] The smaller model will have the same capabilities but is now faster & cheaper

There are a wide range of strategies & one of them is called **response distillation**.
### Response Distillation

![[Response Distillation Overview.png|300]]

It is a very simple approach, have a unlabeled training data & then ask a more <b><span style='color: #FFD700'>powerful model to label the dataset</span></b>. Then we <b><span style='color: #FFD700'>use this question answer data set to train a smaller model</span></b>.

>[!info] These AI generated data is known as "silver" data
>**"Gold"** standard data is one that is <b><span style='color: #FFD700'>verified by a human</span></b>.
>
>**"Bronze"** is data which are not verified but it has some noise.

>[!success] Easy to implement

>[!success] Generally high-quality responses
>As long as the teacher is good & the data which it was trained on.

>[!fail] Labelling a large dataset is expensive

>[!fail] Final outputs do not capture more nuanced knowledge
>It <b><span style='color: var(--mk-color-red)'>does not show how confident the larger model</span></b> is as compared to using logits & probabilities.

>[!fail] Student tends to be less creative
>This is known as <b><span style='color: #87CEEB'>AI inbreeding</span></b> where we use <b><span style='color: #FFD700'>AI to generate data to train a model</span></b> resulting in less variability.
## Self-Instruction

Here is the general workflow:
1. <b><span style='color: #FFD700'>Seed tasks</span></b>: start with a small set of human-written instructions
2. <b><span style='color: #FFD700'>Generate new instructions</span></b>: prompt an LLM to propose new tasks/instructions (*often by varying domains and formats*)
3. <b><span style='color: #FFD700'>Generate responses</span></b>: for each instruction, have the LLM produce an answer (*sometimes multiple*)
4. <b><span style='color: #FFD700'>Filter / deduplicate</span></b>: remove low-quality, unsafe, trivial, or near-duplicates; optionally score with heuristics or another model. This <b><span style='color: #FFD700'>step is critical</span></b>.
5. <b><span style='color: #FFD700'>Fine-tune</span></b> (*SFT*): train on the synthetic instruction-response pairs
6. (*Optional*) <b><span style='color: #FFD700'>Iterate</span></b>: repeat generation → filtering → training

>[!idea] We are asking the same model to based on some task generate other tasks & the data to train itself again.

>[!important] If we do not filter and deduplicate properly we will be training out model with bad data
### Confidence Scores For Filtering & Deduplication

Now we want to **ask ourselves how confident the model is in the new data is just generated?**

There are **3 ways to look at this**:
1) <b><span style='color: #FFD700'>Natively</span></b>

Natively means looking <b><span style='color: #FFD700'>internally</span></b> in terms of the <b><span style='color: #FFD700'>logits</span></b> or the SoftMax probability. For a given output we can <b><span style='color: #FFD700'>average out the logits or take the minimum confidence token in the output</span></b>.

>[!info] A well-calibrated model will display logits reflect the proportion of answers it gives to be correct
>So if the model gives a confidence of 80% then out of 10 answers only 8 of them should be correct (*else the model is over or under confident*).
>

>[!success] The higher the average logits the more confident the model is

>[!fail] We need access to the models logits which might not always be the case

>[!question] Why does this work?
>If we look at the distribution if the model is unsure we will see a flat distribution where everything is the same.
>
>But if the model is **sure** we will <b><span style='color: #FFD700'>see a spike</span></b> in this distribution.

2) <b><span style='color: #FFD700'>Use a proxy</span></b>

Another term is <b><span style='color: #87CEEB'>self-consistency</span></b>, where we <b><span style='color: #FFD700'>ask the model the same question some number of times</span></b> & we see whether <b><span style='color: #FFD700'>majority of the responses agree</span></b> or not.

>[!success] The higher the fraction that agree the more confident the model is

We can also do a <b><span style='color: #87CEEB'>verifier-based confidence</span></b>, where we run some checks, tests or even ensuring grounding (*maybe through human proofs*) for more confidence.

3) <b><span style='color: #FFD700'>Prompt the LLM for a confidence score</span></b>

Here we just <b><span style='color: #FFD700'>prompt a LLM to give us a confidence score</span></b> between some range. It is the <b><span style='color: var(--mk-color-red)'>least reliable</span></b> (*we do not know how they get this number*) but the <b><span style='color: #98FB98'>easiest to obtain</span></b>.

>[!tldr] This brings about LLM as a judge (LLMaaJ)
>Here we let the LLM evaluate because <b><span style='color: var(--mk-color-red)'>human evaluation is timely & costly</span></b> (*& not suitable for simple metrics*). So we use LLMs to <b><span style='color: #98FB98'>make evaluation scalable & consistent</span></b>.
>We can use LLMaaJ if we have:
>- Clear rubric + examples
>- Controlled prompts
>- Multiple samples / majority vote
>- Calibration against human labels
>
>But some best practices are that we:
>- Use a strong reference model
>- Blind the judge to system details
>- Randomize order (*order influences the results*)
>- Add adversarial test sets (*add simple test sets to see if it knows what it is doing*)
>- Measure human agreement  (*use some humans to validate*)
> 
>>[!fail] Risk of model self-preference, susceptibility to prompt injection & wording
>
>>[!fail] Unsuitable for high stakes correctness  & strict factuality is needed

>[!tldr] Human in the loop
>The idea here is that we still use LLM as a judge. But when the **model is unsure** of its generated instructions then we will <b><span style='color: #FFD700'>let the human handle them</span></b> else we can let the LLM to judge.
#### Temperature Scaling

From the **confidence scores** we can tell if our **model is overconfident or underconfident**. And we can solve this using <b><span style='color: #87CEEB'>temperature scaling</span></b> which is <b><span style='color: #FFD700'>simply just scaling the logits</span></b>.

Recall our SoftMax function, we can **add scaling** as such:
$$
P = \frac{exp(x_{i} / t)}{\sum_{j} exp(x_{j} / t)}
$$
Where:
- $t$ is our temperature scaling

The original value of $t = 1$:
- If we have anything **below 1** it is called <b><span style='color: #87CEEB'>sharpening</span></b>, this makes the distribution more <b><span style='color: #FFD700'>sharp</span></b> (*for underconfident*)
- If we have anything **above 1** it is called <b><span style='color: #87CEEB'>smoothing</span></b>, this makes the distribution <b><span style='color: #FFD700'>flatter</span></b> (*for overconfident*)
## Safety

When we do data augmentation we need to <b><span style='color: #FFD700'>be careful that what we add is useful</span></b> (*it should enhance learning*).

>[!important] Augmentation should NOT compromise semantic integrity or introducing vulnerabilities

So we need to ensure that:
- Validate that synthetic data transformations preserve the original label semantics
- Synthetic data should not distort the core features required for accuracy

>[!danger] If we do not augment properly it can lead many issues
>- Semantic shift
>- Introduction of unwanted artifacts (*compounded errors*)
>- Degrade model performance (*model collapse*) on out-of-distribution data

>[!example] We know models prefer their own responses so if we use LLM as a judge to create mode data we are amplifying this preference

And it is **not just quality of the data** we are using but also:
- <b><span style='color: #FFD700'>Duplicates</span></b> or near duplicates (*ensure diversity, some human auditing*) if not it will <b><span style='color: var(--mk-color-red)'>lead to memorisation</span></b>
- Evaluation contamination where we <b><span style='color: #FFD700'>must separate training & test data</span></b> (*we do not know what the model is trained on so to be safe use other models*)
- <b><span style='color: #FFD700'>Personally Identifiable Information</span></b> (*remove them programmatically or manually or augment them*)


