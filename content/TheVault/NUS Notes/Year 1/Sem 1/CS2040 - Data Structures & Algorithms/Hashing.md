---
title: Hashing
Date Created: 2023-06-30
tags:
  - CS2040
  - Hashing
---
# Map ADT
---

It is an ADT which contains a collection of <b><mark class="hltr-cyan">Key, Value</mark></b> pairs.

Similar to python, there <span style='color:#eb3b5a'>cannot be duplicate keys</span>, and a key can only have a <span style='color:#f7b731'>one to one</span> or <span style='color:#f7b731'>many to one</span> relationships.

A <span style='color:#f7b731'>one to many</span> relationship is possible is through a key pointing to another map.

<span style='color:#2d98da'>Hashing</span> via the <span style='color:#2d98da'>hashing function</span> will create the Map ADT. This function uses the concept of an associative array where <span style='color:#2d98da'>some value is linked to an index in the array</span>.

## Direct Addressing Table

It is simply an array, where the numbers of the indexes acts as the key.

This provides a <span style='color:#f7b731'>one to one</span> relation with the key and the value.

### Restrictions

1. Keys must be a <span style='color:#eb3b5a'>non-negative integer values</span>
> As we are using the index of the array which is only an integer and it starts from 0

2. Range of keys must be small
> For a big range of keys will take up a lot of memory

3. Keys must be <span style='color:#eb3b5a'>dense</span> (Not many gaps int he key values)

# Hash Table
---

## Idea of a Hash Table

1. Map <span style='color:#0fb9b1'>large</span> integers to <span style='color:#20bf6b'>smaller</span> integers

There is a <mark class="hltr-red">hashing function</mark> (h), which will convert a integer to another smaller integer which will be an index in an array. Afterwards it will store the key value pair in that index.

2. Map <span style='color:#20bf6b'>non-integer</span> keys to <span style='color:#20bf6b'>integers</span>

## Hashing Function

With a hashing function it will output a integer associated with that large integer/key.

However, there is a possibility that 2 different key values can be associated with the same hash value. Therefore, the <b><mark style='background:#eb3b5a'>value in the array MUST store a key value pair</mark></b>.

This is what is known as a <span style='color:#eb3b5a'>collision</span> where two keys have the same has value. Therefore, `arr[h((key))]`, the method of retrieving does not work all the time.

### Characteristics of a Hash Function

1. <span style='color:#8854d0'>Fast</span> to compute
2. <span style='color:#8854d0'>Distribute keys evenly</span> throughout the has table, to prevent collisions
3. Needs <span style='color:#8854d0'>less space</span> (Slots)

### Types of Hash Functions

**Perfect Hash Function**

It results in a <span style='color:#f7b731'>one to one </span>relation between the keys and the has values.

However it is only possible if all keys are known beforehand.

Example: <span style='color:#8854d0'>GNU gperf</span>

**Minimal Perfect Hash Function**

Same as a perfect has function, however the table size is the <span style='color:#2d98da'>same</span> as the number of keywords supplied.

**Uniform Hash Function**

Distribute keys <span style='color:#2d98da'>evenly</span> in the hash table. However this will work better if the keys are <span style='color:#2d98da'>uniformly</span> distributed.

![[Uniform Hashing Function Example 1.png|center]]

The above hashing function only works if the key values are evenly distributed.

**How it works:**
	let k be (x-1), `floor(m(x-1)x)`
	(x-1)/m approximately give 0.9999..., when multiply by m and floored will give us m-1
	Thus, this function will <span style='color:#0fb9b1'>evenly map between 0 to m-1</span>.

**Modular Method**

If its not using the <span style='color:#2d98da'>modular function</span> in Java will evenly distribute the keys into a size M hash table, `key % m`.

**Multiplication Method**

![[Multiplication Hashing Function Example.png]]

Multiply the value <span style='color:#eb3b5a'>A</span> with a constant real number <span style='color:#2d98da'>between 0 to 1</span>

Afterwards extract the fractional part, afterward multiply <span style='color:#2d98da'>m, the size of the has table</span>

### Finding the Size of the Hash Table

#### Bad Practices

1. Using a number that is a power of 2

In the event of <span style='color:#fa8231'>keys all being even</span>, the even indexes of the has table will only be used, while the odd ones will not be used.

2. Using a value that has a lot of prime factors

This a rule of thumb pick a <b><mark class="hltr-yellow">prime number</mark></b> for m that is <b><mark class="hltr-yellow">not 2</mark></b>.

