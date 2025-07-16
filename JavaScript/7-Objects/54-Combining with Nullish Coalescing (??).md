## 1. What is the nullish coalescing operator (??) in JavaScript?

The nullish coalescing operator `??` returns the right-hand operand when the left-hand operand is `null` or `undefined`. It is used to provide default values only for `null` or `undefined`, unlike the logical OR (`||`) operator which also treats falsy values like `0` or `''` as defaults.

## 2. How do optional chaining and nullish coalescing work together?

Optional chaining safely accesses nested properties, returning `undefined` if any part is missing. When combined with `??`, you can provide a fallback value if the optional chaining results in `undefined` or `null`.

## 3. Provide an example of using optional chaining with `??` to provide fallback values.

```javascript
const user = {
  profile: {
    theme: null
  }
};

const theme = user?.profile?.theme ?? 'default-theme';

console.log(theme); // Output: "default-theme"
```
In this example, `user?.profile?.theme` evaluates to `null`, so the nullish coalescing operator returns the fallback `'default-theme'`.
## 4. Why is `??` preferred over `||`?

The nullish coalescing operator `??` is preferred over the logical OR `||` when you want to provide a fallback value **only** if the left operand is `null` or `undefined`. Unlike `||`, which treats all *falsy* values (such as `0`, `''`, `false`) as triggering the fallback, `??` allows these falsy values to pass through without being replaced.

For example:

```javascript
const count = 0;
console.log(count || 10);  // Outputs: 10 (because 0 is falsy)
console.log(count ?? 10);  // Outputs: 0  (because 0 is not null or undefined)
```
## 5. What would be the result of user?.info?.email ?? "Not provided" if email is null?
If `email` is explicitly `null`, then

```javascript
user?.info?.email ?? "Not provided"
```
will evaluate to `"Not provided"` because `??` returns the right-hand side when the left-hand side is `null` or `undefined`.