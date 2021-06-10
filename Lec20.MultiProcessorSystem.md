## 1. Introdution
- Why we need it
  - CPU power and heat-sinking bottleneck
  - reliability 

- Typical hardware architecture of MP
  - shared memory model
  - message passing multiprocessor
  - wide area distributed system

- Typical problems
  - shared memory model
    - race for bus 
  - message passing multiprocessor
    - data location
    - interconnection network is expensive 
  - wide area distributed system
    - Internet is not reliable 

## 2. MultiProcessors
### 2.1 Hardware Model
- UMA
  - Uniform Memory Access
  - every memory word should be read as fast as every other memory word
- NUMA
  - on the contrary   

### 2.2 OS
#### 2.2.1 OS Types
- Each CPU Share the Same OS codes, but its 
own data structure, i.e, runs its own OS.
  - Can’t Borrow Resources, eg: one cpu run out of memory, it can’t borrow some from others.

- Master-Slave multiprocessors
  - Master CPU process all system calls
  - Master CPU is one bottleNeck

- Symmetric Multiprocessors
  - SMP multiprocessor model
  - Problem: Race Condition
    - divde OS code into independent critical region

#### 2.2.2 OS Synchronization
- TSL（Test and Set Lock） instruction can fail if bus already locked
  - Problem: put a massive load on the bus or memory, slowing down all other CPUs trying to do their normal work

- Problem: CPU that haven't acquire the lock no longer access lock variables in memory, but spinning on private lock in its cache.


#### 2.2.3 OS Scheduling
- Time-sharing
- Space-sharing





## 3. MultiComputers
### 3.1 Hardware Model
- Interconnection topologies
- Switching scheme

### 3.2 OS
- Distributed shared memory
  - possible implementation layer
  - hardware
  - OS
  - user-level software

- Load balancing
  - Graph-theoretic deterministic algorithm
  - minimize network traffic
    - tarjan: find min cut
    - min flow 


## 4. Other
### 4.1 Virtualization
- Type I
  - In reality, it is the operating system, since it is the only program running in kernel mode. Its job is to support multiple copies of the actual hardware, called virtual machines, similar to the processes a normal operating system supports.

- Type II
  - It is just a user program running on, say, Windows or Linux that "interprets" the machine's instruction set, which also creates a virtual machine. We put "interprets" in quotes because usually chunks of code are processed in a certain way and then cached and executed directly to improve performance, but in principle, full interpretation would work, albeit slowly.

### 4.2 Distributed Systems

- Key Issues: 
  - Interaction Pattern among Nodes
  - Document-Based Middleware
    - Internet
  - File-system-based Middleware
  - Object-Based Middleware
    - Corba

- Middleware
  - Middleware is software that lies between an operating system and the applications running on it. Essentially functioning as hidden translation layer, middleware enables communication and data management for distributed applications. It’s sometimes called plumbing, as it connects two applications together so data and databases can be easily passed between the “pipe.” Using middleware allows users to perform such requests as submitting forms on a web browser, or allowing the web server to return dynamic web pages based on a user’s profile.

  - Common middleware examples include database middleware, application server middleware, message-oriented middleware, web middleware, and transaction-processing monitors. Each program typically provides messaging services so that different applications can communicate using messaging frameworks like simple object access protocol (SOAP), web services, representational state transfer (REST), and JavaScript object notation (JSON). While all middleware performs communication functions, the type a company chooses to use will depend on what service is being used and what type of information needs to be communicated. This can include security authentication, transaction management, message queues, applications servers, web servers, and directories. Middleware can also be used for distributed processing with actions occurring in real time rather than sending data back and forth. 