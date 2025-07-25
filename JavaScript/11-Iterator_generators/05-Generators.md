## 1. What is a generator function in JavaScript?

A generator function is a special type of function that can pause its execution and later resume from where it left off. It allows producing a sequence of values over time, enabling lazy evaluation and more controlled iteration.

## 2. How do you define a generator function?

A generator function is defined using the `function*` syntax. Inside the function, the `yield` keyword is used to pause the function and output a value.

## 3. What symbol is used to declare a generator function?

The asterisk (`*`) symbol after the `function` keyword is used to declare a generator function.

Example:

```javascript
function* myGenerator() {
  yield 1;
  yield 2;
  yield 3;
}
```
## 4. What does a generator function return when called?

When called, a generator function does **not** execute its body immediately. Instead, it returns a **generator object** (an iterator) that can be used to control the execution and retrieve values one at a time.

## 5. What is the purpose of the `yield` keyword?

The `yield` keyword pauses the execution of the generator function and returns a value to the caller. Execution can later be resumed from this point when `.next()` is called on the generator object.

## 6. How does `yield` differ from `return` in a regular function?

- `yield` **pauses** the generator function and allows it to be resumed later, producing multiple values over time.
- `return` in a regular function **immediately ends** the function execution and returns a single value.
- In a generator, `return` also ends the generator, but `yield` allows multiple pauses and resumptions.
## 7. Example: Generator that yields three values

```javascript
function* simpleGenerator() {
  yield 'First';
  yield 'Second';
  yield 'Third';
}

const gen = simpleGenerator();

console.log(gen.next()); // { value: 'First', done: false }
console.log(gen.next()); // { value: 'Second', done: false }
console.log(gen.next()); // { value: 'Third', done: false }
console.log(gen.next()); // { value: undefined, done: true }
```
## 8. What does the `.next()` method return when called on a generator?

The `.next()` method returns an object with two properties:
- `value`: The current yielded value from the generator.
- `done`: A boolean indicating whether the generator has completed (`true` if finished, `false` otherwise).

## 9. What happens when a generator function finishes execution?

When a generator function finishes execution, calling `.next()` returns an object with:
- `value: undefined`
- `done: true`

This signals that the generator is complete and there are no more values to yield.

## 10. How can you use `for...of` to iterate over a generator?

You can use a `for...of` loop directly on a generator object to automatically iterate over all yielded values until the generator is done. Example:

```javascript
function* simpleGenerator() {
  yield 'A';
  yield 'B';
  yield 'C';
}

for (const value of simpleGenerator()) {
  console.log(value);
}
// Output:
// A
// B
// C
```
