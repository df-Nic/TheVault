---
Title: Strings & Words
Date Created: 20-January-2026
Last Updated: 27-April-2026
Tags:
  - CS4248
  - AI/NLP/TextProcessing
---
# Regular Expression (RegEx)
---
>[!tldr] Regular expression is a pattern to match a combination of characters in a string
>A common misconception is that regular expression looks for words, but in fact it <b><span style='color: #FFD700'>looks for the sequence of words based on search pattern</span></b>.

**Common application** for regular expression:
- Parse text documents to find specific character patterns
- Validate text to ensure it matches predefined patterns
- Extract, edit, replace, delete substrings matching a pattern

>[!info] Default search
>Finding the <b><span style='color: #FFD700'>first</span></b> occurrence of the pattern.

>[!info] Global search
>Finding <b><span style='color: #FFD700'>all</span></b> occurrence of the pattern.
## Basic Concepts of Regular Expression
### Fixed Patterns

They are the most simplest notations in regular expression where they <b><span style='color: #FFD700'>find the exact match given a pattern</span></b>.

>[!example] Example of a fixed pattern
>Given a regular expression of `floor`, the following will be highlighted "My block has 15 **floor**s, and I live on **floor** 5".

>[!fail] Very little flexibility since it does an exact match
### Metacharacters

To <b><span style='color: #FFD700'>add more flexibility</span></b>, we can use metacharacters.

|     Character     |                           Explanation                            |
| :---------------: | :--------------------------------------------------------------: |
|         .         |             Matches any character except line breks              |
|         ^         |                   Match the start of a string                    |
|         $         |                    Match the end of a string                     |
| \| (*Logical OR*) |         Matches RegEx either before or after the symbol          |
|        \b         |             Matches boundary between word & non-word             |
|        \d         |                   `[0 - 9]`, matches any digit                   |
|        \D         |                `[^0 - 9]`, matches any non-digit                 |
|        \s         |         `[ \n\r\t\f]`,  matches any whitespace character         |
|        \S         |       `[^ \n\r\t\f]`, matches any non-whitespace character       |
|        \w         | `[a-zA-Z0-9_]`, matches any word character, including underscore |
|        \W         | `[^a-zA-Z0-9_]`, it matches any non-word character + underscore  |
>[!important] When matching string if we used '^' & '$' it will match for the entire string
>For example if we want to match CS4248, then in this sentence "I am taking CS4248" it will not detect it. Only if it is just "CS4248" and nothing else.

>[!note] Strings are just a sequence of characters which includes whitespaces & special characters

>[!info] Non-Words
>A non-word is essentially anything that is a <b><span style='color: #FFD700'>whitespace or a punctuation</span></b>.
### Character Classes

It defines a <b><span style='color: #FFD700'>set of valid characters</span></b> instead of just 1 specific character.

It can be written as `[...]` and it can be **negated** as well by adding the ^ character like so `[^...]`.

>[!important] If we encase any special characters inside a `[]` it means we are looking for that character
>For example `^` is to match the start of a string but `[a^b]` means we are finding the '^' character (*if there is other characters do not put it at the front*).

>[!example] Example of using a character class
> Lets say our RegEx is `[0-9][^a-z]`, we want to match 2 sequences of characters where the first is a digit the 2nd is a non lowercase letter.
> 
> So for this string, the following will be highlighted: "My block has **15** floors, and I live on floor **5.**".
### Repetition Patterns

