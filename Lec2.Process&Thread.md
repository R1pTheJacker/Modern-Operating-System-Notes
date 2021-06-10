## 1.Process
### 1.1 Definition
 An abstraction of a running program

### 1.2 Internal Structure
#### 1.2.1 User Space
- Stack Segment
  >The process Stack contains the temporary data such as method/function parameters, return address and local variables.

- Heap Segment
  >This is dynamically allocated memory to a process during its run time.

- Text Segment
  >This includes the current activity represented by the value of Program Counter and the contents of the processor's registers.

- Data Segment 
  >This section contains the global and static variables.

#### 1.2.2 Kernel Space
- Usually, it contains kernel code.

#### 1.2.3 Process Control Block
A Process Control Block is a data structure maintained by the Operating System for every process. The PCB is identified by an integer process ID (PID). A PCB keeps all the information needed to keep track of a process as below.

- Process State
  >Whether it's ready, running or waiting.

- Process Privileges
  >Whether it's allowed to access some resources.

- Process ID & Parent Process ID
  >Unique identification for each of the process and its parent.

- Program Counter
  >A pointer to the address of next instruction.

- CPU registers
  >Various CPU registers.

- Scheduling Information
  >Process priority etc.

- Memory management
  >Pointers to page table, memory limits and segement table etc.

- IO Information
  >List of IO devices allocated by current process.

### 1.3 Process Model
#### 1.3.1 States
- ***Blocked(waiting)***
- ***Running***
- ***Ready***

#### 1.3.2 Process Initialization
- System initialization.
- System call by a running process.
- User request.
- Initiation of a batch job.

#### 1.3.3 Process Implementation
- System Calls
  * ***fork()***
  * ***exec()***
  
#### 1.3.4 Process Termination
- Voluntary
  * Normal exit
    >Calling syscall exit().
  * Error exit
    >Infinite recursion of arithmetic error like choosing 0 as divisor.
    
- Involuntary
  * Fatal error
    >Accessing kernel code.
  * Killed by another process
    >Child Process will be killed if its parent is killed.


## 2.Thread
### 2.1 Definition
The mini and lightweight version of process.

#### 2.1.1 Why Thread
- Faster IPC
  >Sharing a part of memory. For processes, they need other slower IPC methods.
- Faster Creation & Less Space
  >Shared library, shared heap and same text.

### 2.2 Internal Struture
Thread has a program counter for instructions, some registers for holding variables and address, and a stack for assembly *CALL* and *RET* procedure.
>In other words, Thread are the entities scheduled for execution on the CPU

### 2.3 Thread Model
One process consists of one or more threads, they use shared resources and cooperate, everything else are pretty much a process.

### 2.4 Thread Implementation
#### 2.4.1 General Implementation
- User Thread
  >Thread is implemented in user space, kernel doesn't recognize threads. Generally, process controls its threads using ***Thread Table*** and ***TCB***
- Kernel Thread
  >Thread is implemented in kernel space. kernel can only see a bunch of threads and doesn't know what processes they belong to.
- Hybrid

#### 2.4.2 In Reality
- POSIX Thread
  >To make it possible to write portable threaded programs, *IEEE* has defined a standard for threads in IEEE standard 1003.1c. The threads package it defines is called ***Pthreads***. Most UNIX systems support it. 
- Pop-up Thread
  >the arrival of a message causes the system to create a new thread to handle the message. Such a thread is called a pop-up thread.


