---
Title: Big Picture of NLP
Date Created: 18-January-2026 00:00:00
Last Modified: 08-May-2026 12:33:41
Tags:
  - CS4248
  - AI/NLP
---
# What is NLP?
---
In natural language processing we want <b><span style='color: #FFD700'>machines to understand how humans communicate</span></b> through the rules of natural language.

So we want the machine to have or learn some internal representation of language & the world.

NLP's can be used in:
- Chatbots
- Text summarisation
- Text generation
- Large language models (*LLM*)

>[!note] LLMs are model with emergent capabilities
>Essentially it means that it can <b><span style='color: #FFD700'>perform tasks which the model was not explicitly trained for</span></b>.

>[!question] With LLMs why do we need NLP?
>LLMs are <b><span style='color: var(--mk-color-red)'>unsuitable for many NLP tasks</span></b>. This can be due to:
>- Hallucinations & weak grounding
>- Inefficiency & cost
>- Lack of reliability & determinism
>- Poor interpretability & controllability
>- Poor performance for domain-specific task

In the end there are many ways to evaluate a NLP, however there is a <b><span style='color: #FFD700'>trade off between accuracy and interpretability</span></b>. A better model is more complex but lacks interpretability. So <b><span style='color: #98FB98'>generally it is better to make a model that is more interpretable while sacrificing accuracy</span></b>.
## Core Building Blocks of NLP

We need to understand languages, for English here are the core building blocks, each requiring elements of the previous:
1) **Characters** (*Basic symbol of written language*)
2) **Morpheme** (*Smallest meaning-bearing units of language*)
3) **Word** (*Single unit of language that can be represented*)
4) **Phrases** (*Group of words expressing idea or meaning*)
5) **Clause** (*Phrases with subject & verb*)
6) **Sentence** (*Expresses an independent statement, question, etc*)
7) **Paragraph** (*self-contained unit of discourse in writing dealing with a particular point or idea*)
8) **Document** (*or text*)
9) **Corpus** (*Collection of writings*)
### Morphemes

Morphology is the study of the forms & formation of words in a language. So <b><span style='color: #FFD700'>words are built of morphemes</span></b>, thus they are the <b><span style='color: #FFD700'>smallest meaning-bearing unit</span></b> of language.

**Types of morpheme**
![[Types of Morpheme.png|center|500]]

So a **word is made up** of 1 to n morphemes or, <b><span style='color: #FFD700'>1 to n stems plus 0 to n affixes</span></b>.

>[!info] Affixes are prefixes or suffixes

>[!example] An example of a word
>So we have 2 morphemes, dog (*free is also a word in itself*) & s (*suffix*).
>
> And when combined it forms a word dogs.
> 

>[!warning] There are challenges in Morphology which directly affects NLP
>1) Words are <b><span style='color: var(--mk-color-red)'>not always just concatenations of morphemes</span></b> (*read-able-ity -> readability*).
>2) <b><span style='color: var(--mk-color-red)'>Imprecise meanings</span></b> (*flammable = inflammable != non-flammable*)
>3) <b><span style='color: var(--mk-color-red)'>Complex morphology</span></b> (*other languages have more complex morphology*)
#### Bounded Morphemes

Unlike free morphemes, bounded ones <b><span style='color: #FFD700'>cannot stand alone and must be used with another morpheme</span></b> to form a complete word.

>[!info] Derivational morpheme
>It can be a **prefix or suffix**. They <b><span style='color: #FFD700'>change the sematic meaning</span></b> or the part of speech of the affected word.
>
>>[!example] The word happy, can have a prefix 'un' to form un-happy

>[!info] Inflectional morpheme
>It is **suffix** only. They <b><span style='color: #FFD700'>assign a particular grammatical property</span></b> (*tense, number, possession, comparison*) to the word.
>
>>[!example] The word walk can have a suffix 'ed' to form walk-ed
## Fundamental Tasks

![[Fundamental Tasks of NLP.png|center]]
### Lexical Analysis

Also known as <b><span style='color: #87CEEB'>tokenization</span></b>, it is the <b><span style='color: #FFD700'>splitting of sentences</span></b> or text into meaningful / useful units. 

Different granularity can be applied in practice:
-  Character based (*Does not provide a lot of information & is limited based on the task*)
-  Sub word based (*Morden approach, where the AI learns how to split the text*)
- Word based
### Syntactic Analysis

We can do <b><span style='color: #87CEEB'>part of speech</span></b> (*POS*) <b><span style='color: #87CEEB'>tagging</span></b>  is used where we <b><span style='color: #FFD700'>label each word to a part of speech</span></b>.

>[!note] Some basic POS tags
>- Noun
>- Verb
>- Adjective
>- Conjunction
>- And many more ...

Also there is <b><span style='color: #87CEEB'>dependency parsing</span></b>, where we analyse the grammatical structure of the sentence and <b><span style='color: #FFD700'>find the different types of relationships between words</span></b>.

