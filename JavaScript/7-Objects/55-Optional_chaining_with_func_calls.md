## 1. How do you safely call a function using the optional chaining operator?

You can safely call a function that might be `undefined` or `null` by using the optional chaining operator `?.` before the parentheses. For example:

```javascript
obj.someFunction?.();
```
This calls `someFunction` only if it exists; otherwise, it returns `undefined` without throwing an error.
## 2. What is the difference between `fn?.()` and `fn()`?

- `fn()` calls the function `fn` directly. If `fn` is `undefined` or `null`, it throws a runtime error.
- `fn?.()` calls the function only if `fn` is defined (not `null` or `undefined`). If `fn` is `undefined` or `null`, it returns `undefined` without throwing an error.a

## 3. What happens if you call a function that may be undefined using `?.()`?

If you call a possibly undefined function using the optional chaining call syntax (`fn?.()`):

- The function will be invoked if it exists.
- If the function is `undefined` or `null`, the expression safely returns `undefined` instead of throwing an error.
## 4. Can optional chaining be used to call a method from an object that may be null or undefined?

Yes, optional chaining can be used to safely call a method on an object that might be `null` or `undefined`. This prevents runtime errors by only calling the method if the object and method both exist.

## 5. Provide an example of optional chaining used on a method within a nested object.

```javascript
const user = {
  profile: {
    greet() {
      console.log("Hello!");
    }
  }
};

// Safely call greet() only if profile and greet exist
user.profile?.greet?.(); // Output: "Hello!"

const userWithoutProfile = {};

// This call won't throw an error; it will return undefined
userWithoutProfile.profile?.greet?.();
```

## Best Practices and Limitations
## 1. What types of values short-circuit optional chaining (null or undefined, or both)?

Optional chaining short-circuits only if the value before `?.` is **`null` or `undefined`**. If the value is anything else (including `false`, `0`, or an empty string), the chaining proceeds normally.

## 2. Can optional chaining be used on the left-hand side of an assignment?

No, optional chaining **cannot** be used on the left-hand side of an assignment because it does not return a valid reference that can be assigned to.

For example, this will cause a syntax error:

```javascript
obj?.prop = 42; // SyntaxError
```
## 3. Is optional chaining supported in all browsers? How can you handle compatibility?

Optional chaining is supported in most modern browsers but **not in some older browsers** (such as Internet Explorer).

#### How to handle compatibility:
- **Use a transpiler** like [Babel](https://babeljs.io/) to convert optional chaining syntax into equivalent ES5-compatible code.
- **Integrate polyfills** or build tools (like Webpack with Babel) in your development workflow to ensure your code runs correctly in older environments.
## 4. What are potential misuse or readability concerns when overusing optional chaining?

- **Overuse leads to unclear logic**: Relying heavily on optional chaining may hide bugs or poor data modeling by silently returning `undefined` rather than failing fast.
- **Hides underlying issues**: It can obscure the need to properly validate or initialize data structures.
- **Chained ?. becomes unreadable**: Excessive stacking (e.g., `obj?.a?.b?.c?.d`) can reduce code clarity and make debugging harder.

## 5. In what situations should you avoid using optional chaining?

- **When the property must exist**: If a property or method is required for proper program logic, failing silently with `undefined` can cause unintended consequences.
- **During critical assignments**: Optional chaining cannot be used on the left-hand side of assignments, and attempting to do so results in a syntax error.
- **When debugging data issues**: Using optional chaining might mask the root cause of `undefined` values, making it harder to trace bugs.

Instead of using optional chaining everywhere, it's often better to validate objects explicitly or use default values intentionally.
