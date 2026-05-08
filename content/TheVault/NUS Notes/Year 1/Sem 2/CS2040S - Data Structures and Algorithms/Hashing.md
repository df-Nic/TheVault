---
title: Hashing
Date Created: 2024-03-11
Last Updated: 2025-10-20
tags:
  - CS2040S
  - DataStructures/HashTables
---
# Symbol Table
---
It is basically a data structure that <span style='color:#f7b731'>stores a list of a key-value pair</span>, but instead of being stored like a tree, it is like a table where searching is <b><span style='color: var(--mk-color-green)'>O(1)</span></b> time.

| Operation  |                 Description                 |
| :--------: | :-----------------------------------------: |
|  `insert`  |   Insert a key value pair into the table    |
|  `search`  | Retrieve the value paid with the key given  |
|  `delete`  |    Remove the key value pair if it exist    |
| `contains` |     Is there this key inside the table      |
|   `size`   | Total number of key value pair in the table |
The <span style='color:#fa8231'>cost</span> of this fast running time is that the <span style='color:#eb3b5a'>other functionality of the trees cannot be applied.</span>.

**Characteristics of a key :**
- It must be <span style='color:#f7b731'>unique</span>
- <span style='color:#f7b731'>Immutable</span> as it will cause the keys to be misaligned. (<span style='color:#20bf6b'>Good to use java reference types</span> like `String`, `Integer`)

Now in <span style='color:#8854d0'>java</span> there is a class called <span style='color:#8854d0'>map</span> however this is <span style='color:#f7b731'>just an interface</span>, the correct class to use is a <span style='color:#8854d0'>HashMap</span>.

A <span style='color:#8854d0'>TreeMap</span> (**Dictionary**) however supports more functionality since it is a ordered data structure.
## Direct Access Tables

It is the most simple type of table where it is just an <span style='color:#8854d0'>array</span>, where <span style='color:#f7b731'>each index is assigned to a key</span>.

Clearly there are <span style='color:#eb3b5a'>some problems</span> with this :
- This only works on <span style='color:#f7b731'>small number of keys</span> but in reality there millions of different keys
- <span style='color:#f7b731'>Keys</span> can be <span style='color:#f7b731'>strings</span> or <span style='color:#f7b731'>floats</span>.

Now setting a big array size, like say $2^{170}$ to accommodate the all possible strings is <span style='color:#eb3b5a'>too much space needed</span>. One way to reduce the space needed is through <span style='color:#0fb9b1'>hash functions</span>.
# Hash Functions
---
Now let $U$ be the <span style='color:#fa8231'>universe of all keys</span>! But take a smaller subset $K$ and these will be the keys that will be used. These $K$ keys will be used to <span style='color:#f7b731'>map each item into</span> $\color {#f7b731} {m}$ <span style='color:#f7b731'>buckets</span>.

This <span style='color:#2d98da'>hash function</span>, will take a key and <span style='color:#f7b731'>convert</span> it into some value <span style='color:#f7b731'>corresponding to the bucket position</span>. The time taken is the <span style='color:#fa8231'>time</span> to <span style='color:#f7b731'>compute the hash value</span>, and <span style='color:#f7b731'>access the bucket</span>. But it is usually assumed to be <b><span style='color: var(--mk-color-green)'>O(1)</span></b> time <span style='color:#f7b731'>unless stated</span>.

This <span style='color:#2d98da'>hash function</span> must also be a <span style='color:#f7b731'>simple uniform hashing algorithm</span>, to ensure that every key is equally likely to map to every bucket.

With this, it can be expected that :
- **Load per bucket** = $n/m$ where $n$ is the number of items on average and $m$ is the number of buckets.
- **Expected Search Time** = $1 + \text{load per bucket}$ where the O(1) is the hashing function and array access.
## Hash code

When a item is placed into a hash function its output is called a <span style='color:#0fb9b1'>hash code</span>.

**Properties**
- If the value is the **same** the <span style='color:#f7b731'>hash code should be the same</span>
- If 2 objects are **equal**, the hash code should also be the same

In <span style='color:#8854d0'>java</span>, there is a function called `hashcode()` which basically hashes the item. For this to work for an object, firstly <span style='color:#f7b731'>define how to hash a particular item</span>, secondly <span style='color:#f7b731'>redefine what is equals</span> (`equals()`) so that java knows if these 2 are equal then it will output the same hash code.

**Properties of `equals()`** :
1) **Reflexive**
2) **Symmetric**
3) **Transitive**
4) **Consistent** (Always return the same answer)
5) **Null is null** (`x.equals(null)` should output `false`)
<div style="break-after: page;"></div>

