## 1. Paging
### 1.1 Introdution
If a program is too large to fit in the free space, what will happen? we need to do a little modification about the ***Swap*** in last ***Lec6***

### 1.2 Definition
- Each program has its own address space, which is broken up into chunks called ***pages***.
- Pages can be ***swapped in & out***
  
### 1.3 Memory Management Unit
- CPU ***sends virtual addresses to MMU***.
- MMU ***translates*** virtual addresses to physical addresses.
- MMU ***sends physical addresses*** to memory.

### 1.4 Translation
For example, a MMU has 16 4kb pages.
- Calculating ***offset***
    >4kB = 2^12 bit, then offset is a 12 bit address.
- Calculating ***index***
    >Check the corresponding page frame index to the virtual index in page table. That is the index.

The final physical address is [***index*** + ***offset***] 

## 2. Page Tables
### 2.1 Page Table Entry
- Extra space
  - store information
  - padding
  - left for future use
- Caching disabled
  - OS always expect to access user data as soon as possible and may access some inaccurate cache. Therefore, OS can disable this bit by setting it to 1.
- Referenced
  - Record if it's been ***referenced***. 
- Modified
  - Record if it's ***"dirty"*** and write it back to disk.
- Protection
  - Give privilege of ***Read***, ***Write*** and ***Execute***. 
- Present
  - Record if it exists in memory.
- Page frame number
  - Record corresponding page frame number.

## 3. Speeding up Paging
### 3.1 Translation Lookaside Buffer
***TLB*** is used as a page ***cache***. Due to ***spacial locality***, it turns out to be pretty good result.

## 4. Page Table for Large Memories
### 4.1 Reduce the Size of Page Table
- Multilevel Page Table
- Inverted Page Table