## 1. Which built-in JavaScript types are iterable by default?

The following built-in JavaScript types are iterable by default:

- **Arrays**
- **Strings**
- **Maps**
- **Sets**
- **Typed Arrays** (e.g., `Uint8Array`, `Float32Array`)
- **arguments object**
- **NodeLists** (in modern browsers)

These types implement the `Symbol.iterator` method, allowing them to be used with `for...of` loops, spread syntax (`...`), and other iteration constructs.

## 2. How do you access the default iterator of an iterable object?

You can access the default iterator of an iterable object using the `Symbol.iterator` property:

```js
const array = [1, 2, 3];
const iterator = array[Symbol.iterator]();

console.log(iterator.next()); // { value: 1, done: false }
```
## 3. What is the role of the `Symbol.iterator` method?

The `Symbol.iterator` method defines the default **iterator function** for an object. When an object has a `[Symbol.iterator]()` method, it is considered **iterable**. This method must return an **iterator object** that implements the `next()` method.

The presence of `Symbol.iterator` allows the object to be used in:

- `for...of` loops
- spread syntax (`[...iterable]`)
- destructuring (`const [a, b] = iterable`)
- `Array.from(iterable)`
- other constructs that expect iterable objects

#### Example:

```js
const myIterable = {
  *[Symbol.iterator]() {
    yield 1;
    yield 2;
    yield 3;
  }
};

for (const value of myIterable) {
  console.log(value); // Outputs: 1, 2, 3
}
```
## 4. Example: Using the Iterator of a String

```js
const str = "hello";
const iterator = str[Symbol.iterator]();

console.log(iterator.next()); // { value: 'h', done: false }
console.log(iterator.next()); // { value: 'e', done: false }
console.log(iterator.next()); // { value: 'l', done: false }
console.log(iterator.next()); // { value: 'l', done: false }
console.log(iterator.next()); // { value: 'o', done: false }
console.log(iterator.next()); // { value: undefined, done: true }
```
## 5. Example: Using the Iterator of an Array
```js
Copy
Edit
const arr = [10, 20, 30];
const iterator = arr[Symbol.iterator]();

console.log(iterator.next()); // { value: 10, done: false }
console.log(iterator.next()); // { value: 20, done: false }
console.log(iterator.next()); // { value: 30, done: false }
console.log(iterator.next()); // { value: undefined, done: true }
```
These examples show how you can manually access and iterate through a string or array using their default iterators.
## 6. How does `for...of` work internally with an iterator?

The `for...of` loop works by calling the `[Symbol.iterator]()` method on an iterable object to obtain its iterator. Then it repeatedly calls the iterator’s `next()` method to retrieve values until `done` is `true`.

#### Example:

```js
const arr = [1, 2, 3];
const iterator = arr[Symbol.iterator]();

let result = iterator.next();
while (!result.done) {
  console.log(result.value);
  result = iterator.next();
}
```
This is essentially what `for...of` does behind the scenes:

```js
for (const value of arr) {
  console.log(value);
}
```
## 7. What is the difference between `for...in` and `for...of` loops?

| Feature         | `for...in`                                | `for...of`                                 |
|----------------|--------------------------------------------|---------------------------------------------|
| Iterates over  | **Enumerable property keys (names)**       | **Iterable values**                         |
| Works on       | Objects, arrays (as objects)               | Arrays, strings, maps, sets, etc. (iterables) |
| Use case       | Enumerating object keys                    | Iterating through values in a collection    |
| Output         | Property names (as strings)                | Actual element values                       |
| Suitable for   | Plain objects                              | Arrays, strings, collections                |

#### Example:

```js
const arr = ['a', 'b', 'c'];

for (const key in arr) {
  console.log(key); // "0", "1", "2" — property names
}

for (const value of arr) {
  console.log(value); // "a", "b", "c" — element values
}
```