**Dependency graph example**:
![[Images/CS4248 Images/Dependency Graph Example.png|center]]
### Semantic Analysis

Here we can do <b><span style='color: #87CEEB'>word sense disambiguation</span></b> (*WSD*) which is the <b><span style='color: #FFD700'>identification of the right sense of a word among all possible senses</span></b>. This is because of <b><span style='color: #87CEEB'>sematic ambiguity</span></b> where <b><span style='color: var(--mk-color-red)'>many words have multiple meanings</span></b>.

There is also <b><span style='color: #87CEEB'>named entity recognition</span></b> (*NER*) which is the <b><span style='color: #FFD700'>identification of named entities</span></b> which represent real world objects.

>[!example] Examples of named entities
>John (*person*) booked a Singapore Airlines (*company*) flight to Japan (*location*) for (*money*).

There is also <b><span style='color: #87CEEB'>semantic role labeling</span></b> (*SRL*) which is the <b><span style='color: #FFD700'>identification of semantic roles</span></b> of these words or phrases in sentences. It is like identifying the 5W1H in a sentence.

>[!example] Examples of semantic roles
>The teacher (*who*) sent (*what*) the class (*whom*) the assignement (*what*) last week (*when*).
### Discourse Analysis

Here <b><span style='color: #87CEEB'>coreference resolution</span></b> is carried out which <b><span style='color: #FFD700'>identify expressions that refer to the same entity</span></b> in a text. As entities can be referred to by named entities, noun phrases, pronouns etc.

>[!example] Example of expressions that refer to the same entity
>John did not do his (*referring to John*) homework which it (*homework*) was given to by Mr Tan.

There is also <b><span style='color: #87CEEB'>ellipsis resolution</span></b> which is the <b><span style='color: #FFD700'>inference of ellipses using surrounding context</span></b>.

>[!info] Ellipsis
>It is the omission of a word or phrases in a sentence.
>
>>[!example] She is very funny but her sister is not (*meaning her sister is not funny*).
### Pragmatic Analysis

Here <b><span style='color: #87CEEB'>textual entailment</span></b> is carried out which <b><span style='color: #FFD700'>determines the inference relation between 2 short ordered text</span></b>.

[[Year 3/Sem 1/CS3263 - Foundations of Artificial Intelligence/Propositional Logic.md#Entailment|Entailment]] implies that given a text and a hypothesis if the text is true the hypothesis is also true.

There is also <b><span style='color: #87CEEB'>intent recognition</span></b> which is the <b><span style='color: #FFD700'>classification of intent</span></b> based on what the writer is trying to achieve.

>[!example] Example of intent recognition
>Given some context like location, vegetarian & the text "I'm hungry" shows that the writer intents to find somewhere to eat. Thus the action will be to search for vegetarian places near the location to eat.
>
# Challenges with NLP
---
## Characteristics of Language

The rules of language makes it hard for NLP models to fully understand.
### Ambiguity

Some <b><span style='color: #FFD700'>words may mean different things</span></b> depending on the sentence. It can be on:
- **Word** level (*Bank can be the financial institute or the edge of a river*)
- **Part of speech** (*Run can be a verb or a noun*)
- **Syntactic structure**

Often it <b><span style='color: #FFD700'>depends on context & shard understanding of the world</span></b>.

>[!example] "I killed all the children"
>It could be in a context of a serial killer or a system administrator where new smaller processes are called children.

There is also <b><span style='color: #87CEEB'>anaphoric ambiguity</span></b> where a <b><span style='color: #FFD700'>word or phrase can refer back to different things</span></b> in a sentence.

>[!info] Anaphoric
>Describes a word or phrase (like a pronoun) that refers back to something mentioned earlier in a text for its meaning, helping to avoid repetition and connect ideas.

A good example of this is the <b><span style='color: #87CEEB'>Winograd schema</span></b>, which is a pair of sentences differing only 1 or 2 words & <b><span style='color: #FFD700'>containing an ambiguity that is resolved in opposite ways</span></b>.

This usually requires the usage of world knowledge and reasoning to figure out.

>[!example] An example of a Winograd schema
>"I poured water from the bottle into the cup until **it** was full" compared to "I poured water from the bottle into the cup until **it** was empty". Here "it" refers to 2 different things.

There is also <b><span style='color: #87CEEB'>pragmatic ambiguity</span></b> where the <b><span style='color: #FFD700'>semantics is unclear if the context is unknown</span></b>.

>[!example] Example of a pragmatic ambiguity
>When asked "Do you know what time it is?", could it be a yes no question, or asking for an actual time or some rhetorical question.
### Expressivity

In general the meaning of <b><span style='color: #FFD700'>2 sentences can be the same but is just expressed in different forms</span></b> (*like tone*).

Not only that but in English there are also idioms, neologisms (*noob, chillax*), literality devices (*humor, sarcasm, irony, satire, exaggeration*).

>[!note] Literacy devices emphasis some emotion
> However, it is <b><span style='color: var(--mk-color-red)'>hard for machines to understand</span></b> but for humans it is very simple. <b><span style='color: var(--mk-color-red)'>Things like tone and gestures are lost in plain text</span></b>.

>[!abstract] Algorithms influence how we talk & write
> There are some problematic <b><span style='color: #FFD700'>words which are harmful but to bypass censorship there are alternatives </span></b>.
> 
> For example kill -> unalive or sex -> seggs. Thus algorithms do dictate the things humans write.
### Variation

There is <b><span style='color: var(--mk-color-red)'>no one size that fits all NLP solutions</span></b>. For instance:
- There are difference in underlying task
- Many languages and also language families with their own syntax grammar etc
- Different domains for problems (*news, social media, scientific paper*)
- Cultural differences and biases
### Sparsity

In the English language the <b><span style='color: var(--mk-color-red)'>most common words does not provide a lot of information</span></b> of the sentence.

>[!tldr] Zipf's Law
>It states that <b><span style='color: #FFD700'>word frequencies are inversely proportional to their rank</span></b>. Meaning that the 3rd most common word appears one third as frequent as the first.

So regardless of the corpus there will be a lot of infrequent words.
### Scale

There are about 6,500 different languages & approximately 150 language families. Just English a lone there are around 470,000 words and with an abundant of corpuses there is a lot to learn.

In addition, <b><span style='color: #FFD700'>language is unbounded</span></b>, new words can be invented or the meaning of existing words can change.
## Practical Challenges

### Data Collection

To train a model we need data and here are **3 source collection methods**:
1) **Public datasets**
2) **Public APIs** 

