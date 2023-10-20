
> one of the most influential developments in the history of concurrent programming

Communicating Sequential Processes (CSP) is a formal language and framework for describing and analyzing concurrent systems. It provides a mathematical model and a set of rules for composing and synchronizing concurrent processes through message passing. CSP was first introduced by Tony Hoare in the 1970s as a way to reason about the behavior of concurrent systems.

In CSP, a system is modeled as a collection of individual processes that communicate with each other by sending and receiving messages. Each process is composed of a set of sequential steps, and communication between processes occurs through well-defined channels. The key idea behind CSP is that processes can only communicate through explicit synchronization on these channels, and the order of communication is strictly determined by the sequence of events.

Here are some important concepts and features of CSP:
1. Processes: In CSP, processes are independent entities that execute sequentially. Each process has its own state and can perform a series of actions. These actions may include sending or receiving messages, performing computations, or modifying internal state.
2. Channels: Channels act as the communication medium between processes in CSP. They provide a way to pass messages from one process to another. Channels can be unidirectional (only allowing messages to flow in one direction) or bidirectional (allowing messages to flow in both directions).
3. [[Message Passing]]: Communication in CSP occurs through message passing. A process can send a message over a channel, and another process can receive that message from the channel. Message passing is a synchronous operation, meaning that both the sender and the receiver must be ready and willing to participate in the communication.
4. Synchronization: CSP enforces synchronization between processes by requiring them to synchronize on channels. When a process attempts to send or receive a message on a channel, it will block until another process is ready to perform the complementary action. This ensures that communication happens in a coordinated and predictable manner.
5. Process Composition: CSP allows processes to be composed together to create more complex systems. Processes can be combined using various operators, such as parallel composition, sequential composition, and choice composition. These composition operators enable the construction of larger systems from smaller, reusable components.
6. Safety and Liveness Properties: CSP provides a formal framework for reasoning about the safety and liveness properties of concurrent systems. Safety properties ensure that certain undesirable states or behaviors are not reached, while liveness properties ensure that desired states or behaviors eventually occur.


CSP has influenced the development of other concurrency models and programming languages, such as the actor model and the Go programming language. It provides a rigorous foundation for understanding and analyzing concurrent systems, allowing developers to reason about the correctness and behavior of their programs in a formal and mathematical way.

Example: 
```jsx
process A { ...B!e; ... }
process B {... A?x; ... }

```

- `B!e;`  is called an output statement, it names a destination process B, and specifies an expression e which value is to be sent to that process.
- `A?x;`  is called an input statement, it names a source destination from process A, and specifies the variable, where the input message from the source is to be stored.
- these are called `output/input` statements rather then send/recieve, because they are used as both external and inter process communication.
- these two statements are set to `match`.
    - an input or output statement delays the execution process until another process reaches an matching statement.
    - the two statements are then executed simultaneously.
    - the effect is to assign the value of the expression in the `output`statement to the variable in the `input` statement.
- the execution of matching communication statements can be viewed as a distributed assignment
    - transfers a value from one process to a variable another
- the two processes are synchronized while communication takes place, then each process proceeds independently
- the general form:

```jsx
Destination!port(e_1, ..., e_n)
Source?port(x_1, ..., x_n);
```

- `Desitnation` and `Source` names a single process, or an element of an array of processes.
- the source[*]
    - can read from any process in an array of processes
- example

```jsx
process Copy {
	char c;
	do true -> 
			West?c;
			East!c;
	od
}

// copies a character from process west and outputs a character to
// the process east.
// do statement here loops forever. 
```

- the input statement in the example above waits until West is ready to send a character
- the output statement waits until east is ready to take it.
- the `do` and `if` statements in CSP uses guarded commands(Djikstra)
    - form: B -> S

---

### Guarded Communication.

- input and output statements enable processes to communicate.
    - But by themself they are limited
    - both are blocking statements
    - often a process wishes to communicate with different processes, often over different ports, and they dont have an overview in which order other processes wants to communicate with them.
