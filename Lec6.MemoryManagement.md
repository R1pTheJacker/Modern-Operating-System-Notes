## 1. No Memory Abstraction
- When multiple programs run, how to locate memory address?
  - Each Process have its own space, which address starts at 0.
  - Implementation: ***Static Relocation***

## 2. A memory Abstraction: Address Space
- When there's no large chunk of continues physical address space, what to do next?
  - ***Dynamic Relocation*** with ***Base*** Register and ***Limit*** Register

- What if there's no enough space for multiple running programs?
  - ***Swap***: Bring in each process in its entirety, run it for a while, then put it back on the disk.    

- How to deal with Externel Fragementation
  - Memory Compaction: Too slow!
  - Free Space Management

### 2.1 Free Space Management
- Bitmap
  - Each bit represents occupied or not.
- Free List
  - It consists of multiple free chunck of memory. Lists update when process terminated.
  - List Management
    - ***First Fit***: Choose the first hole
    - ***Next Fit***: 
        >It works the same way as *First Fit*, except that it keeps track of where it is whenever it finds a suitable hole. The next time it is called to find a hole, it starts searching the list from the place where it left off last time 
    - ***Best Fit***:
        >Best fit searches the entire list and takes the smallest hole that is suitable. For faster searching computer system holds a bunch of lists with different size and sort them, so there's no need to search all holes.