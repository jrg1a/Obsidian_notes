
> *`What is an generator? what does it do?`*

Generators are a useful programming construct that allows for the generation of a sequence of values on demand. They provide an efficient way to produce a stream of values without the need to generate and store them all at once, which can be beneficial for memory usage and performance.

Generators are typically implemented as functions or objects that can be iterated over. Each iteration yields a new value from the sequence. This enables a more efficient and lazy evaluation approach, where values are computed and generated only when needed, reducing unnecessary computations.

Generators are particularly useful in scenarios where you need to work with large or infinite sequences of data. By generating values on the fly, you can avoid the need to store all the data in memory, which can be impractical or even impossible in certain cases.

In multiprogramming and parallel programming, generators can be utilized to create concurrent and parallel workflows. By dividing the workload into smaller chunks and generating values in parallel, generators can improve the efficiency of processing large datasets or performing computationally intensive tasks.

Generators can be combined with other techniques such as coroutines or async/await patterns to enable asynchronous and non-blocking execution, further enhancing the performance and responsiveness of concurrent programs.

Overall, generators provide a powerful mechanism for managing sequences of data in multiprogramming and parallel programming. They allow for efficient and lazy evaluation of values, making it possible to work with large or infinite sequences without overwhelming system resources. By leveraging generators, developers can create more scalable and responsive applications in the context of multiprogramming and parallel programming.

- Calling a generator does not execute it, instead it will create a new iterator that we can request values from.
- after a generator has generated from a request it `**suspends**` its execution and `**waits**` for the next request.
- The generator works like a state machine!
    - suspended start
    - executing
    - suspended yield
    - completed
- Generator as a state machine as image:

![Skjermbilde.PNG](Skjermbilde%201.png)

- The states:
    - `suspended start`: the generator starts in this state, and noone of its code is executed.
    - `executing`:  the code of the generator is executed in this state. It starts either from the beginning or from where it last suspended. The generator moves to this state when the matching iterators `*next()*` method is called, and there exists code to be executed.
    - `suspended yield`:  during the execution a generator can reach a yield expression, it then creates a new `object` carrying the `return value`, yields it, and suspends its execution. The state of the generator is paused and is waiting to continiue its execution.
    - `completed`:  the generator runs into this state when either a `return statement` is made, or it runs out of code to execute. The generator is then moved into this state.
- code example:

```jsx
function *g() {
	yield 'A';
	yield 'B';
}

const p = g();
const r1 = p.next();
const r2 = p.next();
const r3 = p.next();
    ```

- `suspended start`  — *iterator.next()* —> `executing`  — *yield reached* —> `suspended yield` 
—> {*value: ‘A’, done: false*}, {*value: ‘B’, done: false*}—> *iterator.next()* —> `executing` —> 
—> *return reached or no more code* —> `completed`  {*value: undefined, done: true* }
- image of the process above:

![Skjermbilde1.PNG](Skjermbilde1.png)

- Tracking generators with execution contexts.

## Relations
Generators can be closely related to other subjects in concurrent programming, particularly those that involve handling and processing large datasets or performing computationally intensive tasks in parallel. Here are a few ways generators can link to other subjects:
- Parallel Processing: Generators can be used as a means to distribute and process data in parallel. By dividing the workload into smaller chunks and generating values concurrently, multiple threads or processes can work on different parts of the data simultaneously, effectively leveraging the power of parallel processing.
- Asynchronous Programming: Generators can be combined with asynchronous programming techniques, such as coroutines or async/await patterns, to enable non-blocking execution. By yielding values asynchronously, generators allow other parts of the program to continue executing while waiting for the next value to be generated. This can enhance responsiveness and enable efficient utilization of system resources.
- Stream Processing: Generators can serve as a source of data for stream processing frameworks or libraries. In stream processing, data is processed as a continuous stream rather than as discrete batches. Generators can provide a continuous supply of data that can be processed in a streaming fashion, enabling real-time data processing and analysis.
- Data Pipelines: Generators can be used as building blocks in data pipelines, where data flows through a series of processing stages. Each stage can be implemented as a generator that consumes input data, performs a transformation or computation, and produces output data. This allows for modular and reusable code that can be easily composed to construct complex data processing pipelines.
- Concurrency Control: Generators can play a role in managing concurrency and synchronization in concurrent programs. By carefully designing generators and controlling their execution, you can ensure thread safety and avoid race conditions when multiple threads or processes are accessing or modifying shared data.

In summary, generators in concurrent programming can be interconnected with various subjects such as parallel processing, asynchronous programming, stream processing, data pipelines, and concurrency control. They provide a flexible and efficient mechanism for managing and processing data in concurrent and parallel environments, enabling developers to build scalable and responsive applications.