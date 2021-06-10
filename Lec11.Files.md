## 1. File System Overview
Files & their operations

### 1.1 Why FS
- outside
  - find info
  - privilege control
...

- inside
  - free block management
...

## 2. Files

### 2.1 File Naming
It helps you or OS to indentify information you need.

### 2.2 File Types

- regular file
  - executable
    - in ELF format
    -  any file can be executed in Linux.
      - use chmod to modify permission  
  - archive
    - a file contains other files with their information
    - allow files to be restored to original form by extraction programs
    - easy to locate files  
- device file
  - block device
    - HDD 
    - SSD
  - character device
    - Mouse
    - Keyboard   
- directory file

### 2.2 File Access Methods
- sequential
- random


### 2.3 File Attributes
- protection
- password
- archive flag
- maximum size
...

### 2.4 File Operations
- syscall
  - create()
  - delete()
  - open()
  - close()
  - read()
  - write()
```C
int in_fd;
char buffer[BUF_SIZE];
...
in_fd = open(argv[1], O_RDONLY);
if(in_fd < 0) exit(2);
...
rd_count = read(in_fd, buffer, BUF_SIZE);
...
close(in_fd);
```
- manipulate attributes
  - append()
  - seek()
- rename 

### 2.5 File Structure
- byte sequence
- record sequence
- tree (Van Emde Boas)