## Collisions

Now lets use this <span style='color:#2d98da'>hash function</span> and, oh no <span style='color:#eb3b5a'>2 items have the same hash value</span>, this is known as a <span style='color:#0fb9b1'>collision</span>.

As long as the table size or the <span style='color:#f7b731'>buckets</span> is <span style='color:#f7b731'>smaller than every possible key value</span> it is <span style='color:#f7b731'>impossible to avoid this</span>.

Well, just <span style='color:#fa8231'>change</span> the <span style='color:#2d98da'>hash function</span>, but it is hard to find one that does not collide and the whole table needs to be rebuilt (<span style='color:#eb3b5a'>slow</span>) and there is too many cases to consider.
### Separate Chaining

The main idea of this is that if <span style='color:#fa8231'>2 items have the same hashing value</span>, then just <span style='color:#f7b731'>put both in the bucket</span>.

This can be achieved with<span style='color:#8854d0'> java's link list</span>. Every item that encounters a <span style='color:#f7b731'>collision</span>, then just <span style='color:#f7b731'>add it into the link list</span>.

Think of a <span style='color:#8854d0'>link list</span> as a <span style='color:#f7b731'>item that points to the next item and so on</span>, thus adding will take <b><span style='color: var(--mk-color-red)'>O(n)</span></b> time, unless there is a <span style='color:#0fb9b1'>tail pointer</span> to the back then it will be <b><span style='color: var(--mk-color-green)'>O(1)</span></b> time or just <span style='color:#f7b731'>add to the front</span>. 

What is the <span style='color:#fa8231'>space required</span>, since there is $m$ <span style='color:#fa8231'>buckets</span> and a possible $n$ items in the <span style='color:#8854d0'>link list</span>, the total space is <b><span style='color: var(--mk-color-green)'>O(m + n)</span></b>.

How about `searching`, well first the the <span style='color:#f7b731'>key must go through the hash function</span> which will be <b><span style='color: var(--mk-color-green)'>O(h)</span></b>, the it has to <span style='color:#f7b731'>loop through each item</span> in the <span style='color:#8854d0'>link list</span>, which is <b><span style='color: var(--mk-color-red)'>O(n)</span></b> time for a total of <b><span style='color: var(--mk-color-red)'>O(n + h)</span></b> time.

The <span style='color:#fa8231'>worst case</span> is <b><span style='color: var(--mk-color-red)'>O(log n)</span></b> or a tighter bound of <b><span style='color: var(--mk-color-red)'>O(log n / log log n)</span></b>.
### Open Addressing

The idea of <span style='color:#0fb9b1'>open addressing</span> is if there is a collision, then <span style='color:#f7b731'>find another bucket that is available</span>.

The <b>invariant</b> is that for each sequence in the probing, every $n + 1$ probe, the $n$ probe must be filled (A collision) .

The <span style='color:#fa8231'>sequence for the probing</span> method <span style='color:#f7b731'>must be the same</span> for both <span style='color:#2d98da'>insert</span>, <span style='color:#2d98da'>search</span> and <span style='color:#2d98da'>delete</span> functions.

If finding for a key and a <span style='color:#f7b731'>empty bucket </span>is found then the <span style='color:#f7b731'>item is not in the table</span>.

