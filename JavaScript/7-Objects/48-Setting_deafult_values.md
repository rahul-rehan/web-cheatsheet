## 1. How do you assign a default value during object destructuring?

You assign a default value by using the assignment operator `=` after the property name inside the destructuring pattern.

## 2. What is the default value used for in destructuring syntax?

The default value is used when the property being destructured is `undefined` or missing from the object, allowing the variable to have a fallback value instead of `undefined`.

## 3. Provide an example where a missing property uses a default value.

```javascript
const user = {
  name: 'John'
};

const { age = 30 } = user;

console.log(age); // 30
```
In this example, since the `age` property does not exist in `user`, the variable `age` gets assigned the default value `30`.
## 4. What happens if the property exists but is undefined? Does the default still apply?

- Yes, if the property exists but its value is `undefined`, the default value **will** be applied during destructuring.
- Default values are used when the property value is `undefined`, not just when the property is missing.

## 5. Can you combine renaming and default values together in destructuring?

Yes, you can combine both by using the syntax:

```javascript
const { propertyName: newVariableName = defaultValue } = object;
```
#### Example:
```javascript
const person = { name: undefined };

const { name: firstName = 'Anonymous' } = person;

console.log(firstName); // Anonymous
```