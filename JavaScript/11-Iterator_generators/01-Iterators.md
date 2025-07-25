## 1. What is an iterator in JavaScript?

An **iterator** in JavaScript is an object that provides a standardized way to produce a sequence of values, one at a time. It adheres to the **iterator protocol**, allowing it to be used in constructs like `for...of` loops or spread syntax.

## 2. What protocol must an object follow to be considered an iterator?

To be considered an iterator, an object must implement the **iterator protocol**, which requires it to have a `next()` method. This method must return an object with two properties:

- `value`: the next value in the sequence.
- `done`: a boolean indicating whether the sequence is complete (`true`) or not (`false`).

## 3. What are the two main components of an iterator object?

1. **The `next()` method**  
   - Called to get the next value in the sequence.
   - Returns an object with the shape `{ value: any, done: boolean }`.

2. **The result object returned by `next()`**  
   - Contains:
     - `value`: the current item from the iterator.
     - `done`: indicates whether the iteration is complete.
## 4. What is the purpose of the `next()` method in an iterator?

The `next()` method is used to retrieve the next item from a sequence in an iterator. Each call to `next()` returns an object that tells whether the iteration is finished and, if not, what the next value is.

## 5. What does the object returned by `next()` contain?

The object returned by `next()` contains two properties:

- `value`: The current value yielded by the iterator.
- `done`: A boolean indicating whether the iterator has completed (`true`) or should continue (`false`).

## 6. Provide a basic example of a custom iterator in JavaScript.

```js
function createCounter(limit) {
  let count = 0;
  return {
    next: function () {
      if (count < limit) {
        return { value: count++, done: false };
      } else {
        return { value: undefined, done: true };
      }
    }
  };
}

const counter = createCounter(3);
console.log(counter.next()); // { value: 0, done: false }
console.log(counter.next()); // { value: 1, done: false }
console.log(counter.next()); // { value: 2, done: false }
console.log(counter.next()); // { value: undefined, done: true }
```
## 7. What is the difference between an iterable and an iterator?

- **Iterable**:  
  An **iterable** is any object that implements the **iterable protocol**, meaning it has a method with the key `[Symbol.iterator]` that returns an **iterator**. Common iterables include arrays, strings, sets, and maps.

- **Iterator**:  
  An **iterator** is an object that implements the **iterator protocol**, meaning it has a `next()` method that returns an object with `value` and `done` properties.

---

### Key Differences:

| Feature         | Iterable                                | Iterator                                  |
|----------------|------------------------------------------|--------------------------------------------|
| Protocol        | Must implement `[Symbol.iterator]()`    | Must implement `.next()`                   |
| Purpose         | Can be used in `for...of`, spread, etc. | Produces values one at a time              |
| Examples        | Arrays, Strings, Sets, Maps             | Result of calling `[Symbol.iterator]()`    |
| Reusable        | Usually reusable                        | Usually not reusable after done is `true`  |

---

### Example:

```js
const iterable = [10, 20, 30];         // An iterable
const iterator = iterable[Symbol.iterator](); // An iterator

console.log(iterator.next()); // { value: 10, done: false }
console.log(iterator.next()); // { value: 20, done: false }
console.log(iterator.next()); // { value: 30, done: false }
console.log(iterator.next()); // { value: undefined, done: true }
```