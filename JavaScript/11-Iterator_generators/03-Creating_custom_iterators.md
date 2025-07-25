## 1. How do you define a custom iterable object?

To define a custom iterable object, you must implement the `[Symbol.iterator]()` method on the object. This method should return an iterator—an object with a `next()` method that returns values in the form of `{ value, done }`.

## 2. What is the role of `Symbol.iterator` when creating custom iterables?

`Symbol.iterator` is a well-known symbol that specifies the default iterator for an object. When a `for...of` loop or any other construct expects an iterable, it looks for the `[Symbol.iterator]()` method on the object.

This method:

- Must return an iterator object.
- Should conform to the iterator protocol by having a `next()` method that returns an object with `value` and `done` properties.

## 3. How do you make a plain object iterable using a custom iterator?

You can make a plain object iterable by adding a `[Symbol.iterator]()` method to it that returns an iterator.

#### Example:

```js
const customIterable = {
  data: [10, 20, 30],
  [Symbol.iterator]() {
    let index = 0;
    const values = this.data;
    return {
      next() {
        if (index < values.length) {
          return { value: values[index++], done: false };
        } else {
          return { value: undefined, done: true };
        }
      }
    };
  }
};

for (const val of customIterable) {
  console.log(val); // 10, 20, 30
}
```
This approach allows a plain object to work with `for...of`, spread syntax, and other iterable-aware functions.
## 4. Provide an example of an infinite iterator

An infinite iterator generates an endless sequence of values. Here's an example that yields natural numbers forever:

```js
const infiniteIterator = {
  [Symbol.iterator]() {
    let count = 0;
    return {
      next() {
        return { value: count++, done: false };
      }
    };
  }
};

const iterator = infiniteIterator[Symbol.iterator]();
console.log(iterator.next()); // { value: 0, done: false }
console.log(iterator.next()); // { value: 1, done: false }
// ...and so on (never ends)
```
Be cautious when using infinite iterators in loops; they must include a manual break condition to avoid infinite execution.
## 5. Can an iterator be paused and resumed manually using `next()`?

Yes, iterators in JavaScript are **pull-based**, which means you control their execution by calling the `next()` method explicitly. This allows you to pause and resume iteration at any time.

#### Example:

```js
const arr = [1, 2, 3];
const iterator = arr[Symbol.iterator]();

console.log(iterator.next()); // { value: 1, done: false }
// paused here...
console.log(iterator.next()); // { value: 2, done: false }
// resumed again...
console.log(iterator.next()); // { value: 3, done: false }
```
Each call to `next()` advances the iterator by one step, giving you fine-grained control over the iteration process.