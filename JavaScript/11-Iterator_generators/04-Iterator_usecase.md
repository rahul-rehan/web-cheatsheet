## 1. What are some practical use cases for iterators?

- **Custom data traversal:** Create your own iteration logic for complex data structures.
- **Lazy data processing:** Process data on-demand without loading everything into memory.
- **Implementing streams or pipelines:** Control flow of data processing in steps.
- **Infinite sequences:** Generate sequences like Fibonacci numbers or timestamps without precomputing.
- **Interfacing with APIs:** Use iterators to provide uniform access to paginated or chunked data.

## 2. How are iterators useful in implementing lazy evaluation?

Iterators produce values **one at a time** only when requested via `next()`. This on-demand production means:

- Computation happens **only as needed**, saving memory and CPU.
- You avoid generating all values upfront, which is efficient for large or infinite data sets.
- Enables building **lazy sequences** where elements are computed progressively.

## 3. How do iterators relate to generators in JavaScript?

- **Generators are a special type of iterator.**
- Defined with `function*` syntax, generators automatically implement the iterator protocol.
- Generators use `yield` to pause and resume execution, producing values lazily.
- They simplify creating iterators by handling state and `next()` calls internally.
- Every generator is an iterator, but not every iterator is a generator.
## 4. How do you handle completion (`done: true`) inside an iterator loop?

When an iterator's `next()` method returns an object with `done: true`, it signals that the iteration is complete. You typically handle this by stopping the loop or ending the data processing. For example, in a manual loop:

```js
let result = iterator.next();
while (!result.done) {
  console.log(result.value);
  result = iterator.next();
}
// Once done is true, exit the loop
```
In `for...of` loops, this is handled automatically.
## 5. What happens if `next()` is called after the iterator is complete?

Calling `next()` after the iterator is complete (i.e., after `done: true` has been returned) will keep returning:

```js
{ value: undefined, done: true }
```
The iterator remains in the "completed" state and produces no more values.
## 6. How do iterators improve control over data processing in complex applications?

Iterators provide fine-grained control by:

- Enabling **lazy evaluation**, so data is processed only as needed.
- Allowing **pausing and resuming** iteration, which is useful for asynchronous or large datasets.
- Supporting **custom traversal logic** for complex data structures.
- Improving **memory efficiency** by not loading entire datasets upfront.
- Facilitating **modular and composable** data processing workflows.
