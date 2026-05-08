---
title: RAG Introduction
Date Created: 2025-08-07
Last Updated: 2025-09-28
tags:
  - CS6101
  - RAG
---
# What is RAG?
---

>[!info] Retrieval Augmented Generation
>
> A LLM which <b><span style='color:var(--mk-color-yellow)'>retrieves additional information from a datastore</span></b> (*database, internet*) known as documents to generate an output.
> 
> ![[High Overview of a RAG Model|center|500]]

A LLM or a **language model**, is essentially given the words it has seen, what is the highest probability of the next word (*In a math sense $P(X_{n} \vert X_{1}, X_{2}, \dots, X_{n})$*), this is known as a <b><span style='color:var(--mk-color-yellow)'>autoregressive model</span></b>.

We can also refer to these retrieval based LMs as <b><span style='color:var(--mk-color-turquoise)'>semiparametric</span></b> or <b><span style='color:var(--mk-color-turquoise)'>non-parametric models</span></b>.

>[!tldr] Parametric & Non-parametric Models
>
> A **parametric** model solely <b><span style='color:var(--mk-color-yellow)'>relies on the parameters</span></b> it is built upon to make its decision.
> 
> A **non-parametric** model does not rely on the parameters but <b><span style='color:var(--mk-color-yellow)'>external sources</span></b> (*Datastore*).

LLMs are mainly built using transformers which are fully parametric. They are trained on predictions on next tokens. And this requires a large model and data size.

>[!note] Sparse & Dense Retrieval
>
> When talking about sparse or dense, it refers to **embeddings**.
> 
> A <b><span style='color:var(--mk-color-turquoise)'>sparse</span></b> embedding has a **high dimension** (*More numbers in the vector*). Thus embedding <b><span style='color:var(--mk-color-yellow)'>corresponds to 1 word or thing</span></b>.
> 
> A <b><span style='color:var(--mk-color-turquoise)'>dense</span></b> embedding has a **low dimension** mainly through compression (*[[Unsupervised Learning#Dimensionality Reduction|dimensionality reduction]]*). Thus an embedding can <b><span style='color:var(--mk-color-yellow)'>correspond to a group of similar things</span></b>.

>[!failure] Bottlenecks with LLMs
>
> The creation of retrieval LMs is to **resolve issues faced by traditional LMs**:
> - Cannot memorise all (long tail) knowledge in their parameters
> - Knowledge can be outdated and hard to update
> - Hard to interpret and verify
> - What if private information is being fed it will be leaked
> - Expensive, large and hard to train (*knowledge editing*) & run (*Some models can be compressed using <b><i>Quantization</i></b> which is the reduction of precision for less important weights*)

With the issues that LLMs faces **RAGs** solves this by **reinforcing its own response** (*Identify the sources for interpretability & control*) to <b><span style='color:var(--mk-color-green)'>remove hallucinations</span></b> (*Giving false information*).

It basically <b><span style='color:var(--mk-color-yellow)'>augments the input by giving it more context</span></b> which is done during run time (*inference time*).

And since RAG uses its own datastore, it can <b><span style='color:var(--mk-color-green)'>adapt to new distributions</span></b> (*New or updated information*).
# Retrieval Orchestration
---
In a RAG model, when a query ($q$) is being inputted, there will be a **retriever** which will fetch relevant information from an external datastore $D$.

It seems simple but we need to think about the few things.
- What to retrieve
- How to retrieve
- Presentation & Consumption (*Convert the retrieved information into the LMM*)
## When to Retrieve

To always retrieve data from the datastore can be costly, thus it is preferred to have an <b><span style='color:var(--mk-color-green)'>adaptive retrieval</span></b>.

>[!abstract] Adaptive retrieval
>
>The ideal scenario is that the LLM will only <b><span style='color:var(--mk-color-yellow)'>retrieve from the datastore when it needs to</span></b>.
>
>This should be done when understanding niche topics or things not in its training dataset.

We can do this in a number of ways:
- Classifier-based methods (*Classify if the query needs to be augmented or not*)
- Confidence-based methods (*Similar to point 1*)
- LLM-based methods (*The LLM will determine if retrieval is required or not*)

There are **4 criteria's** to determine retrieval:
1) **Intent-aware**: Whether the user desires retrieval / external information
2) **Knowledge-aware**: The question requires factual knowledge
3) **Time-sensitive-aware**: Question is time sensitive
4) **Self-aware**: Does the LLM has internal knowledge

>[!question] How to determine the criteria?
>
>People have developed a <b><span style='color:var(--mk-color-yellow)'>binary classifier</span></b> to determine this query requires what retrieval.
## Where to Retrieve

The retriever can **access a diverse pool of sources** (*text corpus, web, databases, etc*).

>[!failure] Challenges faced retrieval from multiple sources
> - Cross-source deduplication & conflict resolution (*Resolve conflicting & duplicated information*)
> - Source-selection accuracy (*Not all documents are relevant or reliable (Page rank)*)
> - Heterogeneous data integration (*Combining data of different formats and making sense of the data*)

>[!abstract] How does page ranking work
>
>It follows the perception of prestige, where "a page is important if other important pages link to it".
>
>Thus we can think of <b><span style='color:var(--mk-color-yellow)'>each hyperlink as 1 vote</span></b>, and if the vote <b><span style='color:var(--mk-color-yellow)'>comes from a prestigious website it weighs more</span></b>. 
## What to Retrieve

