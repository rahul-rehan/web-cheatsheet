## 1. What is the purpose of async and await in JavaScript?

- `async` and `await` simplify working with Promises by allowing asynchronous code to be written in a synchronous-looking style.
- They improve readability and maintainability by avoiding deeply nested `.then()` chains.
- `async` marks a function to always return a Promise.
- `await` pauses the execution of an `async` function until the awaited Promise settles, then resumes with the resolved value.

## 2. How do you define an async function?

- Use the `async` keyword before the function declaration or expression.  
- Example:  
  ```js
  async function fetchData() {
    // asynchronous code here
  }

  // Or with arrow function:
  const fetchData = async () => {
    // async code here
  };
  ```
## 3. What does an async function return?

- An `async` function always returns a **Promise**.  
- If you explicitly return a value inside an `async` function, it is automatically wrapped in a resolved Promise.  
- If an error is thrown inside the `async` function, the returned Promise is rejected with that error.  

### Example:
```js
async function example() {
  return 42;
}

example().then(value => console.log(value)); // Logs: 42
```
## 4. What is the effect of using the `await` keyword inside an async function?

- `await` pauses the execution of the async function until the Promise it waits for settles (either resolves or rejects).  
- Once the Promise resolves, `await` returns the resolved value, allowing you to write asynchronous code in a synchronous style.  
- If the awaited Promise rejects, an error is thrown which can be caught using `try/catch` inside the async function.

## 5. Can you use `await` outside an async function? What happens if you do?

- You **cannot** use `await` outside of an async function in regular JavaScript code; doing so will result in a syntax error.  
- However, in modern JavaScript environments like top-level modules or recent Node.js versions, **top-level await** is supported, allowing `await` to be used at the module's top scope.

## 6. Provide a simple example using async and await to fetch data.

```js
async function fetchUser() {
  try {
    const response = await fetch('https://jsonplaceholder.typicode.com/users/1');
    const user = await response.json();
    console.log(user);
  } catch (error) {
    console.error('Error fetching user:', error);
  }
}

fetchUser();
```