- Guarded communication statements support non-determenistic communication.
    - 

```jsx
B; C -> S; 
//B is a boolean expression 
//C is a communication statement
//S is a statement lease
```

- the `B; C` is called the guard
    - the guard succeds if `B` is `TRUE` and executing `C` would not cause a delay.
    - a guard fails if `B` is false.
    - a guard is blocked if `**B`** is true, but `C` cannot be yet executed.
        - *will be blocked and the program will wait until C becomes available to execute. This is because guarded communication statements in concurrent programming require both the guard and the communication to be ready before the statement can execute. If either the guard or the communication is not ready, the statement will wait until it is ready before proceeding.*
- Guarded communication statements appear within `if` and `do` statements
    - example
    
    ```jsx
    if B1; C1 -> S1;
    [] B2; C2 -> S2;
    fi
    ```
    
- ways of executing:
    - First:
        - if both guards fail, the `if` statement terminates with no effect
        - if atleast one guard succeds (non-deterministicly), it goes
        - if both guards block, it waits until one of the guards succeds.
    - Second:
        - after choosing the guard that succeds, execute the communication statement `C` in the choosen guard
    - Third:
        - execute the corresponding statement `S`
    - and at this point, the `if` statement terminates.
    - the `do` statement is executed in a similar way
        - the difference is that the process of selecting a guard, is repeated until all guards fail.
- illustration:

```jsx
Process Copy {
	char c;
	do West?c -> East!c;
	od
}
// we have moved the input statement into the guard of the 
// do statement. Since the guard does not contain an boolean
// expression, it will never fail and the do statement will
// loop forever. 
```

- example:

```jsx
Process Copy {
	char c1, c2;
	West?c1;      // one char is buffered in c1 at start of every itaration of do
	do West?c2 -> East!c1; c1=c2; // waits for a 2nd char from west, outputs the first char to east, then assigns c2 to c1.  
	[] East!c1 -> West?c1; //outputs the first char from to east and inputs another char to west
	od 
}
```

- example of bounded buffer

```jsx
process Copy {
	char buffer[10];
	int front = 0; rear = 0; count = 0;
	do count < 10; West?buffer[rear] -> count++; rear = (rear+1) mod 10;
	[] count > 0; East!buffer[front] -> count--; front = (front+1) mod 10;
	od
}
```

- by using CSP, we can program a symmetric exchange.
- Example of symmetric exchange:

```jsx
process P1 {
	int value1 = 1;
	int value2;
	if P2!value1 -> P2?value2;
	[] P2?value2 -> P2!value1;
	fi
}

process P2 {
	int value1;
	int value2 = 2;
	if P1!value2 -> P1?value1;
	[] P1!value1 -> P1!value2;
	fi
}

//symmetric exchange
//matching symmetric statements
```

- The Sieve of Eratosthenes:

```jsx
process Sieve[1] {
	int p = 2;
	for [i = 3 to n step 2] Sieve[2]!i;
}

process Sieve[i=2 to L] {
	int p, next;
	Sieve[i-1]?p;
	do
		Sieve[i-1]?next -> 
			if
				(next mod p) != 0 -> Sieve[i+1]!next;
			fi
	od
}
```

- Greatest Common Divisor(GCD):

```jsx
process GCD {
	int id, x, y;
	do true ->
		client[*]?args(id, x, y);
		do x > y -> x = x - y;
		[] x < y -> y = y - x;
		od
		Client[id]!result(x);
	od
}
```

---

### Modern CSP:

`green -> red -> STOP`

`LIGHT = green -> red -> LIGHT`

`COPY1 = West?c:char -> East!c -> COPY1`

- Functional
- prefixing (sequencing)
- recursion (repetition)
- guarded alternatives (nondetermenistic choice)

---

### Exam Questions:

- Using Communicating Sequential Processes, define a process **Copy** that copies a character from process **Vestland** to process **Bergen**.

```jsx
process Copy {
	char c;
	do true ->
		vestland!e;
		Bergen!x;
	od
	
}
```