However, some <span style='color:#eb3b5a'>issues</span> will arise during <span style='color:#2d98da'>deletion</span>, as by deleting, it <span style='color:#f7b731'>results in gaps</span> within the table and it is possible during probing, a search will encounter this and return null even though the key is in the table.

One solution is through, <span style='color:#f7b731'>lazy deletion</span>, which is to set the value to some special tombstone value. Now <span style='color:#2d98da'>insert</span> should just <span style='color:#f7b731'>override</span> this tombstone if it encounters one.

**Uniform Hashing Assumption**
>For all $n!$ permutations for a probing sequence, each one is equally likely to be selected.

If the load ($\alpha$) is 1, meaning all the buckets are full (n/m where n = m), then it <span style='color:#eb3b5a'>cannot insert any more</span>.
#### Linear Probing

If there is a collision, <span style='color:#f7b731'>probe a sequence of buckets</span> until an empty bucket is found.

In general, the <span style='color:#2d98da'>hash</span> function will be, `h(k,i) = h(k,1) + i mod m`. where $i$ is the number of collisions encounter.

Now one issue with this is <span style='color:#eb3b5a'>clusters</span>, where if there is a collision, then the <span style='color:#f7b731'>size of the subsequent filled buckets will be increased</span>.

Once the table is about a <span style='color:#fa8231'>quarter full</span> there will be clusters of size $\theta(log n)$.
#### Double Hashing

Instead of 1 hashing function <span style='color:#f7b731'>use 2</span>. Now the hashing function will look like this `h(k,1) = f(k) + i * g(k) + mod m`. 

**Where :**
- `f(k)` and `g(k)` are the 2 hash functions
- $i$ is some constant
- $m$ is the number of buckets

For this to work `g(k)` and $m$ must be <span style='color:#f7b731'>relatively prime</span>, meaning they do **not share any common factors**.

**For example :** If $m = 2^{r}$ then choose a `g(k)` to be odd.

>[!question] How double hashing works?
>If the bucket is occupied then use the 2nd hashing function to determine the steps to take.
>
>Then we will use this step to find a empty slot.
<div style="break-after: page;"></div>

## Comparison Between Chaining & Open Addressing

In terms of <span style='color:#fa8231'>open addressing</span> :
- **Saves space** (Empty slots vs linked list)
- **Rarely need to allocate more memory** (No need to add to the length of the linked list)
- **Better cache performance** (Data all stored in once place, compared to linked list which can be everywhere in memory)

In terms of <span style='color:#fa8231'>chaining</span> :
- **Less sensitive to the choice of hash functions** (Clustering is not a problem)
- **Less sensitive to load**
- **Performance does not degrade badly** as $alpha$ reaches 1
## Table Size

What is a <span style='color:#fa8231'>good table size for the hash table</span>, well it depends. But there are ways to solve this and that is by <span style='color:#f7b731'>expanding the table size</span>.

**When expending the table**
1) Choose a new table size $m$
2) Choose a **new hash function** $h$ because the <span style='color:#f7b731'>old hash function does not handle</span> size $m$ table
3) For every item in the old table, **rehash and add into the new table**

Doing this can be expensive which takes around <b><span style='color: var(--mk-color-red)'>O(m<sub>1</sub> + m<sub>2</sub> + n)</span></b>, where $m_{1}$ is the **size of the old table** and $m_{2}$ is the **size of the new table** (Need time to make a new array or table).

To combat this, it is good to start resizing after a certain threshold lets say $m_{1} \lt n$, then expansion is just <b><span style='color: var(--mk-color-green)'>O(n)</span></b>.
### How Much to Grow By

Lets use the naive approach and just <span style='color:#fa8231'>increase the size by 1</span>, this is however <b><span style='color: var(--mk-color-red)'>O(n<sup>2</sup>)</span></b>. This is because at every iteration it will need <span style='color:#f7b731'>O(n) to increase the table and copy</span> and this will happen $n$ times.

What about <span style='color:#fa8231'>doubling</span>, then in this case the cost of resizing is <b><span style='color: var(--mk-color-green)'>O(n)</span></b> and insert is at amortised <b><span style='color: var(--mk-color-green)'>O(1)</span></b>, since majority of the time the table is not full and only at certain times it will resize.

