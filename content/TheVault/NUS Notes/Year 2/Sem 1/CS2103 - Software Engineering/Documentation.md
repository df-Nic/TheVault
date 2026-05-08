---
title: Documentation
Date Created: 2024-10-21
Last Updated: 2025-09-28
tags:
  - CS2103
  - SWE
  - Documentation
---
# Types of Developer Documentation
---
There a <span style='color:var(--mk-color-orange)'>2 forms of dev-to-dev documentation</span>:
1) **Developer as a user**
Components will be **reused by other developers**, and developers will need to document how:
- To use API (*API documentation*) in <span style='color:var(--mk-color-yellow)'>small, independent and easy to use chunks</span>
- <span style='color:var(--mk-color-yellow)'>Explaining the functions</span> as well as high level explanations of how to use the API (*Tutorial-style*)

2) **Developer as a maintainer**
If the components will be **developed by other people** then, the <span style='color:var(--mk-color-yellow)'>design, implementation and tests must be documented</span>.

This type is <span style='color:var(--mk-color-red)'>harder to write</span> since **explaining can be complex** but they will have access to the source code, thus <span style='color:var(--mk-color-yellow)'>documentation can be done in comments</span> which serves as complementary source information

**Examples of how to do documentation**
![[Documentation Example.png|center|400]]

Documentation is not only for developers but <span style='color:var(--mk-color-yellow)'>also for users as well</span>. It is best<span style='color:var(--mk-color-yellow)'> kept in text</span> format and a <span style='color:var(--mk-color-yellow)'>writer-friendly source format</span> is also desirable (*Non-programmers might edit documentation*).

Some useful <span style='color:var(--mk-color-orange)'>tools for documentation</span>:
1) **Markdown**
2) **AsciiDoc**
3) **PlantUML**
# Comprehensibility
---
It is not enough for the documentation to be **accurate** and **comprehensive**; it should <span style='color:var(--mk-color-yellow)'>also be comprehensible</span>.

> [!info] Tips on Comprehensibility
> - Use plenty of **diagrams** - Pair this with words
> - Use plenty of **examples** - Help visualise the process
> - Use **simple** and **direct** explanations - No long sentences and fany words
> - <span style='color:var(--mk-color-red)'>Do not</span> include **redundant statements**
> - <span style='color:var(--mk-color-red)'>Do not</span> **seperate sections** for each type of artifact (*Diagrams*) - If they have no purpose, put under appendix as reference
# Top-Down Description
---
A **top-down breadth-first** explanation is <span style='color:var(--mk-color-green)'>easier to understand</span> than a bottom-up one.

The main reason is that the reader will <span style='color:var(--mk-color-yellow)'>start at the top</span> and will travel down some path until they find something they are interested in. They <span style='color:var(--mk-color-yellow)'>do not need to search up and down to learn something</span>.

> [!example] Writting in a Top-Down Manner
> Lets have `System` which consist of `GUI` and `Logic`.
> 
> 1) Describe beifly what is `System`, then followed by a high level overview of `System`
> 2) Then we can go into lets say `GUI`, then start with high level then go down into the components of `GUI`
> 3) Then do the same for `Logic`
> 
> Essentially <span style='color:var(--mk-color-yellow)'>start with a parent</span> of the component before talking about its sub components.
# Minimal But Sufficient
---
Aim to write just enough, since <span style='color:var(--mk-color-red)'>maintaining documents is an overhead</span>, try and <span style='color:var(--mk-color-yellow)'>minimise the documentation</span> but make sure it <span style='color:var(--mk-color-yellow)'>provides just enough guidance</span> with the complement of the code.

Try and **describe something in a high-level** which <span style='color:var(--mk-color-yellow)'>cannot be visible </span>in the **code** or **comments**.

Also refrain from copy large texts for describing similar components. One should:
- Describe the <span style='color:var(--mk-color-yellow)'>similarities in one place</span>
- In other places you can **link back to the similarity** but more importantly <span style='color:var(--mk-color-yellow)'>emphasize only differences</span>.