Threads and locks are fundamental concepts in concurrent and multi-programming that enable the execution of multiple tasks or processes simultaneously. They are essential for achieving parallelism and efficient utilization of resources in modern computer systems.

## Threads
A thread is a lightweight unit of execution within a process. It represents an independent sequence of instructions that can be scheduled and executed concurrently with other threads. Threads share the same memory space and resources of the process they belong to, allowing them to access and modify shared data. By utilizing threads, a program can perform multiple tasks simultaneously, enhancing responsiveness and improving performance.
- Thread and locks -- java Thread Example:
![Untitled](Untitled.png)

## Thread Synchronization
Thread synchronization is necessary when multiple threads access shared data concurrently. Without proper synchronization mechanisms, concurrent access to shared data can lead to race conditions, data corruption, and other undesirable outcomes. Locks, also known as mutexes, are commonly used synchronization primitives to protect critical sections of code or shared resources.

## Locks 
A lock is a synchronization mechanism that provides mutual exclusion. It ensures that only one thread can access a critical section of code or a shared resource at a given time, preventing concurrent interference. When a thread acquires a lock, it gains exclusive access to the protected resource, allowing it to perform operations without interference from other threads. Other threads attempting to acquire the same lock will be blocked until the lock is released.

Types of Locks:
1. Reentrant Locks: Reentrant locks allow a thread to acquire the same lock multiple times without deadlocking itself. They provide a higher level of control and flexibility compared to intrinsic locks (synchronized keyword in Java) by allowing explicit lock acquisition and release. 
2. Read/Write Locks: Read/Write locks are specialized locks that provide concurrent access for read operations but exclusive access for write operations. Multiple threads can acquire the read lock simultaneously if no thread holds the write lock. This allows for improved concurrency in scenarios where read operations outnumber write operations.
3. [[Monitors|Condition Variables]]: Condition variables are synchronization objects associated with locks. They allow threads to wait until a specific condition is met before proceeding. Condition variables are useful in scenarios where threads need to coordinate their actions based on certain criteria or signals.

## Thread safety, Deadlocks, and Livelocks
Ensuring thread safety is crucial in concurrent programming. It involves designing and implementing code that can be safely executed by multiple threads concurrently without data corruption or unexpected behavior. Deadlocks and livelocks are common issues that can arise in concurrent programs.
-   Deadlock: Deadlock occurs when two or more threads are blocked indefinitely, waiting for each other to release resources or locks. This leads to a program freeze or unresponsiveness. Proper lock acquisition order, lock timeouts, and resource allocation strategies can help avoid deadlocks.
-   Livelock: Livelock occurs when threads are not blocked, but they are unable to make progress due to continuously responding to the actions of other threads. It is a situation where threads are effectively stuck in a loop of responding to each other without accomplishing their tasks. Livelocks can be resolved by introducing randomness or adjusting the scheduling strategy.

Proper understanding and application of threads and locks are essential for effective concurrent and multiprogramming. They enable parallel execution, efficient resource sharing, and synchronization of access to shared data, ensuring correctness and optimal performance in concurrent systems.

## Notes
Memory model: two threads try to access one variable and write to its memory, creating a race condition.
- Read-monitor-write
	- synchronize the access to the variable, maybe with intrinsic lock that comes with java
- Compiler, JVM and hardware is allowed to statically optimize the code by reordering things
	- can create problems where two threads are running and operating on the same variables
	- synchronized method should be used by both threads, not only one
	- if not; race condition and memory problems

#### Deadlocks; several locks and dining philosopher
- Multiple locks can create [[deadlock]] 
- The dining philosopher problem: [[Semaphores & Barriers|Dining Philosopher]]
![Skjermbilde.PNG](Skjermbilde%201.png)
- either thinking or hungry
	- if hungry = eat
	- if thinking = not using chopstick
- the deadlock can happen when one of the locks tries to acquire another lock, like here when the philosopher has the right chopstick and tries to acquire a lock for the left one, but the philosopher to the left also waiting for its left and holding on to the right, etc.
	- thus creating a [[deadlock]] where everyone is waiting for a condition that is never fulfilling
- can be fixed by acquiring locks in a fixed global order!
	- e.g hold on to id of the chopsticks, and making them lock in increasing order

#### Synchronization and alien methods:
- even if there's only one lock, there can be caused problems
- when a program calls a method that its not in our code, aka an alien method
	- e.g from a library
- the alien method might try to acquire an lock, thus can create an deadlock
- when we want to call alien method, we try to call them outside locks
	- defensive copy; avoid calling alien method withing a held lock, and also minimize the time which the method holds on to a lock.
		- hold locks at the shortest possible time
		
#### Reentrant Lock
- Intrinsic locks:
	- no way to interrupt a thread that's blocked as a result of trying to acquire an intrinsic lock
	- no way to time out while trying to acquire lock
	- exactly one way to acquire lock
	- acquiring and releasing the lock - in the same method
- Java.util.concurrent
	- Reentrant lock, avoids infinite deadlock with recovery time
	- live lock can happen



#### Condition Variables
Condition variables are synchronization primitives used in concurrent programming to allow threads to wait for a certain condition to become true before proceeding. They are typically associated with locks and provide a mechanism for threads to coordinate their actions based on specific conditions or signals.

In general, condition variables enable threads to block and wait until another thread signals that a certain condition has been met. They are useful in scenarios where thread execution needs to be coordinated and synchronized, such as producer-consumer problems, thread communication, and thread cooperation.

Key concepts related to condition variables:
1. Wait and Signal Operations:
    - `wait()`: A thread calling the `wait()` method on a condition variable releases the associated lock and waits until it is signaled by another thread.
    - `signal()`: A thread calling the `signal()` method on a condition variable wakes up one waiting thread. If multiple threads are waiting, only one thread is chosen to be awakened.
