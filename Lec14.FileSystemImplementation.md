## 1. Overview
- MBR
  - boot PC
  - partition table
- Boot block
  - load OS
- Super block
  - data about file system
    - Inode location
    - Free block location
    - number of Free Inodes
- Inode
  - one per file
  - recording file attributes
- Free space management
  - Bitmap
  - Link list
- Root directory
  - root of the file system tree
         
## 2. Log-Structured File System
- Bottle neck -- write
  - write block from current position to  the end, then repeat from the beginning
    - reduce seeking time  

## 3. Journaling File System
The basic idea here is to keep a log of what the file system is going to do before it does it, so that if the system crashes before it can do its planned work, upon rebooting the system can look in the log to see what was going on at the time of the crash and finish the job.

## 4. Virtual File System
The key idea is to abstract out that part of the file system that is common to all file systems and put that code in a separate layer that calls the underlying concrete file systems to actually manage the data.