Semaphores and barriers are synchronization mechanisms commonly used in concurrent programming to control the execution and coordination of multiple threads.

## Semaphores 
A disciplined wait to implement signaling and scheduling, and are supported by majority of the libraries.
-  A semaphore is a signaling mechanism used to control access to a shared resource or limit the number of threads that can access a resource concurrently.
- Semaphores maintain a counter that can be incremented or decremented by threads to indicate the availability of resources.
- There are two types of semaphores: binary semaphore and counting semaphore.
	- Binary semaphore has two states: 0 and 1, typically used for mutual exclusion. It can be used to control access to a shared resource where only one thread can hold the lock at a time.
	- Counting semaphore has an internal counter that can be incremented and decremented by threads. It can be used to control access to a resource with multiple instances or to limit the number of threads that can access the resource concurrently.
- Semaphores provide synchronization by allowing threads to block (wait) or proceed (signal) based on the state of the semaphore counter.
- The `acquire()` operation is used by a thread to request access to a semaphore, and if the semaphore counter is greater than zero, the thread can proceed. Otherwise, the thread blocks until a resource becomes available or the semaphore is signaled.
- The `release()` operation is used to release the semaphore, incrementing the counter and potentially allowing blocked threads to proceed.


- Provides a basic signaling mechanism an are used to implement [[Deadlock|mutual exclusion]] and condition synchronization
- `sem s`;
    - shared variable
    - can only be manipulated by two atomic operations
        - `P` → wait for signal
            - effect: wait until value **>** 0, then decrease the value by 1. ****
        - `V` → signal an event
            - effect: increase value by 1
        - Passeren and vrijgeven
        - 
```jsx
sem s; // initialized to zero
sem lock = 1;
sem forks[5]; 
```

- a value of semaphore; ``sem s``;
	- a non-negative integer
	- default value 0
- Operation V: to signal the occurrence of an event!
	- increments the value of a semaphore
- Operation P: to delay a process until an event has occurred
	- waits until the value of a semaphore is positive, and then decrements the value; the power of the semaphore comes from this.
- `P(s):  <await (s>0) s =  s - 1 >`        → signal atomic action
- `P(s):  <s = s + 1>`
- Weakly fair scheduling policy: if conditional atomic actions eventually get to execute if the delay condition becomes true and remains true
- Strongly fair scheduling policy: if conditional atomic actions eventually get to execute if the delay condition is infinitely often true
- V(s): unconditional fair scheduling policy
- await semaphore
- Critical section problem: solved with semaphores

```jsx
sem mutex = 1;

process CS[i=1 to n] {
	while (true) {
		P(mutex);
			critical section;
		V(mutex);
		non-critical secetion;
	}
}
    ```


```jsx
bool lock = false;
process CS[1] {
	while(true) {
		<await (!lock) lock=true;>
			critical section
		lock = false;
		non-critical section;
	}
}
```

## General and Binary Semaphores
- General semaphore: can take any non-negative value
- Binary semaphore: one whose value is always either 0 or 1
	- V operation on a binary semaphore: executed only when the semaphore has value 0
- Barriers: signaling event
    - Previously: we used flag variables
    - Idea: use one semaphore for each synchronization flag
    - A process sets a flag by executing V operation
    - A process waits for a flag to be set and then clears it by executing P operation
    - Simplification: consider a 2-process barrier
        - neither process can get past the barrier until both have arrived
        - the barrier must be reusable since in general the same processes will need to synchronize after each stage of the computation
    - We use two semaphores as signals: we need to know each time a process arrives at or departs from the barrier
- Signaling semaphore: intialized to 0
    - a process signals an event by executing V(s)
    - other processes wait for that event by executing P(s)
    - 2 - process barrier:
        - Significant events are the process arriving at the barrier
        - Use two semaphores: arrive1, arrive2
        - Each process: signals its arrival by executing V operation in its own semaphore, then waits for the other processs to arrive by executing P operation on the other processes semaphore
    - Barrier synchronization is symmetric, hence, each, process take the same actions

```jsx
sem arrive1 = 0;
sem arrive2 = 0;

process Worker1 {
	...
	V(arrive1); // signal arrival 
	P(arrive2); // wait for other process
	...
}

process Worker2 {
	...
	V(arrive2); // signal arrival 
	P(arrive1); // wait for other process
	...
}
```

## Producers and Consumers:
- Copy all elements of an array from the producer to the consumer
- Producer
	- `a[n]`
- Consumer
	- `b[n]`