We can use repetition patterns to <b><span style='color: #FFD700'>match patterns with flexible lengths</span></b>. These special character are also [[Year 3/Sem 2/CS4248 - Natural Language Processing/Strings & Words.md#Metacharacters|metacharacters]].

|    Pattern     |                          Explanation                           |
| :------------: | :------------------------------------------------------------: |
|       +        |                     1 or more occurrences                      |
|       *        |                     0 or more occurrences                      |
|       ?        |                       0 or 1 occurrences                       |
|      {n}       |                     Exactly n occurrences                      |
|     {1, n}     |                   Between 1 & n occurrences                    |
| {1, } or {, n} | Unbounded ranges, the 1st is 1 or more, the 2nd is less than n |
>[!example] Example of using repetition patterns
> If we have a RegEx `\b\w{2,4}\b`. Then with the following string these will be highlighted: "**My** block **has** **15** floors, **and** I **live** **on** floor **5.**"
### Groups

We can <b><span style='color: #FFD700'>organise patterns into parts</span></b>. These parts are just sub patterns within the overall larger pattern.

Groups are enclosed using `( )`, which can be nested within multiple groups And they <b><span style='color: #FFD700'>capture patterns individually</span></b>.

But this <b><span style='color: var(--mk-color-red)'>does not mean that only 1 group has to match</span></b>, the whole expression must still match in the end.

>[!important] Groups are ordered or indexed based on when they are opened

>[!example] Example of using groups
>Lets say we have a RegEx, `([\w.-]+)@([\w.-]+)`. We have 2 groups and it will match the following string `allice@gmail.com `.
>
>In group 1 we will have a match for `allice` and in group 2 it will be `gmail.com`.
#### Backreferences

It is used along side groups where we can <b><span style='color: #FFD700'>reference a group for repeated patterns</span></b>.

We use `\{group_number}` to denote the backreference to a specific group.

>[!important] Backreferences must contain the same pattern of characters as captured by the referenced group

>[!example] Example of using a backreference
>Assuming we want to find string which starts & end with the same character. Then we can use the following RegEx, `(\b([a-zA-Z])\w*\2\b)`.
>
>Here the `\2` is the backreference to group 2.
### Lookarounds

These are to <b><span style='color: #FFD700'>check for a pattern before or after the main match without including that pattern</span></b> in the final result. These are also known as <b><span style='color: #87CEEB'>assertions</span></b>.

There are 2 types:
1) **Lookaheads**
2) **Lookbehinds**

And there are 2 forms of assertions:
1) **Positive**
2) **Negative**

| Pattern |        Type         |                                    Explanation                                    |
| :-----: | :-----------------: | :-------------------------------------------------------------------------------: |
|  (?=)   | Positive lookahead  |    `A(?= B)` means to find expression A but only when followed by expression B    |
|  (?!)   | Negative lookahead  | `A (?! B)` means to find expression A but only when not followed by expression B  |
|  (?<=)  | Positive lookbehind |   `A (?<= B)` means to find expression A but only when preceded by expression B   |
|  (?<!)  | Negative lookbehind | `A (?<! B)` means to find expression A but only when not preceded by expression B |
>[!example] Example of using lookarounds
>Given this RegEx, `[0-9.,]*[0-9]+(?=\s*kg)`, with the following text this will be highlighted, "Paying 10 SGD for **1,500.00** kg of chicken seems fair.".
## Finite State Automata

With **RegEx**, we can <b><span style='color: #FFD700'>describe regular languages</span></b>. And how is this link to <b><span style='color: #87CEEB'>final state automata</span></b> (*FSA*) is that it is <b><span style='color: #FFD700'>accepted by FSA</span></b>.

![[Using FSA to Describe RegEx.png|center]]

>[!quote] Chomsky Hierarchy
> It's a classification system for formal grammars and languages. It classify regular languages are the most restricted types of languages.

>[!fail] Limitations with RegEx
>FSA bring finite means that we have a finite amount of memory. Thus the limitations is that it <b><span style='color: var(--mk-color-red)'>cannot handle arbitrary nesting or grouping</span></b>.
>
>>[!example] For example finding a string with the same number of 0 & 1
>>We need memory to keep track of the number of 0s which can be an arbitrary amount.
## Error Types

In text with many notations (*decimal, scientific, etc*) it requires more <b><span style='color: var(--mk-color-red)'>complex regular expression</span></b> especially if the text contains different notations and ways of writing something.

There are 2 types of errors:
1) **False positives**
2) **False negatives**

>[!info] False positives or type 1
> Matches string that should not have matched.

>[!info] False negatives or type 2
> Not matching things that should have been matched.

However depending on the context these <b><span style='color: #FFD700'>error types are not equally bad</span></b>. In finance for example, it is better if we detect false positives as the risk of default might be an issue.

But typically there is a <b><span style='color: #FFD700'>trade off between the 2</span></b>. Reducing false positives increases false negatives and vice versa.
# Corpus Preprocessing
---
Here we will discuss techniques to extract tokens from our corpus.

