## 1. Disk Space Management

### 1.1 Appropriate Block Size
- Huge size (cost space)
  - cause fragmentation
  - waste disk space
- Small size (cost time)
  - multiple seeks
  - rotational delay 

### 1.2 Free Space Management
- Free list
- Bitmap

### 1.3 Security Control


## 2. File System Backups
- Incremental dump
   - dump only modified

- Logical dump
*starts at one or more specified directories and recursively dumps all files and directories found there that have changed since some given base date*
- Physical dump
*starts at block 0 of the disk, writes all the disk blocks onto the output tape in order*
  - Problem
    - dumping unused disk blocks
    - dumping bad blocks
  - Advantages
    - simple
    - fast 
  - Shortcomings
    - unable to skip selected directories     


## 3. File System Consistency
- Logical dump with Bitmap (indexed by Inodes)
  - Phase1: all modified files and all directories have been marked 
  - Phase 2：recursively walks the tree again, unmarking any directories that have no modified files or directories in them or under them.
  - Phase 3：scanning the i-nodes in numerical order and dumping all the directories that are marked for dumping. 
  - phase 4: Dump Files

- How to deal with inconsistency
  - $Unix$ 
    - fsck
  - $Windows$ 
    - scandisk

- File system states
  - consistent
  - inconsistent
    - missing block
    - duplicate free block
    - duplicate data block

- Inconsistency solution
  - two tables (to compare with each other) of file reference count
    - from directory pointers
    - from Inodes 


## 4. File System Performance
- Cache
  - Write-through Cache (Caches in which all modified blocks are written back to the disk immediately)
- Block read ahead
  - get blocks into the cache before they are needed to increase the hit rate 
- Reducing disk arm motion
  - clustering relative blocks
    - access
    - allocate  

## 5. Disk Defragmentation

