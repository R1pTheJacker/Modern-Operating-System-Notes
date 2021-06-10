## 1. Implementing Files
### 1.1 Physical Block Allocation
  - Continuous
    - raw! simple to implement
    - drawback occurs more frequently  
  - non-Continues

### 1.2 Physical Block Tracking
  - Link List
    - Implementation in table is a better option.
      - faster random access

    - FAT drawback
      - The entire table must stored in memory. 
  - Inode
    - This data structure includes file attributes and addresses of file blocks.
    - Each file has one Inode.
    - Multiple indexing is involved.
    - Superblock allocates Inode.


## 2. Implementing Directory
### 2.1 File Name & Attriibutes Storage
- Fix-sized entries
  - stored in directory entry
  - stored in Inode 
- flexible size
  - file entry inline
  - allocate in heap 

## 3. Link Files & Implementation

- Hard link
  - allocate new Inode
  - same Inode number with original file
  - recursive
  - not for directories
  - no crossing file-system
  - exist even when orignal file is deleted
  - access file in other directories & different names

- Symbolic link (Soft link)
  - cross different file-system
  - remove link, original file still exists
  - dead link if the original file is removed 
  - access one file with other references