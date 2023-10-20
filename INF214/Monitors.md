
[[Semaphores & Barriers|Semaphores]] could be difficult to understand as we has to look at the other operations in the program to understand what the P and V operations purpose is. 
- Semaphores: easy to program mutual exclusion, signaling
- can be used in a systematic way to solve any synchronization problem
However:
- [[Semaphores & Barriers|Semaphores]] are a low-level mechanism!
    - easy to make errors!

###### Monitors:
- provide more structure than semaphores and can be implemented as efficiently
    - program modules
    - [[Deadlock|mutual exclusion]]: provided implicity
    - condition synchronization: via condition variables

**Monitors:**
- Interface + body
- Various syntax in different languages
- Active processes
- Passive monitors
- Monitor properties:
    - only the procedure names are visible outside of a monitor
    - statements within a monitor may not access variables outside the monitor
    - permanent variables are initialized before any procedure is called
- **Condition variables**:
    - to delay a process that cannot safely continue executing until the monitors state satisfied some Boolean condition
    - to awaken a delayed process when the condition becomes true
    - `cond cv;` a queue of delayed processes, initial empty, accessed indirectly by the operations below:
        - `empty(cv);` returns true if its empty
        - `wait(cv);` delay at the rare of cv´s queue, also releases lock
        - `signal(cv);`  awakens the process at the front of the queue
        - `wait` and `signal`: FIFO
- **signaling disciplines**:
    - signal-and-continue (sc): the signaler continues and the signaled process executes at some later time (non-preemptive)
    - signal-and-wait (sw): the signaler wait until some other later time and the signaled process executes now (preemptive)
- Syntax and semantics;

```jsx
monitor MyMonitor {
	//delcaration of permanent variables
	//initialization of statements
	//procedures

}

call MyMonitor.ProcedureName(arguments)
```

- Cond variables, only used inside monitors2
- Monitor semaphore

```jsx
monitor Semaphore {
	int s = 0; // s>=0, aka positive always
	cond pos;  // signaled when s>0
	
	procedure Psem() { // P operation 
		while (s==0) wait(pos);
	// SW: if(s==0) wait(pos);
		s = s-1;
	}
	procedure Vsem() { // V operation
		s = s+1;
		signal(pos);
	} 
}
```

- Additional Operations on Conditional Variables:
    - Priority wait: allows to excert more control over the order in which the delayed processes are queued and awakened.
        - `wait(cv, rank)` : processes are delayed on cv in ascending order of rank
    - `minrank(cv)` : return the delayed rank of a process to the front of the delay queue.
    - `singal_all(cv)` :
        - `while(!empty(cv)) signal(cv);`
        - unblocks all processes currently waiting on the given condition variable `cv` .
            - is called:  all the processes that are waiting on the condition variable `cv`
             are unblocked and enter the monitor's entry queue
- **The bounded buffers:**
- example:
```jsx
monitor BoundedBuffer {
	typeT buf[n];
	int front=0, rear=0, count=0;
	cond not_full, not_empty;

procedure deposit(typeT data) {
	while(count == n) wait(not_full);
	buf[rear] == data;
	rear = (rear+1) mod n;
	count++;
	signal(not_empty);
}

procedure fetch(typeT data) {
	while(count==0) wait(not_empty);
	result = buf[front];
	front = (front+1) mod n;
	count--;
	signal(not_full);
}
```

- **Readers / Writers: Broadcast signal:**
    - arbitration monitor
```jsx
request_read
release_read
request_write
release_write
nr (numbers of readers) initialy nr=0
nw (numbers of writers) initialy nw=0
```

- code example:
```jsx
monitor ReadersWriters {
	int nr = 0, nw = 0;
	cond OK_to_read;
	cond OK_to_write;
	
	procedure request_read() {
		while (nw > 0) wait(OK_to_read);
		nr = nr + 1;
	}

	procedure release_read() {
		nr = nr - 1;
		if (nr == 0) signal(OK_to_write);
	}

	procedure request_write() {
		while(nr > 0 || nw > 0) wait(OK_to_write);
		nw = nw + 1;
	}
	
	procedure release_write() {
		nw = nw - 1;
		signal(OK_to_write);
		signal_all(OK_to_read);
	}
}
```

- The sleeping barber: Rendezvous
    - client / server relationship example
    - `get_haircut`
    - `get_next_customer`
    - `finished_cut`
    - Rendezvous:
        - both parties must arrive before they can proceed.
            - the customer must arrive!
            - and the barber must be available!
        - incrementing counters to record processes
    - `c_inchair`
    - `c_leave`
    - `b_avail`
    - `b_busy`
    - `b_done`
    - `c_inchair` ≤ `c_leave` AND `b_avail` ≥ `b_busy` ≥ `b_done`

```jsx
monitor Barber {
	int barber=0, chair=0, open=0;
	cond barber_available;
	cond chair_occupied;
	cond door_open;
	cond customer_left;
	
	procedure get_haircut() {
		while (barber == 0) wait(barber_available);
		barber = barber - 1;
		chair = chair + 1;
		signal(chair_occupied);
		while (open == 0) wait(door_open);
		open = open - 1;
		signal(customer_left);
	
	procedure get_next_customer() {
		barber = barber + 1;
		signal(barber_available);
		while (chair == 0) wait(chair_occupied);
		chair = chair - 1;
	}

	procedure finished_cut() {
		open = open + 1;
		signal(door_open);
		while (open > 0) wait(customer_left);
	}

```

- PRACTICE
```jsx
monitor BoundedBuffer {

typeT buf[n]; 
int count=0, rear=0, front=0;
cond not_empty, not_full;

	procedure deposit() {
		while(count == n) wait(not_full); 
		buf[rear] == data;
		rear = (rear+1) mod n;
		count++
		signal(not_empty);
	}

	procedure fetch() {
		while() wait(not_empty);
		buf[front] == data;
		front = (front+1) mod n;
		count--;
		signal(not_full);
	
	}
```

- code
```jsx
monitor ReadersWriters_Controller {

   int nr = 0;

   int nw = 0;

   cond OK_to_read; // signalled when nw == 0
	 cond OK_to_write;

 

   procedure request_read() {
      while(nw>0) wait(OK_to_read);
      nr = nr + 1;
   }

   procedure release_read() {
      nr = nr - 1;
			if(nr == 0) signal(OK_to_read);
   }

   procedure request_write() {
			while(nr>0 || nw>0) wait(Ok_to_write);
      nw = nw + 1;
			
   }

   procedure release_write() {
      nw = nw - 1;
			signal(ok_to_read);
			signal(ok_to_write);
   }
}
```

```jsx
monitor BoundedBuffer {

	typeT buf[n];
	int rear = 0, front = 0, count = 0;
	cond not_full, not_empty;

	procedure deposit(TypeT data) {
		while(count == n) wait(not_full);
		buf[rear] = data;
		rear = (rear+1) mod n;
		count++;
		signal(not_empty);
	}

	procedure fetch(TypeT result) {
		while(count == 0) wait(not_empty);
		data = buf[front];
		front = (front+1) mod n;
		count--;
		signal(not_full);
	}
```

```jsx
monitor BoundedBuffer {

	int count=0, front=0, rear=0;
	typeT buf[n];
	cond not_full, not_empty;

	procedure deposit(TypeT data) {
		while(count == n) wait(not_full);
		buf[rear] == data;
		rear = (rear+1) mod n;
		count++;
		signal(not_empty);
	}

	procedure fetch(TypeT result) {
		while(count == 0) wait(not_empty);
		result = buf[front];
		front = (front+1) mod n
		count--;
		signal(not_full);
	}

}
```