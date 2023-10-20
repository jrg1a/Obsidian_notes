
What is message passing?

- a form of communication between concurrent processes or threads in a concurrent program. Messages are sentand received through a communication channel or message queue.
- message passing provides a way for concurrent processes or threads to exchange information and coordinate their actions without sharing memory. This can help prevent race conditions, deadlocks, and other issues.
- each process or thread has its own memory space and communicates with other processes or threads by sending and receiving messages.
    - a message contains a data payload and a destination address

######  Synchronous message passing

- the sender blocks until the receiver has acknowledged receipt of the message
- the sender and receiver must synchronize their actions in order to exchange messages. This means that the sender cannot proceed until the receiver has recived the message, which can result in a `delay` or a `wait`
- ***advantage***: strong guarantee that the message has been successfully delivered and processed by the receiver before the sender can continue.
- can prevent synchronizations errors and other issues that can arise when multiple threads access shared resource simultaneously
- since it requires that the sender has to wait for a repsonse from the receiver, it can introduce a delay in the program execution. Considered an ***disadvantage*** where performance is critical

###### Asynchronous message passing
- the sender does not block and can continue executing while the message is being transmitted and processed.
- the sender and receiver can exchange messages without syncing their actions
- ***advantage***: can improve performance and concurrency by allowing the sender to continye executing while the message is being processed by the receiver.
	- aware: can cause issues with sync and race conditions.
- Message passing can be used in combination with other concurrency control mechanisms, such as locks, semaphores, and monitors, to coordinate the actions of multiple threads or processes. This can help to prevent synchronization issues and ensure correct program behavior
- Message passing is a fundamental concept in distributed systems and can be used to exchange messages between processes running on different machines. In this case, the communication mechanism typically involves network protocols and sockets, and additional mechanisms such as serialization and deserialization may be required to convert data into a format that can be transmitted over the network.
- Methods to prevent issues in async message passing:
    - [[Semaphores & Barriers|semaphores]]
    - message queues
    - mutual exclusion

###### Async message passing code:
- send are like V operation
- receive are like P operation
- `chan ch (type1 id1, ..., typen idn)`
- `chan input(char)`
- `chan disk_access(int cylinder, int block, int count, char*buffer)`
- `chan result[n](int);`
- `send ch(expr1, ... , exprn);`  non blocking primitive
- `receive ch(var1, ... , varn);`
- example of a filter process:

```jsx
chan input(char), output(char[MAXLINE]);
process char_to_line {
	char line[MAXLINE]; int i = 0;
	while (true) {
		receive input(line[i]);
	}
	line[i] = EOL;
	send output(line);
	i = 0;
	}
}
        ```