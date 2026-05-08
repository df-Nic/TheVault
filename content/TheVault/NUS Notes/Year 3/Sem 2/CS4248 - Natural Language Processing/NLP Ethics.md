---
Title: NLP Ethics
Date Created: 16-March-2026
Last Updated: 16-March-2026
Tags:
  - CS4248
  - AI/Ethics
---
# Why Is This Important?
---
Now a wide range of very common & popular services are based on NLP we all use (*online search / information retrieval, machine translation, chatbots*). Also many <b><span style='color: #FFD700'>NLP applications making decisions affecting people's lives</span></b> (*content censorship*).

Language does not exist in isolation:
- Natural language is what humans gave, give, and will give meaning to written and spoken word
- Humans have different knowledge, beliefs, biases, preconceptions

But AI can be <b><span style='color: #FFD700'>useful and it can also be harmful</span></b> (*fake content, privacy intrusion*).

But not everything a harmful NLP model does it based on the model itself, typically if we have a **biased society, we will get a dataset** which our model will pick up, thus this is an <b><span style='color: #FFD700'>unintentional side effect which is caused by us</span></b>.
# Bias In NLP
---
Many tasks can face bias:
- Word embeddings
- Language identification
- Sentiment analysis
- and many more

And many of these <b><span style='color: var(--mk-color-red)'>issues come from bias datasets</span></b>. Take our word embeddings, we do not want the case where by the vector of Poor + man = useless.

So can we **measure bias**? An approach is to find the <b><span style='color: #FFD700'>nearest set of words to a particular group</span></b>. And we can conveniently do this using <b><span style='color: #FFD700'>cosine similarity</span></b>.

$$
cosine(v(grp1) - v(grp2), v(x) - v(y))
$$
So essentially the formula above is to check if we take 2 groups and then 2 words and subtract them for each group, if they are similar means there are biased based on the 2 groups.

>[!example] Lets say she - he is similar to nurse - surgeon, these 2 can be similar depending on the context of the dataset
>

>[!warning] But not all words should be removed like sister and brother they are not bias it is just what the word mean
>What we can do is to do principle component analysis. Then we can train a binary classifier to predict if its neutral or specific to the group.

Then we can debias our embeddings using the following formula:
![[Debiasing Word Embeddings.png|center]]

The above is our <b><span style='color: #FFD700'>loss function</span></b>:
- The left hand side says keep the original embedding the same, do not change too much
- The right hand side says to change words that are bias to something neutral


