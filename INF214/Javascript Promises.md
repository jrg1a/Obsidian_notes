JavaScript Promises are an essential feature introduced in ECMAScript 6 (ES6) to handle asynchronous operations in a more organized and manageable way. They provide a structured approach to dealing with asynchronous tasks and help avoid callback hell, making code more readable and maintainable.

Promises represent the eventual completion (or failure) of an asynchronous operation and allow you to handle the result (fulfilment) or error (rejection) of that operation using a chain of methods. The primary purpose of Promises is to simplify asynchronous programming and provide a standardised way to handle asynchronous tasks.

## How Promises Work
Here's how Promises in JavaScript work:
1.  Creating a Promise: You can create a Promise using the `new Promise()` constructor, which takes a function with two arguments: `resolve` and `reject`. Inside this function, you write the asynchronous code that eventually calls `resolve` when the operation succeeds or `reject` when it fails.
2.  States of a Promise: A Promise can be in one of three states:
    -   Pending: The initial state, before the asynchronous operation is completed.
    -   Fulfilled: The operation completed successfully, and the Promise is resolved with a value.
    -   Rejected: The operation failed, and the Promise is rejected with a reason (error).
3.  Chaining Promise Methods: Promises provide several methods that allow you to chain operations together. The most commonly used methods are:
    -   `then()`: Registers a callback to handle the fulfillment of the Promise.
    -   `catch()`: Registers a callback to handle the rejection of the Promise.
    -   `finally()`: Registers a callback to be executed regardless of the Promise's outcome.
4.  Handling Asynchronous Tasks: With Promises, you can perform multiple asynchronous tasks in sequence or parallel using Promise chaining or Promise composition techniques. This allows you to control the flow of asynchronous operations and handle the results in a more structured manner.
5.  Error Handling: Promises provide a centralized error handling mechanism. If an error occurs in any part of the Promise chain and is not explicitly handled, it will propagate down the chain until a `catch()` method is encountered. This makes error handling more consistent and avoids the need for excessive [[Exception Handling#Using Try and Catch|try-catch blocks]].

Promises are widely used in JavaScript for handling asynchronous operations, such as making [[Application Layer#Overview of HTTP|HTTP requests]], reading/writing files, working with databases, and performing animations. They provide a cleaner and more readable alternative to callback-based asynchronous code.

With the introduction of Promises, JavaScript's concurrency model has significantly improved, enabling developers to write more maintainable, scalable, and efficient asynchronous code. Promises have become an integral part of modern JavaScript development and have laid the foundation for even more advanced features like async/await, which further enhance the readability and simplicity of asynchronous programming.

## Promises in JavaScript (examples):
We will now take a look at some basic examples of Promises in JavaScript, and how they are resolved and implemented.
- a promise that is immediately resolved:
```jsx
const myPromise = Promise.resolve('hello world');
myPromise.then((value) => {
	console.log(value));
});
```
- a promise that is immediately rejected:
```jsx
const promise = Promise.reject('Promise rejected');
promise.catch((error) => {
	console.log(error);
});
```
- a promised chained by ‘then’ and ‘catch’:
```jsx
const promise1 = Promise.resolve(10);

promise1.then(value => {console.log(value);return value*2;})
.then(value => {console.log(value);return value*2;})
.then(value => {console.log(value);
    throw new Error('Something went wrong!');})
  .catch(error => {
    console.error(error);
  });
```
- a promise using Promise.all() to wait for multiple promises to resolve before continuing:
```jsx
const promise1 = Promise.resolve('Hello');
const promise2 = Promise.resolve('World');

Promise.all([promise1, promise2])
	.then(([result1, result2]) => {
		console.log(result1 + '' + result2);
		//output: 'Hello World'
  })
	.catch(error => {
		console.error(error);
	});
```
- a promise using Promise.race() to wait for the first of two promises to resolve before continuing:
```jsx
const promise1 = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('Promise 1 resolved!');
  }, 2000);
});

const promise2 = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('Promise 2 resolved!');
  }, 1000);
});

Promise.race([promise1, promise2])
  .then((result) => {
    console.log(result);
  })
  .catch((error) => {
    console.error(error);
  });
```
- Using the `async/await` syntax to handle promises in a more [[Message Passing#Synchronous message passing|synchronous-looking way]]. [ H A R D ]
```jsx
async function getUserData(userId) {
  try {
    const response = await fetch(`https://jsonplaceholder.typicode.com/users/${userId}`);
    const userData = await response.json();
    return userData;
  } catch (error) {
    console.error(`Error fetching user data: ${error}`);
    throw error;
  }
}

async function displayUserData(userId) {
  try {
    const userData = await getUserData(userId);
    console.log(`Name: ${userData.name}`);
    console.log(`Email: ${userData.email}`);
    console.log(`City: ${userData.address.city}`);
  } catch (error) {
    console.error(`Error displaying user data: ${error}`);
  }
}

displayUserData(1);
```
- easier example:
```jsx
function delay(ms) {
  return new Promise(resolve => setTimeout(resolve, ms));
}

async function example() {
  console.log("Starting...");
  await delay(1000);
  console.log("One second later...");
}

example();
```
- In this example, the `delay` function returns a Promise that resolves after a certain number of milliseconds. The `example` function uses `await` to wait for the `delay` Promise to resolve before logging a message to the console. When we call `example`, it logs "Starting..." immediately, then waits one second before logging "One second later...".
- Basic Promise Example:
```Java
const myPromise = new Promise((resolve, reject) => {
  // Simulating an asynchronous operation
  setTimeout(() => {
    const data = 'Promise resolved!';
    resolve(data);
    // To simulate an error, use: reject(new Error('Promise rejected!'));
  }, 2000);
});

myPromise
  .then((result) => {
    console.log(result); // Output: Promise resolved!
  })
  .catch((error) => {
    console.error(error); // Output: Promise rejected!
  });

```
- Promise Chaining:
```Java
function fetchUser() {
  return new Promise((resolve, reject) => {
    // Simulating an API call
    setTimeout(() => {
      const user = { id: 1, name: 'John Doe' };
      resolve(user);
    }, 2000);
  });
}

function fetchPosts(userId) {
  return new Promise((resolve, reject) => {
    // Simulating an API call
    setTimeout(() => {
      const posts = ['Post 1', 'Post 2', 'Post 3'];
      resolve(posts);
    }, 1500);
  });
}

fetchUser()
  .then((user) => {
    console.log(user); // Output: { id: 1, name: 'John Doe' }
    return fetchPosts(user.id);
  })
  .then((posts) => {
    console.log(posts); // Output: ['Post 1', 'Post 2', 'Post 3']
  })
  .catch((error) => {
    console.error(error);
  });

```
- ``Promise.all()`` - Parallel Execution:
```Java
const promise1 = Promise.resolve('Promise 1 resolved!');
const promise2 = new Promise((resolve) => {
  setTimeout(() => {
    resolve('Promise 2 resolved!');
  }, 2000);
});
const promise3 = fetch('https://api.example.com/data');

Promise.all([promise1, promise2, promise3])
  .then((results) => {
    console.log(results);
    // Output: ['Promise 1 resolved!', 'Promise 2 resolved!', response]
  })
  .catch((error) => {
    console.error(error);
  });

```
These examples demonstrate the basic usage of Promises, Promise chaining, and parallel execution using `Promise.all()`. Remember, Promises can be used with various asynchronous operations like fetching data from [[CRUD API|APIs]], reading/writing files, making database queries, etc.