>[!info] Tokens
>They are <b><span style='color: #FFD700'>character sequence with semantic meaning</span></b> to the model but is <b><span style='color: #FFD700'>might not always be an actual word</span></b>.
## Tokenization

It is the act of <b><span style='color: #FFD700'>splitting strings into tokens</span></b> which will make up the <b><span style='color: #87CEEB'>vocabulary</span></b> (*all the unique tokens*) for the model.

>[!important] One of the most important steps in NLP algorithms
>Bad tokenisation leads to bad models, <b><span style='color: #FFD700'>garbage in garbage out</span></b>.

There are some **challenges** to this:
1) **Canonical forms** (*separate our clitics, keep hyphenated words together, separate out punctuation*)
2) **Stop words**, words that provide no meaning & are considered noise (*an exception can be not since it switches the semantics*)
3) **Non standard tokens** (*like URs, emojis, emoticons, etc*)

But there are 3 basic approaches to tokenization:
1) **Character** based
2) **Sub word** based
3) **Word** based

>[!fail] Character based though simple is rarely useful
>Single characters does not provide a lot of information.

In the end how we <b><span style='color: #FFD700'>tokenization all depends on the data & the task we are doing</span></b>. So try an assess different ones and see which one brings a better result.

>[!note] As a side note, if we are using a LLM to tokenize we are using same tokenizer the LLM is train for
### Word Based

There are 2 intuitive approaches to do word based tokenization:
1) Match all **words, numbers & punctuation** (`\w+|\d+|[,.;:]`)
2) Match **boundaries between words & non-words** (`(?=\W)|(?<=\W)`)

It may seem simple but it gets complicated. 

>[!warning] Numerous text formats causes incorrect splitting of text
>Take for instance the 1st approach. Given a email address, "john@gmail.com". We can see that this email is broken up into "john", "gmail", ".", "com".

>[!warning] Not suitable for all languages
>Special characters in other languages might give context or meaning to the words.
>
>There are also compound nouns which in German is glued together

However the 2 approaches all comes under the <b><span style='color: #FFD700'>assumption that whitespaces are used to separate words</span></b>. Some <b><span style='color: var(--mk-color-red)'>languages does not even use whitespaces</span></b>.

>[!tldr] Maximum matching
>Is a good method of doing word splitting <b><span style='color: #FFD700'>for languages that do not use whitespaces</span></b>.
>
>How it works is that it will <b><span style='color: #FFD700'>find the longest subsequence of characters that matches a word in a dictionary</span></b>.
>
>>[!fail] This does not work so well for English
>>For example "wetrain" is it wet rain or we train. But typically there are solutions which uses probability to see which one is most probable.
### Sub Word Based

A problem arises when **building statistical models** due to <b><span style='color: var(--mk-color-red)'>unseen or rare words</span></b>.

Here we use, <b><span style='color: #FFD700'>prior specification of rules or essentially data-driven algorithms or models</span></b> to split our text into tokens.

>[!success] Addresses the out of vocabulary problem
>OOV words are words that are not seen by the model during training

>[!success] Handles rare words by breaking it down to some known frequent tokens
>This also limits the vocabulary since we can encounter slangs, shortforms etc.

>[!fail] Unexpected results from varied text formats
>With text there can be <b><span style='color: var(--mk-color-red)'>abbreviations, slang, etc</span></b> which can cause unexpected tokens to be formed.
>
><b><span style='color: var(--mk-color-red)'>Orthography</span></b> (*how the word is written*) as well. This inconsistency can be different causing different splits even though they mean the same (*like egg or EGG*).

>[!fail] "Arbitrary" splitting of numbers
>Common numbers like 100, 1000 might be split correctly but <b><span style='color: var(--mk-color-red)'>rare numbers</span></b> might result in unwanted splitting.

