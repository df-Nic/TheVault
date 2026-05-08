---
title: LLM Prompting
Date Created: 2025-09-02
Last Updated: 2025-09-28
tags:
  - CS6101
  - AI/ML/NN/LLM
---
# Basics of Prompting
---
There are some ways to work with LLMs to **get the desired output**:
1) Fine tuning (*Change in parameters*)
2) Prompting (*No change in parameters*)

>[!info] Prompting
>
>In terms of LLMs, **prompting** is the process of <b><span style='color:var(--mk-color-yellow)'>guiding the LLM</span></b> to the desired output through a series of prompts.

You can let the LLM roleplay as a persona, give examples or re-prompting.

Prompting can be **done in several stages**:
![[Stages to do Prompting in LLMs.png|center]]

Lets cover some in detail:
- **Instruction tuning**
	It is essentially **training** models with <b><span style='color:var(--mk-color-yellow)'>predefined instructions & responses</span></b>.
- **Zero-shot learning**
	It is the process of answering tasks <b><span style='color:var(--mk-color-yellow)'>without seeing any examples</span></b> beforehand
- **In-context learning** (*ICL*)
	The model will learn and adapt based on <b><span style='color:var(--mk-color-yellow)'>examples provided</span></b> from the prompt
- **RAG**
	Model retrieves external knowledge for better accuracy & grounding
- **Chain of thought**
	Or multiple chain of thought is just the steps the LLM took to reach the conclusion. There is also **tree** and **graph** which is basically instead of 1 roadmap it uses structures like trees & graphs to <b><span style='color:var(--mk-color-yellow)'>reason about its thought process</span></b>.

>[!abstract] Zero-shot
>
>Actually there is also 1 shot and few shot.
>
>**1 shot** will just mean that only 1 example is given & **few shots** means that some number of examples are given

>[!question] Why training the "thinking" portion of LLM's beneficial?
>
>By developing its chain of thought an LLM can have:
>- Better reasoning
>- Transparency (*Where the information is coming from*)
>- Better in handling complex tasks
>- Explore alternative
>- Self-correction
# Prompt Sensitivity
---
As we know LLMs are trained on a pre-defined set of data, and thus are <b><span style='color:var(--mk-color-red)'>sensitive to the subtle changes in prompts</span></b>. Thus factual information should not come from probabilities (*LLMs basically guesses the next word*).

Even by increasing few-shot examples, model size & instruction tuning does not eliminate the problem.

>[!note] Sensitivity of a model exhibits a strong negative correlation with accuracy
>
>The <b><span style='color:var(--mk-color-red)'>higher the sensitivity, the lower the accuracy</span></b>.
>
>So instead of checking for accuracy (*might not know if it is correct*) can we **just check for sensitivity**?
## Metrics

1) **POSIX** (*Prompt Sensitivity Index*)
It measures sensitivity by <b><span style='color:var(--mk-color-yellow)'>comparing log-likelihood changes across prompt variants</span></b>.

>[!success] Few-shot helps reduce sensitivity
>
>Since it is giving contextual information along with the prompt, thus variations might not affect as much, since the context is given through the few shot.

>[!failure] Having bigger model or instruction tuning might not always decrease sensitivity

2) **ProSA** (*Prompt Sensitivity Assessment*)
Instead of log-likelihood, it imposes a <b><span style='color:var(--mk-color-yellow)'>prompt sensitivity score</span></b> to measure stability under prompt variations.

>[!success] Few-shot helps reduce sensitivity

<b><span style='color:var(--mk-color-yellow)'>Model confidence is also a sign of stability</span></b>, with a higher confidence the response will be more consistent meaning more stable..
## Prompt Optimisation

One method proposed was, <b><span style='color:var(--mk-color-turquoise)'>combinatorial optimisation framework for prompt lexical enhancement</span></b> (*COPLE*).

>[!info] COPLE
>It identifies **words** in the prompt has the **greatest impact** on the model performance, and <b><span style='color:var(--mk-color-yellow)'>change it with other replacement words</span></b>.

We will repeat COPLE until no gains is observed.

The other method is <b><span style='color:var(--mk-color-turquoise)'>prompt optimisation with 2 gradients</span></b> or PO2G.

>[!important] This is mainly used for classification tasks

It uses **2 gradients** to guide the prompt refinement making <b><span style='color:var(--mk-color-green)'>optimisation stable</span></b>.

>[!success] It uses few iterations to reduce prompt sensitivity & making the prompt more reliable
# Hallucinations & Factual Errors
---
## Hallucinations

In general **hallucinations** are essentially an LLM giving the <b><span style='color:var(--mk-color-red)'>wrong answer which they think is correct</span></b>.