2. Signaling and Notification:
    -   Condition variables support two modes of signaling:
        - `signal()`: Wakes up a single waiting thread. The awakened thread must reacquire the lock before it can continue its execution.
        - `signalAll()`: Wakes up all waiting threads. Each awakened thread must reacquire the lock before proceeding.
3. Spurious Wakeups:
    - In some cases, a thread waiting on a condition variable may be awakened without a corresponding signal. These are called spurious wakeups. It is essential to guard against spurious wakeups by using a loop construct that rechecks the condition after waking up.
4. Guarded Blocks:
    - A common pattern in using condition variables is to enclose the wait operation in a while loop that tests for the desired condition. This is known as a guarded block and helps protect against spurious wakeups and ensure the condition is still true after waking up.

Condition variables play a crucial role in thread synchronization and coordination. They allow threads to wait until a specific condition is met, reducing unnecessary busy-waiting and improving overall system efficiency. Proper usage of condition variables, in combination with locks, helps ensure correct thread synchronization and avoids issues like race conditions and deadlocks.

It's important to note that different programming languages and frameworks may provide different implementations and variations of condition variables, but the underlying concept and purpose remain the same: enabling threads to wait for a condition to become true before proceeding.

- we often need to wait for a condition to fulfill
- Condition cond = lock.newCondition();
	- use a while loop within a try/finally block
	- thread must hold the lock and check if the conditions are true before starting
	- if not it wail invoke the await() statmement, until the signal() or signalAll() is given
		- checks wether if the condition is fulfilled again

#### Atomic variables
Atomic variables, also known as atomic types or atomic classes, are special types in concurrent programming that provide atomic operations on shared variables without the need for explicit locking. They ensure that operations on the variables are performed atomically, meaning they are indivisible and appear as a single, consistent action from the perspective of other threads.

In multithreaded environments, when multiple threads concurrently access and modify shared variables, synchronization is required to maintain data integrity and prevent race conditions. Traditionally, locks (e.g., synchronized blocks or explicit locks) are used to achieve mutual exclusion and ensure thread-safe access to shared data. However, using locks can introduce overhead and potential issues like deadlock or contention.

Atomic variables provide an alternative approach by using low-level atomic instructions provided by the hardware or operating system to perform operations on shared variables atomically. These atomic operations guarantee that no other thread can observe an intermediate or inconsistent state during the execution of the operation.

Some key characteristics of atomic variables are:
1.  Atomicity: Operations on atomic variables are performed atomically, without interruption or interference from other threads.
2.  Lock-Free: Atomic variables use hardware-level or OS-level atomic instructions to achieve synchronization without the need for explicit locks.
3.  Thread-Safety: Atomic variables ensure thread-safe access to shared data without the need for external synchronization mechanisms.
4.  Supported Operations: Atomic variables typically support common operations such as read, write, compare-and-set, increment, decrement, etc., as atomic operations.

Java provides the `java.util.concurrent.atomic` package, which includes several atomic classes such as `AtomicInteger`, `AtomicLong`, `AtomicBoolean`, and more. These classes encapsulate atomic variables with methods to perform atomic operations on them.

Using atomic variables can simplify concurrent programming and eliminate the need for explicit locks in some scenarios. They are particularly useful when dealing with simple, independent operations on shared variables, where the granularity of locking would be excessive or unnecessary.

However, it's important to note that atomic variables are not a universal replacement for locks. They are most effective when used for simple operations on individual variables. For more complex operations or when dealing with multiple variables that require consistent updates, explicit locking mechanisms may still be necessary to ensure correct synchronization and maintain data integrity.

- atomic integer
- atomic variables advantages:
	- cant forget to acquire lock before executing an operation
	- avoid the deadlock situation
	- basis of blockfree algorithms
		- achieves without locks
- be interrupted while trying to acquire a lock
- time out while acquiring a lock
- acquire and release locks in any orders
- avoid locks entirely by using atomic variables

#### Recap:
- sequential programs: one thread of execution
- concurrent: multiple threads of execution
- shared memory concurrency
- message passing concurrency

Threads and locks are fundamental concepts in concurrent programming that enable the execution of multiple tasks concurrently while ensuring data integrity and synchronization.

Threads:
- Threads represent individual units of execution within a program. They allow multiple tasks to run concurrently and independently of each other.
- Threads share the same memory space, allowing them to access and modify shared data.
- Threads can be created and managed in programming languages, including Java, using thread APIs and libraries.
- Concurrent execution of threads can lead to race conditions and data inconsistency if proper synchronization is not in place.

Locks:
- Locks are synchronization mechanisms used to coordinate access to shared resources in a multithreaded environment.
- Locks ensure that only one thread can access a shared resource at a time, preventing race conditions and maintaining data integrity.
- Locks provide mutual exclusion, allowing threads to acquire the lock and enter critical sections of code, ensuring exclusive access to shared resources.
- Locks can be implemented using various mechanisms, such as synchronized blocks or explicit lock objects, depending on the programming language or concurrency library.
- Locks can be used to protect critical sections of code, ensuring that only one thread can execute that section at a time.
- Locks can be non-reentrant or reentrant, depending on whether a thread can acquire the lock multiple times.

Recap:
- Threads enable concurrent execution and allow multiple tasks to run simultaneously.
- Locks provide synchronization and mutual exclusion to ensure thread-safe access to shared resources.
- Proper use of locks helps prevent race conditions, data inconsistencies, and other concurrency-related issues.
- It is important to use locks judiciously, considering factors such as granularity, performance, and potential deadlock situations.
- Concurrent programming requires careful design and synchronization techniques to ensure correct and efficient execution in multithreaded environments.