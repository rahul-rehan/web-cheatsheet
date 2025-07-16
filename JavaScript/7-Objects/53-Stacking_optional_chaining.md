## 1. What does "stacking" optional chaining mean in JavaScript?

"Stacking" optional chaining refers to using multiple `?.` operators in a chain to safely access deeply nested properties or methods without risking runtime errors if any intermediate value is `null` or `undefined`.

## 2. Provide an example of safely accessing a deeply nested property using stacked optional chaining.

```javascript
const user = {
  profile: {
    address: {
      street: "123 Main St"
    }
  }
};

// Safely accessing street with stacked optional chaining
const street = user?.profile?.address?.street;

console.log(street); // Output: "123 Main St"
```
If any intermediate property like `profile` or `address` is `null` or `undefined`, the expression returns `undefined` instead of throwing an error.
## 3. What will `user?.profile?.settings?.theme` return if `settings` is undefined?

It will return `undefined` without throwing an error, because optional chaining stops evaluation when it encounters `undefined`.

## 4. Is optional chaining allowed with arrays and their indexes? Show an example.

Yes, optional chaining can be used to safely access array elements by index.

```javascript
const arr = [10, 20, 30];
const value = arr?.[2];  // 30
const missing = arr?.[5]; // undefined (no error)
```
## 5. Can optional chaining be used in a `for` or `if` condition?

Yes, optional chaining can be used within `if` or `for` conditions to safely check for property existence before proceeding.

```javascript
if (user?.profile?.isActive) {
  // execute code only if user.profile.isActive exists and is truthy
}

for (const item of user?.items ?? []) {
  // safely iterate only if user.items exists; otherwise iterate empty array
}
```
