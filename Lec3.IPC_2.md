## 1.Semaphore
This was the situation in 1965, when E. W. Dijkstra(1965) suggested using an integer variable to count the number of ***wakeups saved for future use***. In his proposal, a new variable type, which he called a semaphore, was introduced. A semaphore could have the value 0, indicating that no wakeups were saved, or some positive value if one or more wakeups were pending.

```C++
    #define N 100 /* number of slots in the buffer */
    typedef int semaphore; /* semaphores are a special kind of int */
    semaphore mutex = 1; /* controls access to critical region */
    semaphore empty = N; /* counts empty buffer slots */
    semaphore full = 0; /* counts full buffer slots */

    void producer(void) {
        int item;
        while (TRUE) { /* TRUE is the constant 1 */
            item = produce_item( ); /* generate something to put in buffer */
            down(&empty); /* decrement empty count */
            down(&mutex); /* enter critical region */
            insert_item(item); /* put new item in buffer */
            up(&mutex); /* leave critical region */
            up(&full); /* increment count of full slots */
        }
    }

    void consumer(void) {
        int item;
        while (TRUE) { /* infinite loop */
            down(&full); /* decrement full count */
            down(&mutex); /* enter critical region */
            item = remove_item( ); /* take item from buffer */
            up(&mutex); /* leave critical region */
            up(&empty); /* increment count of empty slots */
            consume_item(item); /* do something with the item */
        }
    }
```
## 2.Mutex
A ***Light-weight Binary Semaphore***, it only has to states ***0*** and ***1***.

### 2.1 Mutex Implementation
```C++
mutex_lock:
    TSL REGISTER, MUTEX
    CMP REGISTER, #0
    JZE ok
    CALL thread yieldthread
    JMP mutex lock
ok: RET

mutex_unlock:
    MOVE MUTEX, #0
    RET
```

### 2.2 Conditional Variables
- Avoid busy waiting
```C++
#include <stdio.h>
#include <pthread.h>
#define MAX 1000000

pthread_mutex_t the_mutex;
pthread_cond_t condc, condp;
int buffer = 0;

void *producer(void *ptr) {
    for(int i = 1; i <= MAX; i++) {
        pthread_mutex_lock(&the_mutex);
        while(buffer != 0) {
            pthread_cond_wait(&condp, &the_mutex);
            //if there is no condtional wait, the producer will be busy waiting till the buffer is empty
        }
        buffer = i;
        pthread_cond_signal(&condc);
        pthread_mutex_unlock(&the_mutex);
    }
    pthread_exit(0);
}
```

### 2.3 Mutex and Semaphore
A mutex is essentially the same thing as a binary semaphore and sometimes uses the same basic implementation. The differences between them are in how they are used. While a binary semaphore may be used as a mutex, a mutex is a more specific use-case, in that only the thread that locked the mutex is supposed to unlock it. This constraint makes it possible to implement some additional features in mutexes:

- Since ***only the thread that locked the mutex is supposed to unlock it***, a mutex may store the id of thread that locked it and verify the same thread unlocks it.
  - Semaphore are usually used to be a signal passing media. Though binary semaphore can do the same job as mutex, it doesn't require locker and unlocker to be the same process or thread.

- Mutexes may provide ***priority inversion*** safety. If the mutex knows who locked it and is supposed to unlock it, it is possible to promote the priority of that thread whenever a higher-priority task starts waiting on the mutex.

- Mutexes may also provide ***deletion safety***, where the thread holding the mutex cannot be accidentally deleted. Alternately, if the thread holding the mutex is deleted (perhaps due to an unrecoverable error), the mutex can be automatically released.

- A mutex may be ***recursive***: a thread is allowed to lock it multiple times without causing a deadlock.

## 3.Monitor
High-level abstraction to avoid deadlock problem.

### 3.1 Definition
 A monitor is a collection of procedures, variables, and data structures that are all grouped together in a special kind of module or package. Processes may call the procedures in a monitor whenever they want to, but they cannot directly access the monitor’s internal data structures from procedures declared outside the monitor.
- Only one process can be active in a monitor at any instant.
  
## 4.Message Passing
This method of interprocess communication uses two primitives, send and receive, which, like semaphores and unlike monitors, are system calls rather than language constructs. As such, they can easily be put into library procedures.

```C++
#define N 100 /* number of slots in the buffer */
void producer(void) {
    int item;
    message m; /* message buffer */
    while (TRUE) {
        item = produce_item( ); /* generate something to put in buffer */
        receive(consumer, &m); /* wait for an empty to arrive */
        build message(&m, item); /* constr uct a message to send */
        send(consumer, &m); /* send item to consumer */
    }
}

void consumer(void) {
    int item, i;
    message m;
    for (i = 0; i < N; i++) send(producer, &m); /* send N empties */
    while (TRUE) {
        receive(producer, &m); /* get message containing item */
        item = extract_item(&m); /* extract item from message */
        send(producer, &m); /* send back empty reply */
        consume item(item); /* do something with the item */
    }
}

```

## 5.Barriers
For ***groups of processes*** rather than two-process producer-consumer type situations, Some applications are divided into phases and have the rule that no process may proceed into the next phase until all processes are ready to proceed to the next phase. This behavior may be
achieved by placing a barrier at the end of each phase. When a process reaches the barrier, it is ***blocked until all processes have reached the barrier***. This allows groups of processes to synchronize.