We know that what the models needs to retrieve is **based on the query given**.

We can do a <b><span style='color:var(--mk-color-yellow)'>query stratification</span></b> (*ranking query complexities*)
1) **Explicit facts** - Facts which are directly present in the given data
2) **Implicit facts** - Requires common sense reasoning or basic logical deductions
3) **Interpretable rationales** - Need to comprehend & apply domain-specific rationales
4) **Hidden rationales** - Rationales not explicitly documented and must be inferred from patterns & outcomes

We can <b><span style='color:var(--mk-color-yellow)'>augment the query</span></b> to make the retrieval <b><span style='color:var(--mk-color-green)'>more efficient</span></b> through the following methods:
- Compression (*Not everything in the query is useful*)
- Expansion (*Need to add more context to the query to yield desired results*)
- Conversion (*Is like expansion but reshaping the query into a new one based on its inherent structure*)
- Decomposition (*Break the query into smaller queries to allow adding chain of through*)

>[!note] Adaptive query reformulation
>
>To **determine the most appropriate** query augmentation a <b><span style='color:var(--mk-color-turquoise)'>query router</span></b> (*Some LLM*) is used.

If <b><span style='color:var(--mk-color-red)'>one augmentation is not enough</span></b>, it can be <b><span style='color:var(--mk-color-yellow)'>fed back to the query router</span></b> again to be reformatted.

We can also do <b><span style='color:var(--mk-color-turquoise)'>query routing</span></b>, which is <b><span style='color:var(--mk-color-yellow)'>finding the correct LLM which can satisfy the query</span></b> the best.
## How to Retrieve

Each document will have unique item ID. We then need to know which of these IDs are relevant to our query.

1) **Sparse Retrieval**
It is essentially <b><span style='color:var(--mk-color-yellow)'>information represented as a v-dimensional sparse vectors</span></b> containing a lot of non-zero elements.

>[!example] Examples of sparse retrieval
>
> Term matching sparse retrieval, neural-based sparse retrieval

>[!success] Efficient retrieval with inverted index
>
>An **inverted index** means, using <b><span style='color:var(--mk-color-yellow)'>words in a lookup table</span></b> and its associated documents.

>[!success] Strong term filtering ability
>
>Sparse retrieval is <b><span style='color:var(--mk-color-yellow)'>exact-match based</span></b>, thus documents containing the query will show up.

2) Dense Retrieval
Similar to sparse retrieval, however it <b><span style='color:var(--mk-color-yellow)'>focus on semantic embeddings</span></b> (*Similarity matching*).

There are 2 types of sense retrieval:
1) **Single vector retrieval**: Both the query and document(s) will be represented into a single embedding
2) **Multi-vector retrieval**: Each token will represented by its own embedding

>[!question] Single or Multi vector retrieval?
>
>Both have their own advantages and disadvantages.
>
>For single vector, it takes up <b><span style='color:var(--mk-color-green)'>less memory</span></b>, <b><span style='color:var(--mk-color-green)'>faster response time</span></b>, but <b><span style='color:var(--mk-color-red)'>less accurate</span></b>.
>
>For multi vector, it takes up <b><span style='color:var(--mk-color-red)'>more memory</span></b>, <b><span style='color:var(--mk-color-red)'>slower response time</span></b>, but <b><span style='color:var(--mk-color-green)'>more accurate</span></b>.

3) **Re-ranking**
Essentially the first round of retrieval uses a general ranking system, and thus we will need a strong re-evaluation to <b><span style='color:var(--mk-color-yellow)'>filter in relevant documents</span></b>.

**How it works**:
1) Use a simple retriever to retrieve documents (*Cheap & fast*)
2) Then we use a strong re-ranking model (*BERT*) or an LLM to re-rank all documents

>[!note] We need to strike a balance between efficiency & effectiveness

>[!failure] Performance degrades as size of initial retrieval grows

>[!abstract] How is retrieval evaluated
>
>There are many metrics, MAP, NDCG@10, MRR@10
>
>To elaborate on 1, MRR@10 means <b><span style='color:var(--mk-color-turquoise)'>mean reciprocal rank</span></b>. It observes the <b><span style='color:var(--mk-color-yellow)'>first 10 retrieved results and find the first relevant document</span></b>.
>
>It will take the reciprocal ($1/\text{rank}$) and average it out across all queries.
## Presentation & Consumption

>[!info] Presentation is how to prepare the retrieval results for consumption

>[!info] Consumption is the process of how the LMM incorporates retrieved information

>[!example] Examples of some tatics
>
>- Summarization: More Information w/ Less Tokens
>- Long Context Summarization
>- Long Context Reranking
>- Adaptive Context Length via Truncation
>- Compressed Representation

# Optimisation Techniques
---
In general when optimising we can either
- Modify the generator (*LLM*) only (*retriever is frozen*)
	- One paradigm is to encode the query + the document, then concatenate them together and pass it through the decode. A downfall is if there is **a lot of documents**, it will be <b><span style='color:var(--mk-color-red)'>large and inefficient</span></b>
	- We can also add noise (*Gumbel noise*) since generators are not discrete & continuous (*gradient descent*)
- Modify the retriever (*generator is frozen*)
- Or modify both

>[!info] We can also do reinforcement learning
>
>This is to let the model <b><span style='color:var(--mk-color-yellow)'>learn by itself</span></b>.
>
>We can model the different actions as states and if the model choose to answer, retrieve, what to search for, it will be rewarded accordingly.

