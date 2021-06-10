## 1. Page Fault Reducing: Time Optimizaion
- Local Replacement
- Global Replacement
- Race Condition
  - Reduce number of processes competing for memory.
  - swap one or more to disk, divide up pages they held.
- Clean Policy
  - Write back to disk in time.

## 2. Page size Optimization: Space Optimization
- Small page size
  - Advantages
    - less internal fragmentation 
    - better fit for various data structures, code sections
    - less unused program in memory
  - Disadvantages
    - programs need many pages, larger page tables
- Increase Address Space
  - Separate Instruction and Data Spaces.
- Save Memory
  - fork(): copy on write.
  - Another famous techniques: shared library

 
## 3. Memory Mapped Files: Application Optimization
- Memory mapped-files
  - Saving space
    - No need to create two buffer for each process.
  - Saving time
    - If syscalls are constantly used, we better adopt mmap files because in & out kernel is slow.
    >Two Processes map one file into memory. Each of them could directly read write file without calling read & write syscall, but using pointer to directly access memory.