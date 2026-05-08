---
title: File Systems
Date Created: 2025-03-31
Last Updated: 2025-09-28
tags:
  - CS2106
  - Disk
---
# File System
---
<b><span style='color:var(--mk-color-red)'>Physical memory is volatile</span></b>, meaning that when the system turns off, everything in RAM will be removed.

Thus we want something that is <b><span style='color:var(--mk-color-green)'>persistent</span></b> and that is where we use external storage.

**Direct access** to storage media is <b><span style='color:var(--mk-color-red)'>not portable</span></b> (*depends on hardware specification & organisation*)

A <span style='color:var(--mk-color-orange)'>file system provides</span>:
- An **abstraction** on top of the physical media
- A **high level resource management** scheme
- **Protection** between processes and users
- **Sharing** between processes and users

<span style='color:var(--mk-color-orange)'>General criteria</span> for file systems:
1) **Self-contained**: Information stored on a media is enough to describe the entire organisation (*plug & play*)
2) **Persistent**: Beyond the lifetime of the OS and processes
3) **Efficient**: Provides good management of free and used space as well as minimum overhead for bookkeeping information

**Memory management vs File Management**
![[Memory Management vs File Management.png|center|400]]
## File System Abstractions

Firstly a **file** is a <b><span style='color:var(--mk-color-yellow)'>logical unit of information</span></b> created by a process. Essentially it is an <b><span style='color:var(--mk-color-yellow)'>abstract data type</span></b> with a set of common operations with various possible implementations.

It contains **data** which is <b><span style='color:var(--mk-color-yellow)'>information structured</span></b> in some ways but it also contains **metadata** (*file attributes*) which is <b><span style='color:var(--mk-color-yellow)'>information associated with the file</span></b>.
### File Metadata

![[File Metadata Examples.png|center]]

We **need metadata** so that we <b><span style='color:var(--mk-color-yellow)'>can access the file</span></b>.

> [!abstract] Operations on file metadata
> 1) **Rename**
> 	- Change filename (`touch`)
> 1) **Change attributes**
> 	- File access permissions
> 	- Dates
> 	- Ownership
> 	- etc.
> 3) **Read attribute**
> 	- Get file creation time
#### File Name

Different **file systems** have <b><span style='color:var(--mk-color-yellow)'>different naming rules</span></b> (*determine a valid file name*). This is for the file system to interpret the file.

Some common <span style='color:var(--mk-color-orange)'>naming rules</span>:
- Length of the file name
- Case sensitivity
- Weather special characters are allowed
- File extensions (`file_name.Extension`). **Some** file systems, the **extension is used to indicate the file type**
#### File Type

The OS supports a number of file types. **Each file type** has its <b><span style='color:var(--mk-color-yellow)'>own set of operations</span></b> and possibly a <b><span style='color:var(--mk-color-yellow)'>specific program for processing</span></b>.

<span style='color:var(--mk-color-orange)'>Common file types</span>:
- **Regular files**: contains user information
- **Directories**: system files for FS structure
- **Special files**: character/block oriented

> [!note] Major types of regular files
> 1) **ASCII files**: They are our text files, programming source codes etc. It can be <b><span style='color:var(--mk-color-yellow)'>displayed or printed as it is</span></b>.
> 
> 2) **Binary files**: They are executable java class files, pdf files, mp3/4, png / jpeg etc. There is a <b><span style='color:var(--mk-color-yellow)'>predefined internal structure</span></b> that can be <b><span style='color:var(--mk-color-yellow)'>proceeded by a specific program</span></b> (*PDF reader, JVM to execute java files*).

A file type can be <span style='color:var(--mk-color-orange)'>distinguished</span> by:
1) **Extension**: Used by Windows OS, the `XXX.Extension` determines the file type, <b><span style='color:var(--mk-color-yellow)'>changing the extension means changing the file type</span></b> (`XXX.docx` *is a word document*)
2) **Embedded information**: Used by Unix, is <b><span style='color:var(--mk-color-yellow)'>stored at the beginning of the file</span></b> which is commonly known as a <b><span style='color:var(--mk-color-turquoise)'>magic number</span></b>
#### File Protection

We <b><span style='color:var(--mk-color-yellow)'>need controlled access</span></b> (*what can we do to it*) to the information stored in a file.

