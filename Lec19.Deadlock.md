## 1. Deadlock Concepts
- Key factors
  - race for resource
  - non-preemptable resource

- Four Conditions
  - Mutual exclusion condition
    - Each resource is either currently assigned to exactly one process 
  or is available.
  - Hold and wait condition
    - process holding resources can request additional
  - No preemption condition
    - previously granted resources cannot forcibly taken away
  - Circular wait condition
    - must be a circular chain of 2 or more processes
      - each is waiting for resource held by next member of the chain


## 2. Deadlock Nature
- Deadlock modeling
  - directed graphs
    - deadlock may happen if cycle occurs  


## 3. Handle Deadlock
### 3.1 The ostrich algorithm
  - pretend there is no problem
  - deadlock occur rarely
  - cost of prevention is high

  - Unix and Windows take this approach

### 3.2 Deadlock Detection & Recovery
#### 3.2.1 Detection
- Detection with One Resource of Each Type
  - find cycles of the graph 

- Deadlock Detection with Multiple Resource of Each Type
  - Allocation Matrix
  - Request Matrix
  - means
    - Look for an unmarked process, Pi, for which the i-th row of R is less than or equal to A.
    - If such a process is found, add the i-th row of C to A, mark the process, and go back to step 1. 
    - If no such process exists, the algorithm terminates. When the algorithm finishes, all the unmarked processes, if any, are deadlocked 

#### 3.2.2 Recovery
- Recovery through preemption
  - take a resource from some other process
  - depends on nature of the resource

- Recovery through rollback
  - checkpoint a process periodically
  - use this saved state 
  - restart the process if it is found deadlocked

- Recovery through killing processes
  - crudest but simplest way to break a deadlock
  - kill one of the processes in the deadlock cycle
  - the other processes get its resources 
  - choose process that can be rerun from the beginning

### 3.3 Avoidance
- Draw resource request trajectory
  - processes must not enter critical region simultaneously

- Safe & Unsafe states
  - A state is said to be safe if it is not deadlocked and there is some scheduling order in which every process can run to completion even if all of them suddenly request their maximum number of resources immediately.

- The banker's algorithm
  - The banker’s algorithm considers each request as it occurs, and see if granting it leads to a safe state. If it does, the request is granted; otherwise, it is postponed until later. 
  - To see if a state is safe, the banker checks to see if he has enough resources to satisfy some customer. If so, those loans are assumed to be repaid, and the customer now closest to the limit is checked, and so on. 
  - If all loans can eventually be repaid, the state is safe and the initial request can be granted.


### 3.3 Prevention
Attack four deadlock condition.

|Condition      | Approach      |
| :-----        | :-----        |
|Mutual Exclusion |Spooling everything  |
|Hold and Wait | Request all resources initially |
|No preemption | Take resources away             |
|Circular wait | Order resources numerically     |



## 4. Other Issues
### 4.1 Two-phase Lock

- ***Phase I***
  - process tries to lock all records it needs, one at a time
  - if needed record found locked, start over (no real work done in phase one)
- ***Phase II***
  - If phase one succeeds, it starts second phase, 
  - performing updates
  - releasing locks

### 4.2 Non-resource Deadlock

- possible for twp processes
  - each of them is waiting for the other to do some task
- possible for semaphores
  - multiple down() or up() in wrong order

### 4.3 Livelock
- all processes are leaving resource to each other

### 4.4 Starvation
- it works great for multiple short jobs condition
- shortest job first may postpone long jobs forever

Solution:
1. First come, first serve policy.
