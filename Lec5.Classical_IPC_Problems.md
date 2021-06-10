## 1.Dining Philosophers
- Problem
  - Philosophers eat or think.
  - Eating requires 2 forks
  - Pick only one fork at one time

- Solution
```C++
#define N 5 /* number of philosophers */
#define LEFT (i + N − 1) % N /* number of i’s left neighbor */
#define RIGHT (i + 1) % N /* number of i’s right neighbor */
#define THINKING 0 /* philosopher is thinking */
#define HUNGRY 1 /* philosopher is trying to get for ks */
#define EATING 2 /* philosopher is eating */
typedef int semaphore; /* semaphores are a special kind of int */

int state[N]; /* array to keep track of everyone’s state */
semaphore mutex = 1; /* mutual exclusion for critical regions */
semaphore s[N]; /* one semaphore per philosopher */

void philosopher(int i) /* i: philosopher number, from 0 to N−1 */
{
    while (TRUE) { /* repeat forever */
        think(); /* philosopher is thinking */
        take_forks(i); /* acquire two forks or block */
        eat(); /* yum-yum, spaghetti */
        putforks(i); /* put both forks back on table */
    }
}

void take_forks(int i) /* i: philosopher number, from 0 to N−1 */
{
    down(&mutex); /* enter critical region */
    state[i] = HUNGRY; /* record fact that philosopher i is hungry */
    test(i); /* try to acquire 2 forks */
    up(&mutex); /* exit critical region */
    down(&s[i]); /* block if forks were not acquired */
}

void put_forks(int i) /* i: philosopher number, from 0 to N−1 */
{
    down(&mutex); /* enter critical region */
    state[i] = THINKING; /* philosopher has finished eating */
    test(LEFT); /* see if left neighbor can now eat */
    test(RIGHT); /* see if right neighbor can now eat */
    up(&mutex); /* exit critical region */
}

void test(int i) /* i: philosopher number, from 0 to N−1 */
{
    if (state[i] == HUNGRY && state[LEFT] != EATING && state[RIGHT] != EATING) {
        state[i] = EATING;
        up(&s[i]);
    }
}
```  

## 2.Readers & Writers
- Problem
  - Imagine an airline reservation system, with many competing processes wishing to read and write it. It is acceptable to have multiple processes reading the database at the same time, but if one process is updating (writing) the database, no other processes may have access to the database, not even readers.
- Solution

```C++
typedef int semaphore; /* use your imagination */

semaphore mutex = 1; /* controls access to rc */
semaphore db = 1; /* controls access to the database */
int rc = 0; /* # of processes reading or wanting to */

void reader(void)
{
    while (TRUE) { /* repeat forever */
        down(&mutex); /* get exclusive access to rc */
        rc = rc + 1; /* one reader more now */
        if (rc == 1) down(&db); /* if this is the first reader ... */
        up(&mutex); /* release exclusive access to rc */

        read_data_base( ); /* access the data */

        down(&mutex); /* get exclusive access to rc */
        rc = rc − 1; /* one reader few er now */
        if (rc == 0) up(&db); /* if this is the last reader ... */
        up(&mutex); /* release exclusive access to rc */

        use_data_read( ); /* noncritical region */
    }
}

void writer(void)
{
    while (TRUE) { /* repeat forever */
        think_up_data( ); /* noncr itical region */
        down(&db); /* get exclusive access */
        write_data_base( ); /* update the data */
        up(&db); /* release exclusive access */
    }
}
```

## 3.Driver & Busman
```C++
semaphore door = 0;
semaphore move = 0;

void driver() {
    down(move);
    driving();
    reachingStaion();
    up(door);
}

void busman() {
    up(move);
    selling();
    down(door);
}
//Sequence:
//up(move) -> down(door) -> down(move) -> up(door)
```

## 4.Producer & Consumer
```C++
#define N 100
int in = 0, out = 0;
item buffer[N];
semaphore mutex = 1;
semaphore empty = N, full = 0;

void producer() {
    while(true) {
        produce an item nextp;
        ···
        down(empty);  
        down(mutex); 
        buffer[in] = nextp;
        in = (in+1)%n;
        up(mutex);
        up(full); 
    }
}

void consumer() {
    while(true) {
        down(full);
        down(mutex);
        nextc = buffer[out];
        out = (out+1) %n;
        up(mutex);
        up(empty);
        ...
        consume an item nextc;
    }
}
```