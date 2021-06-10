## 1.Scheduling Introduction
Scheduling is to solve the problem that when multiple processes/threads are ready, which one should be put on the CPU.
### 1.1 When to Schedule
- process creation
- process exit
- process blocks on IO
- IO interrupt

### 1.2 How to Schedule
- Scheduling Algorithm
- Category
  - Preemptive ***VS*** Non-Preemptive
  - Batch
  - Interactive
  - Real-time

## 2.Scheduling in Batch Systems
- Throughput
  >The number of processes that complete their execution per time unit.
- Turnaround time
  >The interval from submission to completion.
- Waiting time
  >The amount of time for a process waiting in the ready queue.
- Response time
  >The amount of time it takes from a request to the first response.

## 3.Scheduling in Real-time Systems
- Shortest Job First
- Average Turnaround
- Priority Scheduling
- Multiple Queue
  - Each queue can choose its scheduling algorithm differently. 