- `buffer`
- `p`: the number of items that have been deposited.
- `c`: the number of items that have been fetched.
- synchronization requirements: c ≤ p ≤ c+1
	- the values `c` and `p` can differ by at-most one, aka the producer has deposited at-most one more element than the consumer has fetched.

    ```jsx
// Copy all elements of an array from the producer to the consumer
int buf = 0;
int p = 0;
int c = 0;

process Producer {
	int a[n]; // the elements that is being sent
	while (p<n) { 
		<await(p==c; buf=a[p]; p=p+1:> // waits for fetch to be done, then copys to the buffer, and increases the variable p
	}
}

process Consumer {
	int b[n]; // stores the elements being received from the producer
	while(c<n) { 
		<await (p>c); b[c] = buf; c=c+1;> // waits for p to increase, copy from buffer, increase c, so that Producer knows that its fetched
	}
}
    ```
    

## Split binary Semaphores:
- multiple producers and consumers
- signaling flags semaphores
- producers -> `deposit`
- consumers -> `fetch`
- signaling semaphores:
    - to indicate when processes reach critical execution points
    - to indicate changes to the status of shared variables
    - deposit; fetch;  -> critical execution points
    - semaphores:
        - empty=1;
        - full=0;
    - when a producer wants to deposit,  the buffer must be empty ( =1),
```jsx
//split binary semaphores for producer/consumer
typeT buf;
sem empty = 1;
sem full  = 0;

process Producer[i = 1 to M] {
	while(true) {
		..
		P(empty);
		buf data;
		V(full);
		..
}

process Consumer[j = 1 to N] {
	while(true) {
		..
		P(full);
		result = buf;
		V(empty);
		..
}
    ```


## Bounded Buffers: Resource Counting.
- producer and consumer execution is tricky
- e.g., producer may produce alot of data and needing a bigger buffer
- `buf[n], n>1`
- `front`: the index of the message at the front of the queue
- `rear`: the index of the firsty empty slot past the message at the rear of the queue.
- `mod n` is used to ensure that the values of front and rear are always between 0 and (n-1)
```jsx
buf[rear] = data;
rear = (rear+1) mod n;
result = buf[front];
front = (front+1) mod n;

0 .. n-1
buf[front] .. ~~buf[rear]~~ // up to, but not includning rear
~~~~buf[n-1]; buf[0];
    ```
- deposit and fetch can execute concurrently if there is both an empty slot and a stored message, and will not interfere with eachother.
	- use of P(s) and V(s) used the same
	- difference: the semaphore empty is initialized to n and not to 1.
		- `sem n;`
		- ~~`sem 1;`~~
		- because there are intialiy `n` empty slots
- code solution: circular buffer and counting semaphores:
    ```jsx
typeT buf[n];
int front = 0;
int rear = 0;
sem empty = n;
sem full  = 0;

process Producer {
	while(true) {
		..
		P(empty);
		buf[rear]=data; rear=(rear+1) mod n;
		V(full);
		..
}

process Consumer {
	while(true) {
		fetch message result and consume it;
		P(full);
		result = buf[front]; front=(front+1) mod n;
		V(empty);
}
```

  - code example:

```jsx
typeT buf[n];
int front = 0;
int rear = 0;
sem empty = n;
sem full  = 0;
sem mutexD = 1;
sem mutexF = 1;

process Producer[i = 1 to M] {
	while(true) {
		..
		produce the message data and deposit in the buffer;
		P(empty);
		P(mutexD);
		buf[rear]=data; rear=(rear+1) mod n;
		V(mutexD);
		V(full);
		..
}

process Consumer[j = 1 to N] {
	while(true) {
		fetch message result and consume it;
		P(full);
		P(mutexF);
		result = buf[front]; front=(front+1) mod n;
		V(mutexF);
		V(empty);
}
    ```
- this provides mutual exclusion on critical sections where the indices `rear` and `front` are updated.
- `mutexD`: now only one producer can modify the `rear` index at a time
- `mutexF`: now only one consumer can modify the `front` index at a time.
- the `empty` and `full` ensures that producers and consumers block when the buffer is either full or empty, avoiding busy-waiting and unnecessary CPU usage.



## The dining philosopher problem
- 5 pilosophers, each need two forks, and one fork is placed between them. But there are only 5 forks.
- we need to avoid deadlock
- circular waiting cannot reccur.
	- make the last pilosopher pick up the right, while the others pick up left.

    ```jsx
sem fork[5] = {1, 1, 1, 1, 1 };

process Philosopher[i=0 to 3] {
	while(true) {
		P(fork[i]); P(fork[i+1]);
		eat;
		V(fork[i]); V(fork[i+1]);
		think;
   }
}

process Pilosopher[4] {
	while(true) {
		P(fork[0]); P(fork[4]);
		eat;
		V(fork[0]); V(fork[4]);
		think;
	 }
}
    ```

- another is to get odd-number to pick up one side first, and the even numbered to pick up in the other order.



## Readers and Writers:
- `Readers`: examine
- `Writers:` examine + update
- a practical problem often used.
	- shared data source