**Amortized Cost**
> An operation has amortized cost $T(n)$ if for every integer $k$ the cost of $k$ operations is $\le kT(n)$

**Example :**
Amortized Cost of **O(7)**
1) Insert : O(5), $5 \le 7$
2) Insert : O(5), $5 + 5 \le 2 \times 7$
3) Insert : O(13), $5 + 5 +13 \le 3 \times 7$
4) Insert : O (7), $5 + 5 + 13 + 7 \le 4 \times 7$

The <b>order matters for amortized</b>, if the order is $13, 7 , 5, 5$, then the example above is <span style='color:#eb3b5a'>wrong</span>.

Then what about <span style='color:#fa8231'>squaring the size</span>, unfortunately it will be <b><span style='color: var(--mk-color-red)'>O(n<sup>2</sup>)</span></b> as resizing takes <b>O(m<sub>1</sub> + m<sub>2</sub> + n)</b> and $m_{1} = n$ and $m_{2} = n^{2}$.

### Shrinking

Now what if after some <span style='color:#2d98da'>deletions</span> the <span style='color:#f7b731'>table is barely utilised</span>, then it is time to <span style='color:#f7b731'>shrink the table size</span>. Lets try the same solution where if $n \lt m/4$ then <span style='color:#fa8231'>shrink the size of the table by half</span>.

The time complexity is the <span style='color:#f7b731'>same</span> as resizing the hash table by <span style='color:#f7b731'>doubling</span> it.
# Bloom Filter
---
## Fingerprint Hash Table

The idea of this is that through the <span style='color:#2d98da'>hash function</span>, whichever bucket the has function points to <span style='color:#f7b731'>set the value to 1</span>.

So what happens when a <span style='color:#fa8231'>collision occurs</span>, then it is <span style='color:#20bf6b'>alright</span> since the <span style='color:#f7b731'>value stored is just 1 or 0</span>. However this <span style='color:#eb3b5a'>causes false positives</span> because it is possible that an item even though was not inserted may point to a bucket with a 1 after hashing.

The <span style='color:#fa8231'>probability of a false positive</span> is at most :
$$
1 - \left(\frac{1}{e}\right)^{n/m}
$$
## Bloom Filters

So instead of 1 <span style='color:#2d98da'>hash function</span>, why not use 2? Thus in this case, when searching for an item, <span style='color:#f7b731'>both</span> the hash functions must <span style='color:#f7b731'>point</span> to buckets containing both <span style='color:#f7b731'>1 in order for an item to be considered inside</span>.

This makes <span style='color:#eb3b5a'>each item take up more space in the table</span>, however, the <span style='color:#fa8231'>probability of a false positive</span> will be <span style='color:#20bf6b'>significantly reduced</span>.
<div style="break-after: page;"></div>

$$
1 - e^{-kn/m}
$$
Where :
- $k$ is the number of hash functions
- $n$ is the number of items in the table (**Value 1**)
- $m$ is the size of the table

The **above is for 1 spot**, if it is for $k$ spots then :
$$
(1 - e^{-kn/m})^{k}
$$
With this the time complexity for all <span style='color:#2d98da'>insert</span>, <span style='color:#2d98da'>delete</span> and <span style='color:#2d98da'>query</span> are all <b><span style='color: var(--mk-color-green)'>O(k)</span></b>, where $k$ is the number of hash functions used. 

If a bitwise AND or OR is used for <span style='color:#2d98da'>intersection</span> and <span style='color:#2d98da'>union</span> of <span style='color:#f7b731'>2 sets</span> will take <b><span style='color: var(--mk-color-green)'>O(m)</span></b>.

<span style='color:#2d98da'>Intersection</span> is to find <span style='color:#f7b731'>similar items</span> in both sets and combine into 1, while <span style='color:#2d98da'>union</span> is to <span style='color:#f7b731'>join</span> 2 sets.