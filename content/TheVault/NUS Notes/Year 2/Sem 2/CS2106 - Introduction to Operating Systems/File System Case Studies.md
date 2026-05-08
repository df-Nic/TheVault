---
title: File System Case Studies
Date Created: 2025-04-11
Last Updated: 2025-09-28
tags:
  - CS2106
  - Disk
---
# Microsoft FAT File System
---
Used in the MS-DOS in the 1980s and was the default file system until Windows XP in 2001.

There were several versions, FAT12 $\rightarrow$ FAT16 $\rightarrow$ FAT32.

The FAT32 is popular as it is:
- Supported across all major OSes
- Used in portable drives, gaming consoles, digital cameras etc

**FAT file system layout**:
![[FAT File System Layout.png|center]]

> [!info] When a computer ask to format a disk, it is actually to format it to be understandable a structure like the FAT layout.
## File Allocation Table

This is what [[File System Implementations#File Allocation Table|FAT]] means for this file system. here file <b><span style='color:var(--mk-color-yellow)'>data is allocated to a number of data blocks</span></b> or data block clusters (*bunch of data blocks*) and it <b><span style='color:var(--mk-color-yellow)'>kept as a linked list</span></b>.

All the **pointers** to the data blocks are **kept** separately in the <b><span style='color:var(--mk-color-turquoise)'>file allocation table</span></b>. **One entry** in this table is for <b><span style='color:var(--mk-color-yellow)'>a data block / cluster</span></b>

> [!note] The OS will cache the table in RAM to facilitate linked list traversal

A <span style='color:var(--mk-color-orange)'>FAT entry contains</span> either:
- <b><span style='color:var(--mk-color-green)'>FREE</span></b> code (*the block is available / empty*)
- <b><span style='color:var(--mk-color-teal)'>Block number</span></b> (*pointer to the next file/block*)
- End of file code or <b><span style='color:var(--mk-color-purple)'>EOF</span></b> (*here we will not use -1*)
- <b><span style='color:var(--mk-color-red)'>BAD</span></b> code (*the block is unusable*)

> [!danger] If our disk is large, our table will also be larger as a result
## Directory Structure & File Information

For **directories** (*folders*) are represented as <b><span style='color:var(--mk-color-yellow)'>special type of file stored in a data block</span></b> unlike the root directory which is stored in a special location on disk.

Then for each **file / subdirectory** within the folder is **represented** as a <b><span style='color:var(--mk-color-turquoise)'>directory entry</span></b> inside this data block, where it traditionally uses a **8-3 naming scheme**.

![[Directory Entry Visualisation.png|center]]

> [!info] Additional information about the directory entry fields
> - The **first byte of the file name** may be used for some special characters. It can be deleted, end of directory entries, parent directory etc.
> - The file creation **date is limited to 1980 to 2107**
> - The file creation **time accuracy is plus minus 2 seconds**
> - Depending on the FAT variant the bits differ for the first disk block (*FAT12, 12 bits, FAT16, 16 bits FAT32, 32 bits*)

We only need the first disk block because in a linked list implementation we can traverse all the disk blocks.

> [!summary] Putting it all together
> 1) Read the **first disk block** stored in the directory entry
> 2) **Access the disk block in FAT** in memory to find out **subsequent disk blocks** (*EOF to terminate*)
> 3) We can use the **disk block number to perform actual disk access** on the data blocks
### Long File Names

For long files names a work around is to <b><span style='color:var(--mk-color-yellow)'>use multiple directory entries</span></b> (*a chain of entries*). We will keep the 8+3 short version for backward compatibility.

Another way is to use a <b><span style='color:var(--mk-color-turquoise)'>virtual FAT</span></b> (*VFAT*). Which supports long filenames up to 255 characters.
## Variants of FAT

As mentioned we have FAT12, FAT16, FAT32 and so on. This is to <b><span style='color:var(--mk-color-yellow)'>support larger hard disk as a single partition</span></b>.

<span style='color:var(--mk-color-orange)'>2 major themes</span> to support larger hard disks:
1) **Disk clusters**
> Instead of using a single disk block as the smallest allocation unit, <b><span style='color:var(--mk-color-yellow)'>use a number of contiguous disk blocks</span></b>.

2) **FAT size**
> A bigger FAT, more disk blocks/clusters which means <b><span style='color:var(--mk-color-yellow)'>more bits to represent each disk block/cluster</span></b>.

Generally we will **use a combination of the 2** to determine the largest usable partition.

|                            FAT12                             |                             FAT16                             |                                                FAT32                                                 |
| :----------------------------------------------------------: | :-----------------------------------------------------------: | :--------------------------------------------------------------------------------------------------: |
| $2^{12} \times 2^{14} = 2^{26}$ clusters<br><br>Or **16MiB** | $2^{16} \times 2^{14} = 2^{30}$ clusters<br><br>Or **256MiB** | $2^{28} \times 2^{14} = 2^{42}$  clusters<br>(*4 bits are used for other things*)<br><br>Or **1TiB** |
> <b><span style='color:var(--mk-color-charcoal)'>Assuming a cluster is 4KiB</span></b>.

