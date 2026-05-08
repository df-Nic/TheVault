---
title: File System Implementations
Date Created: 2025-04-04
Last Updated: 2025-09-28
tags:
  - CS2106
  - Disk
---
# File System Layout
---
We know that files are stored on storage media (*hard disks, secondary storages*). However the **structure** of a disk in general is a <b><span style='color:var(--mk-color-yellow)'>1-D array of logical blocks</span></b>.

> [!info] Logical block
> It is the <b><span style='color:var(--mk-color-yellow)'>smallest accessible unit</span></b>. Usually **512-bytes to 4KB**.

These **logical blocks** will be <b><span style='color:var(--mk-color-yellow)'>mapped into disk sector(s)</span></b>. The layout of the disk sector is hardware dependent.

![[File System Layout Visualisation.png|center|500]]
# Hard Disk Organisation
---
A **logical blocks** is spilt into **multiple partitions** in these partitions it will contain:
1) **Master boot record** (*MBR*) at sector 0
2) From sectors 1 onwards it will store files and each sector/partition can have its own independent file system

> [!info] Master boot record
> It is a record to show how the partition looks like in the hard disk

**General disk organisation**
![[Generic Disk Structure.png|center]]
# File Implementation
---
A **file** is just a <b><span style='color:var(--mk-color-yellow)'>collection of logical blocks</span></b>. And similar to processes, if the **file size is not exactly the same as multiple logical blocks** then the last block may have [[Memory Management#Basics of Memory|internal fragmentation]].

A good file implementation we must:
- Keep track of the logical blocks
- Allow efficient access
- Disk space is utilised effectively
## Contiguous Block Allocation

Same concept as [[Memory Management#Contiguous Memory Allocation|contiguous memory management]], we <b><span style='color:var(--mk-color-yellow)'>allocate the files in consecutive disk blocks</span></b>.

![[Contiguous Block Allocation Example.png|center|500]]

The <b><span style='color:var(--mk-color-yellow)'>details of where the file is is stored</span></b> in a <b><span style='color:var(--mk-color-turquoise)'>file table</span></b>.

> [!success] Advantages of contiguous block allocation
> - **Simple to keep track**
> - **Fast access** (*we only need to find the first block*)

> [!fail] Disadvantages of contiguous block allocation
> - <b>[[Memory Management#Basics of Memory|External fragmentation]]</b> (*Might need to do defragmentation which is also costly*)
> - **File size needs to be specified in advance** (*if we don't have enough space during allocation we need to move the entire file which is very slow*)
## Linked List Block Allocation

Now we just store a **linked list of disk blocks**. Each block will contain:
- **The next disk block number** (*pointer*)
- **Actual file data**

For this we only need to <b><span style='color:var(--mk-color-yellow)'>store the first and last disk block number</span></b>.

![[Link List Block Allocation Example.png|center|500]]

> [!success] Advantages of contiguous block allocation
> - **Solves fragmentation problem** in contiguous allocation

> [!fail] Disadvantages of contiguous block allocation
> - **Random access in a file is very slow**
> - We **use part of the disk block** to store the pointer
> - **Less reliable** (*if one of the pointers is incorrect then issues will arise*)
## File Allocation Table

Similar to link list but we <b><span style='color:var(--mk-color-yellow)'>use a table</span></b> instead. This table is known as a <b><span style='color:var(--mk-color-turquoise)'>file allocation table</span></b> (*FAT*).

> [!important] This table will always be in memory

![[File Allocation Table Example.png|center|500]]

> [!success] Advantages of file allocation table
> - **Faster random access** (*linked list traversal takes place in memory now*)

> [!fail] Disadvantages of file allocation table
> - It **keeps track of all disk blocks** in a partition. It can be <b><span style='color:var(--mk-color-red)'>huge consuming valuable memory space</span></b>.
## Index Allocation

Each file will have an <b><span style='color:var(--mk-color-turquoise)'>index block</span></b>, which is just an <b><span style='color:var(--mk-color-yellow)'>array of disk block addresses</span></b>. Thus at index $N$ we will get the $N$-th block address.

![[Index Allocation Example.png|center|500]]

> [!success] Advantages of index allocation
> - **Lesser memory overhead** (*only the index block needs to be in memory*)
> - **Fast direct access**

> [!fail] Disadvantages of index allocation
> - Limited maximum file size (*Max blocks depends on the number of index block entries*).
> - **Index block overhead** (*We need to disk to store it*)
### Variations Of Index Allocation

If we want to store a larger file we can <b><span style='color:var(--mk-color-yellow)'>use the last part of the index block</span></b> to **point to another index block** (*linked list of index block*).

We can also do <b><span style='color:var(--mk-color-turquoise)'>multilevel indexing</span></b> where we have:
- **Direct blocks** which contains pointers which <b><span style='color:var(--mk-color-yellow)'>points to actual logical blocks</span></b>
- **Indirect blocks** which contains pointers that points to a <b><span style='color:var(--mk-color-yellow)'>logical block that contains a list of pointers</span></b>
# Free Space Management
---
We need to know which disk block is free. Thus we need to **maintain some information on which blocks are free**.

When we <span style='color:var(--mk-color-orange)'>allocate</span>:
- Remove free disk block from free space list
- We do this when when file is created or enlarged (*appended*)

When we <span style='color:var(--mk-color-orange)'>free up</span> space:
- Add free disk block to free space list
- We do this when file is deleted or truncated (*reduce in size*)
## Free Space Management Using a Bitmap

We can just use **1 bit** and a array to denote if a block is free or not. Usually if it is <b><span style='color:var(--mk-color-red)'>0 it is occupied</span></b>, if it is <b><span style='color:var(--mk-color-green)'>1 is it free</span></b>.

> [!success] Advantages of using a bitmap
> It provides a <b><span style='color:var(--mk-color-green)'>good set of manipulations</span></b>.
> 
> It is also <b><span style='color:var(--mk-color-green)'>memory efficient</span></b> 1 bit per block

> [!fail] Disadvantages of using a bitmap
> We need to <b><span style='color:var(--mk-color-red)'>keep it in memory</span></b> for efficiency reasons.
## Free Space Management Using a Linear List

Similar concept we just have a linked list of all the free disk blocks. Each block will have a <b><span style='color:var(--mk-color-yellow)'>pointer to the next available block</span></b>.

> [!success] Advantages of using a linked list
> - **Easy to locate free block**
> - Only the **first pointer needs to be in memory** (*other blocks can be caches for efficiency*)

> [!fail] Disadvantages of using a linked list
> - **High overhead**
# Implementing Directories
---
The directory has <span style='color:var(--mk-color-orange)'>2 main tasks</span>:
1) Keep track of all the files in the directory (*possibly with the file metadata*)
2) Map the file name to the file information

Before we use a file we need to open it like `open(file_name)`. The purpose is to locate the file information using the provided pathname + file name.

Lets say we have a file path of `/dir2/dir3/data.txt`, we will <b><span style='color:var(--mk-color-yellow)'>recursively traverse down until the file is found</span></b>.

When there is a `/` it contains <b><span style='color:var(--mk-color-turquoise)'>sub-directory</span></b> is usually stored as <b><span style='color:var(--mk-color-yellow)'>file entry with special type in a directory</span></b>.

We will need to <span style='color:var(--mk-color-orange)'>store</span> the:
- File name (*minimum*), it will be unique per directory
- Possibly other metadata
- File information or pointer to this information

We can store everything or just the file name and a pointer to a data structure for other information.
## Directories Using a Linear List

A directory can be **composed of a list**, <b><span style='color:var(--mk-color-yellow)'>each entry will represent a file</span></b>.

Since it is a list we will need a **linear search** which will be <b><span style='color:var(--mk-color-red)'>inefficient</span></b> for larger directories or deep tree traversal.

A **solution** will be to <b><span style='color:var(--mk-color-green)'>cache the last few searches</span></b>.
## Directories Using a Hash Table

Now a directory can have a **hash table** of size $N$. Every <b><span style='color:var(--mk-color-yellow)'>file name will be hashed</span></b> into some bucket in the hash table.

But now we need to handle <b><span style='color:var(--mk-color-red)'>collisions</span></b> which is usually resolved by <b><span style='color:var(--mk-color-green)'>using seperate chaining</span></b>.

> [!success] Advantages of using a linked list
> - **Fast lookup**

> [!fail] Disadvantages of using a linked list
> - **Hash table has a limited size**
> - **Depends on the hashing function used**
# File System in Action
---
Now we will combine everything together. At run time when a user interacts with a file, **run-time information** is needed and is maintained by the OS.
## Creating a File

We want to make a file at `../../parent/File`, then we will:
1) Use the <b><span style='color:var(--mk-color-yellow)'>full pathname to locate</span></b> the `parent` directory
2) **Search** the filename `F` to <b><span style='color:var(--mk-color-yellow)'>avoid duplicates</span></b> (*terminate if there is a duplicate*), this search can be on cached directory structure
3) Now we need to <b><span style='color:var(--mk-color-yellow)'>find free space</span></b> in our free space list (*depending on allocation scheme and implementation*)
4) <b><span style='color:var(--mk-color-yellow)'>Add the new file into</span></b> the `parent` directory (*list or hash table*) with the relevant file information

![[Creating a File Visualisation.png|center|500]]
## Opening a File

Lets say we want to open file `F`:
1) <b><span style='color:var(--mk-color-yellow)'>Check if the file is open</span></b> using the <b><span style='color:var(--mk-color-turquoise)'>system-wide file table</span></b> for an existing entry `E`
	1) If found create an entry in P's table to point to `E`
	2) Return the pointer to this entry
2) If we <b><span style='color:var(--mk-color-red)'>cannot find it</span></b> then use the <b><span style='color:var(--mk-color-yellow)'>full pathname to locate</span></b> `F` (*cannot find then terminate with an error*)
	1) Once located the file information is loaded into a new entry `E` in the system-wide file table
	2) It creates an entry in P's table to point to `E`
	3) Return the pointer to this entry

This **pointer** is used for further <b><span style='color:var(--mk-color-yellow)'>read/write operations</span></b>.

![[Opening a File Visualisation.png|center|500]]