In a sub word based tokenization algorithm it generally consist of 2 parts:
1) Token **learner** (*takes a raw text & learns the vocabulary*)
2) Token **segmenter** (*takes a raw text and tokenizes it according to the vocabulary*)
#### Byte-Pair Encoding (BPE)

 In BPE, how it **learns tokens** is by following this simple algorithm:
 1) Do pre-tokenization on the corpus by <b><span style='color: #FFD700'>splitting everything into characters</span></b>
 2) Initialise vocabulary with all the characters plus a underscore (*end of word token*)
 3) Find the <b><span style='color: #FFD700'>2 most frequently adjacent tokens</span></b>
 4) <b><span style='color: #FFD700'>Add the 2 merged tokens</span></b> into the vocabulary
 5) <b><span style='color: #FFD700'>Replace the 2 most frequent tokens with the merged value</span></b>
 6) Repeat steps 3 to 5 until k merges have been done

We **denote the merge** with the following notation `(e, s)`. This means that token e & s are the most frequent adjacent tokens and will be merged to become `es`.

>[!question] Why do we need the end of word token?
> 
> We need this during **decoding**. When doing text generation the model will give a list of tokens, this end of word token <b><span style='color: #FFD700'>denotes when to not merge with the next token</span></b>.
> 
> >[!example] [new, er_, car] -> Car will be a word & newer will be the other word

>[!note] If K = 0, the vocabulary will just be characters & if K = $\infty$ it will eventually be word based tokenization

After learning, BPE will now **tokenize the text** by following this algorithm:
1) Similarly split everything into characters
2) <b><span style='color: #FFD700'>Run each merge in the order they have been added/learned</span></b>
3) Repeat step 2 until no possible merge can be done
4) The remaining tokens will be its final output

>[!example] Example of BPE tokenizing
>Lets say our merge order is "(e, s), (es,  t), (est, \_), (n, e), (ne, w), (new, est_), (e, r), (er, \_)" & our word is "newer". Then the following will happen:
>1) "n e w e r \_"
>2) "ne w e r \_"
>3) "new e r \_"
>4) "new er \_"
>5) "new er\_" (*These will be our final tokens since we cannot do any more merging*)
#### WordPiece