The <b><span style='color:var(--mk-color-red)'>actual size is a little lesser</span></b> because of the special values (*EOF, FREE, etc*) which reduces the total number of valid data block/clusters.

> [!success] The larger the cluster size the larger the usable partition

> [!failure] The larger the cluster size the larger the internal fragmentation
# Extended-2 File System
---
Also known as <b><span style='color:var(--mk-color-turquoise)'>Ext2</span></b>, which is popular among Linux systems. 

![[Ext2 File System Layout.png|center]]

> [!important] The information contained is only for that block group with the exception of the super block

1) **Superblock**
> It contains <b><span style='color:var(--mk-color-yellow)'>information about the whole file system</span></b> (*total I-nodes number, I-Nodes per group, total disk blocks, disk blocks per group, etc*). It is **duplicated** in each block group for redundancy.

2) **Group descriptors**
> <b><span style='color:var(--mk-color-yellow)'>Describes each of the block groups</span></b> or information about itself (*Number of free disk blocks, free I-nodes, location of bitmaps etc*). May be **duplicated** in each block group as well.

3) **Block bitmap**
> [[File System Implementations#Free Space Management Using a Bitmap|It]] keeps track of the <b><span style='color:var(--mk-color-yellow)'>usage status of the blocks of this group</span></b> (*1 occupied, 0 is free*).

4) **I-node bitmap**
> It keeps track of the <b><span style='color:var(--mk-color-yellow)'>usage status of the i-nodes of this group</span></b> (*1 occupied, 0 is free*).

5) **I-node table**
> An <b><span style='color:var(--mk-color-yellow)'>array of I-nodes</span></b>, each entry can be access by an unique index (*only contains I-nodes in this block group*). This stores file data (*metadata*).
## I-Node Structure

All I-nodes in each of the block group is of the <b><span style='color:var(--mk-color-yellow)'>same size of 128 bytes</span></b>. An index will <b><span style='color:var(--mk-color-yellow)'>contain file metadata and the pointer to the data blocks</span></b>.

> [!success] It does not matter how big the file is, the pointer size is fixed. So it can point to any file size.
### I-Node Data Block Pointers

![[I-Node Data Block Pointers Visualisation.png|center]]

An I-Node **contains 15 disk block pointers**
- The **first 12 pointers** (*direct pointers*) points to disk blocks known as <b><span style='color:var(--mk-color-turquoise)'>direct blocks</span></b>
- The **13th pointer** points to a disk block that stores direct pointers known as <b><span style='color:var(--mk-color-turquoise)'>single indirect block</span></b>
- The **14th pointer** points to a disk block containing a number of single indirect blocks known as <b><span style='color:var(--mk-color-turquoise)'>double indirect block</span></b>
- The **15th pointer** points to a disk block containing a number of double indirect blocks known as <b><span style='color:var(--mk-color-turquoise)'>triple indirect block</span></b>

> [!question] Why is it design like this?
> It allow <b><span style='color:var(--mk-color-green)'>fast accesses to small files</span></b>, and also have the <b><span style='color:var(--mk-color-green)'>flexibility in handling huge files</span></b>.
## Directory Structure

The data blocks of a <b><span style='color:var(--mk-color-yellow)'>directory stores a linked list of directory entries</span></b> for each file/subdirectories information within this directory.

Each <span style='color:var(--mk-color-orange)'>directory entry will contain</span>:
- I-Node number for that file / subdirectory
- Size of this directory entry (*locating the next directory entry*)
- Length of the file / subdirectory name
- Type of file or subdirectory (*other special file type is possible*)
- File / subdirectory name (*up to 255 characters*)

![[Directory Structure.png|center]]

> If it points to **0 then it is an empty block**
### Searching for a File

![[Searching a File in Ext2 File System.png|center]]

> [!info] As an OS it might want to cache the I-Node for `" / "` or `" sub / "` because of locality
### For Deletion

Before we can delete we <b><span style='color:var(--mk-color-yellow)'>need to check the status</span></b> of the file (*other process opening the file, links to the file*).

Then when we delete we need to <b><span style='color:var(--mk-color-yellow)'>update the information within the block group</span></b>:
- Data blocks
- I-node table
- I-node bitmap
- Block bitmap
- Directories needs to be updated
## Links with I-Nodes

### Hard Links

![[Hard Links with I-Nodes.png|center]]

The <b><span style='color:var(--mk-color-turquoise)'>reference count</span></b> will contain **how many directories are pointing to this I-node** (*multiple references to a I-node*).

> [!success] Deleting a hard link, will cause the file to still exist because other directories are pointing to it

> [!failure] If we delete a file it might still be there but we think it is gone
### Symbolic Link

![[Symbolic Links with I-Nodes.png|center]]

Here only the <b><span style='color:var(--mk-color-yellow)'>pathname is stored</span></b> in the data block. So it makes a new "file" which points to the directory.

> [!failure] If we delete the file or change the file name, the pointer will point to nowhere

> [!failure] We need to do a extra lookup just to go to the actual file in disk