<span style='color:var(--mk-color-orange)'>Type of access</span>:
- **Read**: Retrieve information from the file
- **Write**: Write/Rewrite the file
- **Execute**: Load file into memory and execute it
- **Append**: Add new information to the end of the file
- **Delete**: Remove the file from the FS
- **List**: Read metadata of a file
##### Implementing File Protection

The most basic way is to use <b><span style='color:var(--mk-color-yellow)'>role based protection</span></b>. We need to know what is the user who is it and then figure out what can they do to a file.

Most of these protection systems have an <b><span style='color:var(--mk-color-turquoise)'>access control list</span></b>.

> [!info] Access control list
> A list of user identity and the allowed access types. It is <b><span style='color:var(--mk-color-green)'>very customizable</span></b>, but there is <b><span style='color:var(--mk-color-red)'>too much information associated with file</span></b>.
> 
> In <b><span style='color:var(--mk-color-purple)'>Unix</span></b>, it can be:
> 1) **Minimal ACL**: Using permission bits
> 2) **Extended ACL**: Added named users and groups

We identify permissions by <b><span style='color:var(--mk-color-yellow)'>using bits</span></b>. We have <span style='color:var(--mk-color-orange)'>3 groups</span>:
1) **Owner**: The user who created the file
2) **Group**: Set of users who need similar access to a file
3) **Universe**: All other users in the system

Each of these groups will each have <b><span style='color:var(--mk-color-yellow)'>3 bits signifying what they can do</span></b>. The 3 bits are for **r**ead, **w**rite, e**x**ecute (*we can use `ls -l` or `getfacl file_name`to see this*).

> [!note] Sometimes there can be 1 more bit at the front which will show as `d` this just means its a directory
### File Data

**Generic file data operations**
![[Generic File Data Operations.png|center|500]]

These **file operations** are <b><span style='color:var(--mk-color-yellow)'>system calls provided by the OS</span></b>.

This provides protection, concurrent and efficient access as well as to maintain information.

> [!info] An OS cannot be used with any file system. It must be compatable

<span style='color:var(--mk-color-orange)'>Information kept for an opened file</span> (*in open file table*):
- **File Pointer**: Current location in file
- **Disk Location**: Actual file location on disk
- **Open Count**: How many process has this file opened? Useful to determine when to remove the entry in table

But how do we **store this information** the common approach will be to use <span style='color:var(--mk-color-orange)'>2 tables</span>:
1) **System-wide open-file table** (*OS open file table*): One entry <b><span style='color:var(--mk-color-yellow)'>per unique file</span></b>
2) **Per-process open-file table**: One entry <b><span style='color:var(--mk-color-yellow)'>per file used in the process</span></b>, where each entry points to the system-wide table

![[Example of How to Access a File.png|center|400]]

A **file descriptor table** is just an table or an array inside the processes PCB and is <b><span style='color:var(--mk-color-yellow)'>independent per process</span></b>. So each process if they open the same file will have <b><span style='color:var(--mk-color-yellow)'>2 different open file table entry</span></b>.

The **only time this is shared is when** we `fork()` the process.

In the <span style='color:var(--mk-color-orange)'>file descriptor</span>:
1) File descriptor 0 is for standard input
2) File descriptor 1 is for standard output
3) File descriptor 2 is for standard error
4) And many more but the first 3 is special

> [!question] Why do we need this?
> - Several processes can open the same file (*same file descriptor*)
> - Several different files can be opened at any time
> - What is a good way to organize the open-file information?
#### Structure

In general the **data** in a file is just an <b><span style='color:var(--mk-color-yellow)'>array of bytes</span></b> (*records*). Each byte has a unique <b><span style='color:var(--mk-color-yellow)'>offset</span></b> (*distance*) from the start of the file.

> [!info] Since it is an array we can do a O(1) look up

If the **records are fixed length** then we can <b><span style='color:var(--mk-color-green)'>easily access to any record</span></b> ($\text{size of record} \times (N - 1)$).

If the **records are of variable length**, it will be more <b><span style='color:var(--mk-color-green)'>flexible</span></b> but <b><span style='color:var(--mk-color-red)'>harder to locate</span></b>.
#### Access Methods

1) **Sequential access**
We **read data in order**, starting from the beginning. We <b><span style='color:var(--mk-color-yellow)'>cannot skip but can be rewound</span></b>.

2) **Random access**
Data can be <b><span style='color:var(--mk-color-yellow)'>read in any order</span></b> using <span style='color:var(--mk-color-orange)'>2 methods</span>:
- `Read( Offset )`: Every read operation explicitly states the position to be accessed
- `Seek( Offset )`: A special operation is provided to move to a new location in file

