## 1. How does a generator pause and resume execution?

A generator pauses execution whenever it encounters a `yield` expression, returning the yielded value. Execution resumes from the paused point when the `.next()` method is called again on the generator.

## 2. Can you pass a value back into a generator with `next()`? How?

Yes. You can pass a value as an argument to the `.next(value)` call, which becomes the result of the current `yield` expression inside the generator. This allows two-way communication between the generator and the caller.

Example:

```javascript
function* gen() {
  const received = yield 'First yield';
  console.log('Received:', received);
}

const iterator = gen();
console.log(iterator.next());           // { value: 'First yield', done: false }
console.log(iterator.next('Hello'));    // Logs: Received: Hello
                                       // { value: undefined, done: true }
```
## 3. What is the effect of calling `.return()` on a generator?

Calling `.return(value)` immediately terminates the generator and returns the specified `value`. It sets the generator’s `done` property to `true` and returns an object in the form `{ value, done: true }`, no matter where the generator currently is in its execution.

Example:

```javascript
function* gen() {
  yield 1;
  yield 2;
  yield 3;
}

const iterator = gen();
console.log(iterator.next());                 // { value: 1, done: false }
console.log(iterator.return('Stopped early')); // { value: 'Stopped early', done: true }
console.log(iterator.next());                 // { value: undefined, done: true }
```
## 4. What is the effect of calling `.throw()` on a generator?

Calling `.throw(error)` on a generator injects an exception at the point where the generator is currently paused (at a `yield` expression). This causes the generator to throw the specified error inside its execution context, which can be caught and handled using `try...catch` blocks within the generator function. If the error is not caught inside the generator, it propagates outside and terminates the generator.

## 5. Example of handling errors inside a generator using `try...catch`

```javascript
function* gen() {
  try {
    yield 1;
    yield 2;
  } catch (e) {
    console.log('Caught inside generator:', e.message);
  }
  yield 3;
}

const iterator = gen();
console.log(iterator.next());       // { value: 1, done: false }
console.log(iterator.throw(new Error('Something went wrong')));  
// Logs: Caught inside generator: Something went wrong
// Returns: { value: 3, done: false }
console.log(iterator.next());       // { value: undefined, done: true }
```