- selective mutual exclusion
	- here classes of processes (r, w) compete for the access to the data source
	- `Readers` processes: compete with writers
	- `Writers`: compete with each other
	- Reader processes must wait until no writers are accessing the database
	- Writer processes must wait until no readers or other writers are accessing the data source / database.
- Writer process need mutually exclusive access to the database
- Reader process(as a group): also need exclusive access with respect to any writer process.
- Approach: overconstrain the solution; then relax
- Each reader and writer process have exlusive access to the database
- Mutual exclusion `semaphore rw=1`;
- example:

    ```jsx
sem rw = 1;
int nr = 0;

process Reader[i = 1 to M] {
	while(true) {
		...
		<nr=nr+1; if(nr==1) P(rw);> //if first reader, then get lock
		
		read the data;
		<nr=nr-1; if(nr==0) V(rw);> // if last reader, then release lock
		...
	}
}

process Writer[j = 1 to N] {
	while(true) {
		...
		P(rw);
		write to the database;
		V(rw);
		...
}
    ```

- better example (complete solution).  Readers preference solution.

```jsx
sem rw = 1;
int nr = 0;
sem mutexR =1; // lock for reader access to nr

process Reader[i = 1 to M] {
	while(true) {
		...
		P(mutexR);
		nr=nr+1; 
		if(nr==1) P(rw); //if first, then get lock
		V(mutexR);
		read the database;
		P(mutexR);
		nr=nr-1; 
		if(nr==0) V(rw);> // if last, then release lock
		V(mutexR);
		...
	}
}

process Writer[j = 1 to N] {
	while(true) {
		...
		P(rw);
		write to the database;
		V(rw);
		...
}
    ```

- this solution above is not fair
- Code example: conditional synchronization with chat GPT.

    ```jsx
sem mutex = 1;
sem wrt = 1;
int nr = 0;

process Reader[i = 1 to M] {
	while (true) {
		...
		P(mutex);
		nr++;
		if (nr == 1) {
			P(wrt); // lock the database for writers
		}
		V(mutex);
		  read the database;
		P(mutex);
		nr--;
		if (nr == 0) {
			V(wrt); // release the lock if no readers are left
		}
		V(mutex);
		...
	}
}

process Writer[j = 1 to N] {
	while (true) {
		...
		P(wrt); // wait to acquire the lock for writers
		write to the database;
		V(wrt); // release the lock for writers
		...
	}
}
    ```

- Passing the baton:
- first phase:

```jsx
int nr = 0;
int nw = 0;

process Reader[i=1 to M] {
	while(true) {
		...
		<await (nw==0) nr=nr+1;>
		read database;
		<nr=nr-1;>
		...
	}
}

process Writer[j=1 to n] {
	while(true) {
		...
		<await(nr==0 and nw==0) nw=nw+1;>
		write to database
		<nw=nw-1;>
	}
}
    ```

second:

```jsx
int nr = 0;
int nw = 0;

sem e = 1;
sem r = 0;
sem w

int dr = 0;
int dw = 0;

process Reader[i=1 to M] {
	while(true) {
		...
		//<await (nw==0) nr=nr+1;>
		P(e);
		if(nw > 0) { dr=dr+1; V(e); P(r); }
		nr = nr + 1;
		SIGNAL;
		read database;
		//<nr=nr-1;>
		P(e);
		nr = nr-1;
		SIGNAL;
		...
	}
}

process Writer[j=1 to n] {
	while(true) {
		...
		<await(nr==0 and nw==0) nw=nw+1;>
		write to database
		<nw=nw-1;>
	}
}

SIGNAL:
if (nw == 0 and dr > 0) {
	dr = dr - 1;
	V(r);  // awaken a reader
}
else if (nr == 0 and nw == 0 and dw > 0) {
	dw = dw - 1;
	V(w);  // awaken a writer
}
else {
	V(e);  // release the entry lock
}
```

## Barriers
- A barrier is a synchronization point that ensures a group of threads reaches a common point before proceeding further.
- Barriers are commonly used when multiple threads need to synchronize their progress and wait for all threads to reach a specific point before proceeding.
- A barrier has a predefined count, specifying the number of threads required to reach the barrier before it is released.
- Threads reach the barrier and wait until all other threads in the group have also reached the barrier. Once the last thread arrives, the barrier is released, and all threads can proceed.
- Barriers are useful in scenarios where threads need to divide a larger task into smaller subtasks and synchronize their progress at certain points.

Both semaphores and barriers are valuable tools for managing thread synchronization and coordination in concurrent programming. Semaphores allow for more flexible resource management and control, while barriers facilitate synchronization among threads at designated points in their execution. The choice between semaphores and barriers depends on the specific requirements and synchronization needs of the concurrent program.