3) **Direct access** 
- Used for file containing <b><span style='color:var(--mk-color-yellow)'>fixed-length records</span></b>
- Allows <b><span style='color:var(--mk-color-yellow)'>random access to any record directly</span></b>
- Very useful where there is a large amount of records
- Basic random access method can be view as a special case. Where **each record is one byte**
# Directory
---
Directory ( *folder* ) is used to provide a logical grouping of files. But it also <b><span style='color:var(--mk-color-green)'>allows the system to keep track of files</span></b>.

There are many ways to <span style='color:var(--mk-color-orange)'>structure a directory</span>:
## Single-Level

![[Single-Level Directory Structure.png|center|300]]

> [!warning] This is a starting point, but we <b><span style='color:var(--mk-color-red)'>cannot have 2 files with the same name and type</span></b>
## Tree-Structure

![[Tree-Structure Directory Structure.png|center|300]]

Directories can be <b><span style='color:var(--mk-color-yellow)'>recursively embedded in other directories</span></b>, which forms a tree structure.

> [!success] Here 2 files can have the same name and type but in 2 different directories

We have <b><span style='color:var(--mk-color-orange)'>2 ways to refer to a file</span></b> in this scheme:
1) **Absolute pathname**
> Directory name followed from the <b><span style='color:var(--mk-color-yellow)'>root of the tree to the final file</span></b> (*it is the path from root to file*).

2) **Relative pathname**
> Directory names followed <b><span style='color:var(--mk-color-yellow)'>from the current working directory</span></b> (*CWD*). The **CWD can be set explicitly or implicitly and changed** (*example will be the* `cd` *command*).
## Directed Acyclic Graph

Or a [[Year 1/Sem 2/CS2040S - Data Structures and Algorithms/Graphs#Directed Acyclic Graph|DAG]].

![[DAG Directory Structure.png|center|300]]

In a DAG we can <b><span style='color:var(--mk-color-yellow)'>introduce shortcuts or links</span></b> this is known as <b><span style='color:var(--mk-color-turquoise)'>alias</span></b>. Thus it now does not follow the properties of a tree structure and it is more of a graph.

> [!success] With links files can be shared
> <b><span style='color:var(--mk-color-yellow)'>Only 1 copy of the actual document</span></b> but it can "appear" in multiple directories <b><span style='color:var(--mk-color-yellow)'>with different path names</span></b>.
### File Links

There are <span style='color:var(--mk-color-orange)'>2 types of links in unix</span>:
1) **Hard link**
Here the link will <b><span style='color:var(--mk-color-yellow)'>point to the actual file</span></b> inside disk. We can use the command `ln` to create a hard link.

> [!success] Advantages of hard link
> It has a <b><span style='color:var(--mk-color-green)'>low overhead</span></b>, only pointers are added in the directory.

> [!failure] Disadvantages of hard link
> There is a <b><span style='color:var(--mk-color-red)'>deletion problem</span></b>. Will the file get deleted if directory A deletes the file and another directory B has the same hard link, or what if the file is open and it gets deleted.

2) **Symbolic link** (*soft link*)
This link can be to <b><span style='color:var(--mk-color-yellow)'>a directory or a file but it will be in a special link file</span></b>. This file will contain the **path name** to the file.

We can use the command `ln - s` to create a symbolic link.

> [!success] Advantages of symbolic link
> It allows for <b><span style='color:var(--mk-color-green)'>simple deletion</span></b>, where if a directory deletes the special link file the file still remains and if the file is deleted then the link is broken.

> [!failure] Disadvantages of symbolic link
> It has a <b><span style='color:var(--mk-color-red)'>large overhead</span></b>. The special link file will take up actual disk space
## General Graph

Similar to the DAG, but now there can be <b><span style='color:var(--mk-color-red)'>cycles</span></b>, which can cause an infinite loop when traversing.

![[Graph Directory Structure.png|center|300]]

With a **symbolic link** as mentioned previously, it <b><span style='color:var(--mk-color-yellow)'>understands that there is a cycle</span></b> and not traverse (*sometimes the OS will not allow you to create cycles*).

There is a command `locate <file_name>`, it will **find all possible instances** of the file. But if there is a cycle, when will it know when to stop (*we need some additional information*).

> [!failure] General graphs are not desirable
> - **Hard to traverse** (*infinite looping*)
> - **Hard to determine when to remove a file/directory**