>[!success] It can come with metadata which can be useful

3) **Web scraping** (*Usually it will be in HTML format*)

>[!fail] Has a legal grey area

>[!fail] It has practical challenges
>For instance, dynamic content or anti-scraping measures.

>[!fail] HTML itself contains many tags with unwanted data
>These includes headers, footers, navigation bar and many more.
### Data Conversion

No only that but after collecting data, we need to do **data conversion**. Most <b><span style='color: var(--mk-color-red)'>data collected are not "ready-to-use"</span></b>. Typically <b><span style='color: #FFD700'>conversion to plain text or markdown is required</span></b>. 

The difficulty lies in the <b><span style='color: var(--mk-color-red)'>numerous text formats</span></b> like PDF, HTML. DOCX (*XML*) requires different standards to extract relevant content.

>[!warning] Conversion itself might have some issues 
> For instance 2 characters may <b><span style='color: var(--mk-color-red)'>look the same but on a byte level they can be different</span></b>.
> 
> Typically a similarly threshold is used to determine if 2 texts are similar.
### Data Quality

As the saying goes garbage in garbage out. The **challenge is getting high quality data**. 

>[!danger] Data is the most time consuming & costly to prepare

There are various aspects that related to low quality data like:
- Poor spelling and grammar
- Strong biases
- Toxicity
- Sensitive data
- Duplicate

>[!tldr] Duplicate
>It is a common occurrence in web crawls which leads to <b><span style='color: var(--mk-color-red)'>slower training & higher risk of memoization</span></b>. <b><span style='color: #87CEEB'>Deduplication</span></b> itself can be challenging as it is a <b><span style='color: var(--mk-color-red)'>resource intensive task to identify if it is actually a duplicate</span></b>.

>[!tldr] Toxicity & biases
>These are improper content (*misinformation, biased remarks, racism etc*). To identify these, <b><span style='color: #98FB98'>rely on content from trusted sources</span></b> or do <b><span style='color: #98FB98'>crowdsource quality control</span></b>.

>[!tldr] Sensitive data
> Datasets may contain personally identifiable information or sensitive information which should not be used for training.

**Here are some strategies to filer out low-quality data**:
![[Methods to Filter Out Low Quality Data.png|center]]

There is also a need for <b><span style='color: #87CEEB'>data decontamination</span></b>. In a model hyperparameter turning is important which is based on training and **validation data**. This <b><span style='color: #FFD700'>validation set must be separate from the training data</span></b>.

So the hard part is that data can be contaminated, we are <b><span style='color: var(--mk-color-red)'>not sure what data the LLM is trained on</span></b> and there is <b><span style='color: var(--mk-color-red)'>no guarantee that the test data contains some initial training data</span></b>.

This also leads to <b><span style='color: #87CEEB'>AI-inbreeding</span></b>. <b><span style='color: #FFD700'>LLMs generate data which is used to train other LLMs</span></b>, this data is known as <b><span style='color: #87CEEB'>syntactic data</span></b>. This can lead to <b><span style='color: var(--mk-color-red)'>model quality degradation</span></b> (*model collapse*), <b><span style='color: var(--mk-color-red)'>amplification errors & biases</span></b>.