WordPiece is almost identical to [[Year 3/Sem 2/CS4248 - Natural Language Processing/Strings & Words.md#Byte-Pair Encoding (BPE)|BPE]] however with these slight differences in the **tokens learner**:
- First the **"\_"** special character now <b><span style='color: #FFD700'>marks the continuation of a word</span></b>. Thus in pre-tokenization all characters will lead with a "\_" <b><span style='color: #FFD700'>except the first character</span></b> of a word
- Instead of most frequent adjacent tokens, we now <b><span style='color: #FFD700'>take the 2 most likely adjacent tokens</span></b>
- WordPiece also <b><span style='color: #FFD700'>denote merges differently</span></b>

>[!example] Example of another merge notation
>Given a merge (a \_p, ap) it means that characters "a" and "\_p" will be merged to form the new token "ap". 
>
>Similarly if we have (\_e \_r, \_er) it means the 2 will be combined to form the new token "\_er". 

To **compute the likelihood** we use <b><span style='color: #87CEEB'>point-wise mutual information</span></b> & compute it as such:
$$
\frac{P(t_{1}, t_{2})}{P(t_{1})P(t_{2})}
$$
Where:
- $t_{1}$ & $t_{2}$ are tokens 1 and 2
- $P(t_{1},t_{2})$ is the probability of token 1 appearing before token 2 or in other words $P(t_{2} \vert t_{1})$
- $P(t_{1})$ is the probability of token 1 appearing in the entire corpus

We can **simplify the equation** into:
$$
\frac{\text{count}(t_{1}, t_{2})}{\text{count}(t_{1}) \times \text{count}(t_{2})}
$$
Where:
- $\text{count}(t_{1}, t_{2})$ is just the BPE

This is true because $P(t_{1}, t_{2}) = \text{count}(t_{1}, t_{2}) / \text{count}(t_{1})$. And similarly $P(t_{1}) = \text{count}(t_{1}) / N$. So if we were to plug these into the original equation we will end up with the simplified version.

>[!note] When you try to plug in the equations $N$ will be in the numerator of the simplified equation
>We <b><span style='color: #FFD700'>ignore</span></b> $\color{#FFD700}{N}$ as it does not affect the relative differences.

>[!success] This approach favours pairs who rarely appear
>Imagine if 2 characters are supposed to be together for example "e" & "r" but in the raw text this occurrence rarely happen. In BPE this will be ignored but in WordPiece it has a chance to be considered.
## Normalization

With a lot of noise or "randomness" in text normalization's goal is to <b><span style='color: #FFD700'>convert text into a canonical form</span></b> (*standard form*).

We can create a set of <b><span style='color: #87CEEB'>equivalence classes</span></b> which any text which falls under this class will be convert to a specific text / token.

>[!success] This sometimes solves the orthography issue as now we do not care how the word is written

>[!example] Example of normalisation
>Assuming our text contains USA, U.S.A, US of A, all this when normalized will become USA.
### Case folding

Case folding is the process of <b><span style='color: #FFD700'>converting all characters to lowercase</span></b>. It is a common application in information retrieval.

>[!failure] Uppercase character might mean different meanings
>MOM vs mom, one can refer to the abbreviation for ministry of manpower while the other refers to mother.

>[!question] When to not fold?
>It depends on the NLP task. If <b><span style='color: #FFD700'>letters or words are important features</span></b> then do not fold.
>
>>[!example] Maybe the distinction between us and US is important for the task at hand
## Stemming & Lemmatization

Sometimes 2 sentences mean the same to us but to the machine it is different. So stemming & lemmatization <b><span style='color: #FFD700'>handles similar sentences but with different syntax</span></b>.

Where do these variations come from:
- Singular vs plural form
- Different tenses of verbs
- Comparative/superlative of adjectives
### Stemming

The idea of stemming is to <b><span style='color: #FFD700'>reduce words to their stem form</span></b> by cutting of affixes based on the rules these stemmers apply.

>[!success] Fast to do

>[!success] No lexicon required
>It does not need a dictionary or a vocabulary to do stemming.

>[!fail] Stemmed words does not necessarily result in a proper word in the dictionary
> This can ignored as even though this is not a word we <b><span style='color: #FFD700'>just want it all to be compact to the same word</span></b> because all that matters is how the model understands this.

>[!fail] Potential loss in meaning of the word
>Words of different meaning can be stemmed into the same word.

>[!example] An example of a stemmer is the Porter Stemmer
> Used mostly for English text, is a <b><span style='color: #FFD700'>set of rules applied in some sequence determined by linguist</span></b>.
> 
> At each step it applies one or more rules and the output will be fed to the next step.
> 
> It is <b><span style='color: #98FB98'>simple, efficient and yields good results in practice</span></b>.
### Lemmatization

Similarly to stemming lemmatization <b><span style='color: #FFD700'>reduces infectious or variant forms to a certain base form</span></b>. But unlike stemming, it <b><span style='color: #FFD700'>requires to know the part of speech</span></b> (*verb, noun, adj, etc*) before converting it.

>[!example] Example of lemmatization
>Assuming our word is "running" and in the context it is a noun it will be converted into "running". If it is a verb it will be converted into "run" instead.

For any word that <b><span style='color: #FFD700'>does not have some word form then it will be returned unchanged</span></b>.

>[!success] Lemmatized words are proper words
>Words from the dictionary

>[!success] Can normalize irregular forms
>For instance "worst" can be converted to "bad" & "went" to "go".

>[!fail] Requires curate lexicons / lookup tables and some rules typically

>[!fail] Requires part of speech tags for correct results

>[!fail] Generally slower than stemming
## Segmentation

Here we want to <b><span style='color: #FFD700'>segment a corpus into sentences</span></b>.

>[!warning] Might seem simple but the period symbol "." can be ambiguous
> For example decimals can cause incorrect splitting. While <b><span style='color: var(--mk-color-red)'>poor punctuation</span></b> (*missing whitespace or capitalisation*) poses issues as well in segmentation.
> 
> Because of these issues to <b><span style='color: var(--mk-color-red)'>create a RegEx can become very complex</span></b>.

An alternative approach is to use a <b><span style='color: #FFD700'>binary classifier to classify if it is a end of sentence or not</span></b>. It can use machine learning or a set of handwritten rules or even RegEx.

**Example of a binary EOS classifier**:
![[Binary End of Sentence Classifier.png|center|450]]

We can also use **numerical features** as well:
- Length of word before or after the period
- Distance (*in characters*) to the next punctuation mark
- Probabilities derives from a dataset