### Hashing of String Keys

The main concept is to convert the string into a integer. However <span style='color:#2d98da'>using the ASCII value </span>to sum up the characters is a <span style='color:#eb3b5a'>bad implementation</span>.

A better way of doing this is to "shift" the sum of each character thus the <span style='color:#0fb9b1'>position of the characters</span> will affect the has value.

Example:
```Java
import java.util.*;
public class Hashing {
	public static void main(String[] args){
		String key = "Hello"
		int hash_table_size = 23
		sum = 0
		for (int i = 0; i < key.length(); i++){
		// 31 is a good number to use
			sum = sum * 31 + key.charat(i);
		}
		int hash_value = sum % hash_table_size
	}
}
```

## Analyzing Performance of a Hash Table

Other than time complexity, the <span style='color:#3867d6'>load factor</span> is another attribute to determine the performance of the hash table. Which measures how <span style='color:#3867d6'>full</span> the hash table is.

**Formula: a = n / m**
a = Load Factor
n = Number of keys in the hash table
m = Size of the hash Table (Number of slots)

Therefor, alpha can be <mark class="hltr-red">bounded</mark> with a constant such that all hashing operations will be of <b><mark class="hltr-red">O(c)</mark></b> time on average.

Whenever the load factor exceeds the bound, the keys will <mark class="hltr-red">need to be rehashed in a bigger table</mark>. One way to choose a new size is to find the <span style='color:#f7b731'>next prime double</span> of the old hash table size.

# Collision Resolution
---

## Separate Chaining

### Concept

It uses a hash table, where each hash value will have a <span style='color:#f7b731'>link list of key value pairs</span>.

All our hashing operations, `insert`, `find` and `delete` will take <b><mark class="hltr-red">O(n)</mark></b> time.
> Note the reason for `insert` bring O(n) time and not O(1) is because we <span style='color:#f7b731'>need</span> to ensure that there is no entry with the same key value.

However, using a linked list is not <span style='color:#eb3b5a'>cache friendly</span>. Compared to an array, a linked is made of multiple objects at different places in memory, thus only that node will be in cache.

## Open Addressing

### Linear Probing

**Probing Sequence**

Formula for probing is `(hash(key) + n) % m`.

**Searching**

For linear probing, if the key referencing to the hash value does not match the key that it wants to find, it will iterate through each row in the has table until it finds the value or no.

**Insert**

Before any insertion into a hash table, call a `find` function and check if the key is already in the hash table. Insertion should be at the <span style='color:#eb3b5a'>first available slot</span>.

Once there is no duplicate keys, check if there is any <span style='color:#eb3b5a'>collision</span>, if there is, look for the next empty slot, by iterating through the hash table.

**Deletion**

Same as searching, however, the value cannot be removed as the <span style='color:#fa8231'>terminating condition is an empty slot</span>.

One way is to do <span style='color:#3867d6'>lazy deletion</span>, where the slot in the hash table will be assigned a state where is either:
- Occupied
- Occupied but deleted
- Empty

#### Issues with Linear Probing

**Primary Clustering**

The way linear probing inserts a key, it will cause <span style='color:#eb3b5a'>consecutive occupied slots</span>. It will cause later insertions to iterate more to the back of the hash table.

**Workarounds**

1. Modified Linear Probing

Using a modified probing sequence, `(hash(key) + 1 * d) % m`.

Where d is some constant integer where d > 1 and is <span style='color:#3867d6'>co-prime to m</span>. Being co-prime enables it to <span style='color:#3867d6'>cover all</span> slots in the has table.

2. Quadratic Probing

Instead of incrementing the probing value by 1, it can be squared to cover a larger distance, `(hash(key) + k ** 2) % m`.

However, if the <mark class="hltr-red">load factor is > 0.5</mark>, there is no guarantee that the probing function will terminate, as it will always probe occupied slots in the has table.

A workaround is to keep track of the load factor and double the hashing table and rehash when it exceeds.

However, this method will cause another problem called <span style='color:#eb3b5a'>secondary clustering</span>, where the same hash value will have the same probing sequence.

**Double Hashing**

It makes use of 2 different hashing functions to carry out its probe sequence, `(hash1(key) + 1 * hash2(key)) % m`.

The secondary hash function, determines the step size, if the first hash function hash value is occupied in the table.

The secondary has function, <mark class="hltr-red">must not evaluate to 0</mark>. Thus we can modify in this way, `5 - (key % 5)`, this removes the possibility of a 0.