There are a few **types** of hallucinations:
1) **Intrinsic** - The output has direct <b><span style='color:var(--mk-color-yellow)'>contradiction</span></b> with the source material
2) **Extrinsic** - The output is based on <b><span style='color:var(--mk-color-yellow)'>speculation</span></b> which the model came up with
3) **Factuality** - Similar to intrinsic where it <b><span style='color:var(--mk-color-yellow)'>contradicts</span></b> real world facts
4) **Faithfulness** - Inconsistencies with the response, possibly <b><span style='color:var(--mk-color-yellow)'>diverting from the input/instruction</span></b>
## Mitigation by Prompting

We can do prompting to help reduce hallucinations:
- Self-consistency - Run multiple times and get a majority vote
- Tree of thought
- Chain of through
- Chat protect - Drops contradicting answers
- Reflection - An additional LLM which offers criticism
## Mitigation by RAG

RAG can mitigate hallucinations through the <b><span style='color:var(--mk-color-yellow)'>retrieval of information about the query</span></b>.

For instance in a **self-rag**:
- It will retrieve when needed
- Generate multiple candidate answers
- Critique & select the best answers using reflection tokens

>[!info] Reflection tokens
> They are like points for retrieval, relevancy of the retrieval, supported by facts & usefulness

With **multi-RAG**, we need to handle some possible <b><span style='color:var(--mk-color-red)'>issues</span></b> like:
1) Inter-source inconsistency
2) Redundancy
3) Incomplete inference paths

# LLM Jailbreaking
---
>[!summary] Jailbreaking is making LLM do things that they are not allowed to
>It can be things are unethical, harmful to other or to yourself or to get restricted client.
>
>This is usually done <b><span style='color:var(--mk-color-red)'>through prompt injection </span></b> which aims to insert malicious instructions & override the system prompt.

There are 2 main ways of carrying out prompt injection:
1) **Direct** - Malicious prompt is in the <b><span style='color:var(--mk-color-yellow)'>original query</span></b>, often used <b><span style='color:var(--mk-color-red)'>for social engineering or persona-based attacks</span></b>
2) **Indirect** - Malicious prompt is <b><span style='color:var(--mk-color-yellow)'>hidden within third-party documents</span></b> for the LLM to process

Some of the potentially bad things which can happen through jailbreaking are:
- **Personal identification information** & **training data exposure** (*Primate data used for training will be leaked*)
- **System prompt leakage** (*Knowing the system prompt makes LLM jailbreaking easier*)
- **Unintended behaviour**
## Jailbreaking Mitigation

1) **RAG**
It <b><span style='color:var(--mk-color-yellow)'>removes sensitive data</span></b> from the LLM **training** entirely.

2) **Red Teaming**
<b><span style='color:var(--mk-color-yellow)'>Thoroughly testing</span></b> the models, physically or automatically before release or deployment.

3) **Human-in-the-loop**
This is more more sensitive cases, but essentially <b><span style='color:var(--mk-color-yellow)'>human reviews flagged content</span></b>.

4) **Prompt-based approaches**
The <b><span style='color:var(--mk-color-yellow)'>LLM has a known jailbreaking prompt dataset</span></b> which will do a semantic check before replying.

![[LLM Jailbreaking Prompt-Based Approach Example.png|center|500]]


5) **Adversarial training**
Here we want to <b><span style='color:var(--mk-color-yellow)'>minimise the users ability</span></b> to force harmful generations.

There are a few ways of **doing AT**:
1) **Discrete AT**
During training, the model will be <b><span style='color:var(--mk-color-yellow)'>given a set of prompts and will try and react differently</span></b> when encountering these prompts.

>[!fail] It is expensive to do

2) **Continuous AT**
It takes a prompt and embed it, afterward it will <b><span style='color:var(--mk-color-yellow)'>augment the prompt maximising loss</span></b>. Then the model will be trained on these "worst case" scenarios <b><span style='color:var(--mk-color-green)'>making them more robust & generalisable</span></b>.

>[!fail] Does not correspond to real input tokens, making the LLM vulnerable

3) **Mix AT**
It is the <b><span style='color:var(--mk-color-yellow)'>mix of both</span></b> for the best results.
# LLM Blender
---
Each LLM has its own strengths & weaknesses. So how about **using all of them and get the best result**?

That's what LLM blender does, we <b><span style='color:var(--mk-color-yellow)'>take an ensemble</span></b> of open source LLMs then <b><span style='color:var(--mk-color-yellow)'>rank its outputs and fuse the top ones</span></b>.

>[!success] Leverage the different strengths from different models, reducing single-model quirks/biases

>[!success] Don't need to retrain base models as we only operate on their outputs
## How does it Work?

First we will for all pairs, compare 2 output candidates from 2 models using the `PAIRRANKER(rank)` which **uses a cross attention-encoder**.

Afterwards we will use `GENFUSER(fuse)` and feed the top-K ranked answers into a `seq2swq` model and generate one <b><span style='color:var(--mk-color-yellow)'>refine answer that keeps its strengths & weaknesses</span></b>.


