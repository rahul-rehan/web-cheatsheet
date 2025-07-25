## 1. What are common use cases of generators in JavaScript?

- **Lazy evaluation**: Generate values on demand without computing them all upfront.
- **Implementing custom iterators**: Provide iterable behavior for objects.
- **Asynchronous programming**: Simplify async flows (especially before async/await).
- **State machines**: Manage state transitions with pause/resume.
- **Infinite sequences**: Create infinite streams like counters or random numbers.
- **Complex control flows**: Pause and resume execution at specific points.

## 2. How can generators be used for lazy evaluation?

Generators produce values only when requested via `.next()`, which means they compute each value lazily rather than all at once. This saves memory and CPU by avoiding unnecessary calculations until the value is actually needed.

## 3. How do generators help in implementing custom iterators?

Generators automatically implement the iterator protocol. When you define a generator function, calling it returns an iterator object with a `.next()` method. This simplifies creating custom iterable objects without manually writing the iterator interface methods.
## 4. What are the benefits of using generators over regular functions?

- **Pause and resume execution:** Generators can pause their execution at each `yield` and resume later, unlike regular functions which run to completion.
- **Lazy evaluation:** They produce values on demand rather than computing everything upfront, improving performance and memory usage.
- **Simplified iterators:** Generators automatically implement the iterator protocol, reducing boilerplate code.
- **Better control flow:** They allow complex control flow management, such as producing sequences or handling asynchronous tasks more intuitively.
- **Maintain internal state:** Generators preserve their context between yields, enabling easy stateful computations.

## 5. How can generators be used to model asynchronous workflows (before async/await)?

Before `async/await`, generators combined with libraries like `co` or custom runners were used to write asynchronous code that looks synchronous. The generator yields Promises, and a runner function automatically resumes the generator when each Promise resolves, enabling cleaner, linear async code flow without deeply nested callbacks or explicit `.then()` chains.
