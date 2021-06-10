## 1. Time for Paging
- When Paging subsystem begins to work?
  - Process creation
    - determine program size
    - create page table
  - Process execution
    - MMU reset for new process
    - TLB flushed
  - Page fault time
    - determine virtual address causing fault
    - swap target page out, needed page in
  - Process termination time
    - release page table, pages
## 2. Page Fault Handling
- Hardware traps to kernel
- General registers saved
- OS determines which virtual page needed
  - Often one of the hardware registers contains this information. If not, the operating system must retrieve the program counter, fetch the instruction, and parse it in software to figure out what it was doing when the fault hit. 
- OS checks validity of address, seeks page frame
- If selected frame is dirty, write it to disk
- OS brings schedules new page in from disk
- Page tables updated
- Faulting instruction backed up to when it 
began
  - Saving the instruction caused page fault is ***Intruction Backup***.
- Faulting process scheduled
- Registers restored
- Program continues

## 3. Paging with I/O
- Locking Pages in Memory
  - Virtual memory and I/O occasionally interact
  - Proc issues call for read from device into buffer
    - while waiting for I/O, another processes starts up
    - has a page fault
    - buffer for the first proc may be chosen to be paged out
  - Need to specify some pages locked
    - exempted from being target pages
## 4. Separation of Policy and Mechanism
- Advantage 
  - This implementation is more modular and with greater flexibility. 
- Disadvantage 
  - The extra overhead of crossing the user-kernel boundary several times and the overhead of the various messages being sent between the pieces of the system. 
## 5. Segmentation
### 5.1 Segmentation with Paging
- Caluting VA for Segmentation
  - VA = Segment Register + Offset
    - Usually ***DS*** and ***SS*** with ***EDX*** and ***ESP***