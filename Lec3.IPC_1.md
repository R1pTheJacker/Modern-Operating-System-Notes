### 1.Race Condition
Where two or more processes are reading or writing some shared data and the final result depends on who runs precisely when, are called race conditions.

### 2.Critical Region
The part of the program where the shared memory is accessed is called the critical region.

- How to avoid race condition?

- Good Solution Predefinition
  * No two processes may be simultaneously inside their critical regions.
  * No assumptions may be made about speeds or the number of CPUs.
  * No process running outside its critical region may block any process.
  * No process should have to wait forever to enter its critical region.
  
### 3.Mutual Exclusion with Busy Waiting
#### 3.1 Disabling Interrupts
On a single-processor system, the simplest solution is to have each process disable all interrupts just after entering its critical region and re-enable them just before leaving it. With interrupts disabled, no clock interrupts can occur. ***MIT XV6*** adopted this approach for a compact kernel.

#### 3.2 Lock Variables
- Strict Alternation
  ```C++
    while(true) {
        while(turn != 0);
        critical_region();
        turn = 1;
        noncritical_region();
    }

    while(true) {
        while(turn != 1);
        critical_region();
        turn = 0;
        noncritical_region();
    }
  ```

- Peterson's Solution
  ```C++
  #define N 2

  int turn;
  int interested[N];

  void enter(int process) {
      int other;

      other = 1 - process;
      interested[process] = true;
      turn = process;

      while(turn == process && interested[other] == true);
  }

    void leave(int process) {
        interested[process] = false;
  }
  ```
- TSL Instruction
  To acquire atomicity, we use ***TSL*** or ***XCHG*** statement. First acquire the lock, then check if it's locked already.
  * GNU Assembly
    ```C++
    enter_region:
        TSL REG, LOCK
        CMP REG, 0
        JNE enter_region
        RET
    
    leave_region:
        MOV LOCK, 0
        RET
  
    ```
  * 8086 Assembly
    ```C++
    enter_region:
        MOV REG, 1
        XCHG REG, LOCK
        CMP REG, 0
        JNE enter_region
        RET

    leave_region:
        MOV LOCK, 0
        RET
    ```
    
### 4.Sleep & Wakeup
#### 4.1 Problems of busy waiting
- wasting CPU time
- causing priority inversion
