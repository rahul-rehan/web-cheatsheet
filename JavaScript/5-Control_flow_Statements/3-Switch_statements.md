## 1. What is the syntax of a switch statement in JavaScript?

The `switch` statement allows you to execute different blocks of code based on the value of an expression.

```javascript
switch (expression) {
  case value1:
    // code to execute if expression === value1
    break;
  case value2:
    // code to execute if expression === value2
    break;
  // ... more cases ...
  default:
    // code to execute if none of the above cases match
}
```
- **expression**: The value to compare.

- **case value**: Possible values to match against the expression.

- **default**: Optional block executed if no cases match.
## 2. How does `switch` compare case values (strictly or loosely)?

The `switch` statement uses **strict comparison (`===`)** to compare the `expression` with each `case` value. This means both the value and the type must be the same for a match.
## 3. What is the role of the `break` statement in a `switch` block?

- The `break` statement **terminates the switch block** after executing a matched case.
- Without `break`, execution will "fall through" to subsequent cases, running their code even if their cases do not match.
- This can lead to unexpected behavior unless fall-through is intentional.

#### Example:
```javascript
switch (day) {
  case 1:
    console.log("Monday");
    break;  // stops execution here
  case 2:
    console.log("Tuesday");
    break;
  default:
    console.log("Another day");
}
```
## 4. What happens if `break` is omitted in a switch case?

If a `break` statement is omitted in a `switch` case, **execution "falls through" to the next case**, meaning the code in the next case(s) will run regardless of whether their case matches the expression. This continues until a `break` is encountered or the switch block ends.

#### Example of fall-through:
```javascript
let day = 2;

switch (day) {
  case 1:
    console.log("Monday");
  case 2:
    console.log("Tuesday");
  case 3:
    console.log("Wednesday");
    break;
  default:
    console.log("Another day");
}
```
### Output:
```mathematica
Tuesday
Wednesday
```
Since there is no `break` after `case 2,` the code falls through and executes `case 3` as well.
## 5. Can multiple case labels lead to the same block? Example?

Yes, multiple `case` labels can share the same block of code by stacking them without a `break` in between.

#### Example:
```javascript
let fruit = "apple";

switch (fruit) {
  case "apple":
  case "banana":
  case "orange":
    console.log("This is a common fruit.");
    break;
  case "kiwi":
    console.log("This is a kiwi.");
    break;
  default:
    console.log("Unknown fruit.");
}
```
In this example, `"apple"`, `"banana"`, and `"orange"` all lead to the same block printing `"This is a common fruit."`.
## 6. What is the purpose of the `default` case in a switch statement?

The `default` case in a `switch` statement serves as a **fallback**. It is executed when none of the specified `case` values match the `switch` expression. This ensures that the code can handle unexpected or unmatched values gracefully.

---

## 7. Can a switch statement be used with non-numeric values like strings?

Yes, a `switch` statement in JavaScript can be used with **non-numeric values**, including **strings**, **booleans**, and even other types. The `switch` compares the expression with each case using **strict equality (`===`)**, so the value and type must match exactly.

#### Example with strings:
```javascript
let color = "red";

switch (color) {
  case "red":
    console.log("Stop");
    break;
  case "green":
    console.log("Go");
    break;
  default:
    console.log("Unknown color");
}
```