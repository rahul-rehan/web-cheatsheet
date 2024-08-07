# Conditionals

### 1. Different Types of Conditional Statements in Java

Java provides several conditional statements to control the flow of execution based on certain conditions:

- **`if` Statement**: Executes a block of code if a specified condition is true.

  **Code Snippet**:
  ```java
  public class IfExample {
      public static void main(String[] args) {
          int number = 10;

          if (number > 0) {
              System.out.println("Number is positive.");
          }
      }
  }
  ```

- **`else if` Statement**: Used to specify a new condition to test if the previous `if` condition was false.

  **Code Snippet**:
  ```java
  public class ElseIfExample {
      public static void main(String[] args) {
          int number = -5;

          if (number > 0) {
              System.out.println("Number is positive.");
          } else if (number < 0) {
              System.out.println("Number is negative.");
          }
      }
  }
  ```

- **`else` Statement**: Executes a block of code if none of the preceding `if` or `else if` conditions were true.

  **Code Snippet**:
  ```java
  public class ElseExample {
      public static void main(String[] args) {
          int number = 0;

          if (number > 0) {
              System.out.println("Number is positive.");
          } else if (number < 0) {
              System.out.println("Number is negative.");
          } else {
              System.out.println("Number is zero.");
          }
      }
  }
  ```

### 2. Evaluating a Condition in an `if` Statement

In an `if` statement, a condition is evaluated to a boolean value (`true` or `false`). The block of code within the `if` statement executes only if the condition evaluates to `true`.

**Code Snippet**:
```java
public class IfConditionEvaluation {
    public static void main(String[] args) {
        int age = 18;

        if (age >= 18) { // Condition is evaluated
            System.out.println("You are an adult.");
        }
    }
}
```

### 3. Logical Operators Used with Conditionals

Java provides logical operators to combine multiple conditions:

- **AND (`&&`)**: Returns `true` if both conditions are true.
  ```java
  public class LogicalAnd {
      public static void main(String[] args) {
          int age = 25;
          boolean hasID = true;

          if (age >= 18 && hasID) {
              System.out.println("Access granted.");
          }
      }
  }
  ```

- **OR (`||`)**: Returns `true` if at least one of the conditions is true.
  ```java
  public class LogicalOr {
      public static void main(String[] args) {
          int age = 16;
          boolean hasPermission = true;

          if (age < 18 || hasPermission) {
              System.out.println("Access granted.");
          }
      }
  }
  ```

- **NOT (`!`)**: Reverses the logical state of its operand.
  ```java
  public class LogicalNot {
      public static void main(String[] args) {
          boolean isRegistered = false;

          if (!isRegistered) {
              System.out.println("Please register first.");
          }
      }
  }
  ```

### 4. What Happens If You Don't Have an `else` Statement After an `if` Statement?

If you don't have an `else` statement after an `if` statement, the program simply continues executing any subsequent code after the `if` block. The `else` block is optional and only executes when the `if` condition is `false`.

**Code Snippet**:
```java
public class NoElseExample {
    public static void main(String[] args) {
        int number = 10;

        if (number > 0) {
            System.out.println("Number is positive.");
        }

        System.out.println("This line always executes.");
    }
}
```

### 5. Program to Find the Largest of Two Numbers

**Code Snippet**:
```java
public class LargestOfTwo {
    public static void main(String[] args) {
        int num1 = 15;
        int num2 = 20;

        if (num1 > num2) {
            System.out.println("The largest number is: " + num1);
        } else {
            System.out.println("The largest number is: " + num2);
        }
    }
}
```

### 6. Program to Check If a Number is Even or Odd

**Code Snippet**:
```java
public class EvenOrOdd {
    public static void main(String[] args) {
        int number = 7;

        if (number % 2 == 0) {
            System.out.println("The number is even.");
        } else {
            System.out.println("The number is odd.");
        }
    }
}
```

### 7. Program to Determine the Grade of a Student Based on Their Marks

**Code Snippet**:
```java
public class GradeDetermination {
    public static void main(String[] args) {
        int marks = 85;

        if (marks >= 90) {
            System.out.println("Grade: A");
        } else if (marks >= 80) {
            System.out.println("Grade: B");
        } else if (marks >= 70) {
            System.out.println("Grade: C");
        } else if (marks >= 60) {
            System.out.println("Grade: D");
        } else {
            System.out.println("Grade: F");
        }
    }
}
```

### 8. Program to Check if a Year is a Leap Year

**Code Snippet**:
```java
public class LeapYearCheck {
    public static void main(String[] args) {
        int year = 2024;

        if ((year % 4 == 0 && year % 100 != 0) || (year % 400 == 0)) {
            System.out.println(year + " is a leap year.");
        } else {
            System.out.println(year + " is not a leap year.");
        }
    }
}
```

### 9. Difference Between an `if` Statement and a `switch` Statement

- **`if` Statement**:
  - Used for making decisions based on complex conditions.
  - Can handle ranges and multiple conditions using logical operators.
  - More flexible, allowing for different types of conditions.

  **Code Snippet**:
  ```java
  public class IfStatementExample {
      public static void main(String[] args) {
          int day = 2;

          if (day == 1) {
              System.out.println("Monday");
          } else if (day == 2) {
              System.out.println("Tuesday");
          } else {
              System.out.println("Weekend");
          }
      }
  }
  ```

- **`switch` Statement**:
  - Best suited for handling multiple specific values for a single variable.
  - More readable for many discrete cases and often used for selecting among several options.
  - Each `case` is compared with the `switch` expression.

  **Code Snippet**:
  ```java
  public class SwitchStatementExample {
      public static void main(String[] args) {
          int day = 2;

          switch (day) {
              case 1:
                  System.out.println("Monday");
                  break;
              case 2:
                  System.out.println("Tuesday");
                  break;
              default:
                  System.out.println("Weekend");
                  break;
          }
      }
  }
  ```

### 10. When to Use `else if` Instead of Nested `if` Statements

**`else if`** statements are generally preferred over nested `if` statements when you have multiple mutually exclusive conditions to check. Using `else if` makes the code more readable and avoids deeply nested structures.

- **`else if` Example**: More readable when you have a clear sequence of conditions.

  **Code Snippet**:
  ```java
  public class ElseIfExample {
      public static void main(String[] args) {
          int score = 85;

          if (score >= 90) {
              System.out.println("Grade A");
          } else if (score >= 80) {
              System.out.println("Grade B");
          } else if (score >= 70) {
              System.out.println("Grade C");
          } else {
              System.out.println("Grade D");
          }
      }
  }
  ```

- **Nested `if` Example**: More complex and harder to follow.

  **Code Snippet**:
  ```java
  public class NestedIfExample {
      public static void main(String[] args) {
          int score = 85;

          if (score >= 70) {
              if (score >= 80) {
                  System.out.println("Grade B");
              } else {
                  System.out.println("Grade C");
              }
          } else if (score >= 60) {
              System.out.println("Grade D");
          } else {
              System.out.println("Grade F");
          }
      }
  }
  ```

### 11. Handling Invalid User Input Using Conditionals

To handle invalid user input, use conditionals to check if the input meets the expected criteria. You can prompt the user to enter a valid input if the initial input is invalid.

**Code Snippet**:
```java
import java.util.Scanner;

public class InputValidation {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int age;

        System.out.print("Enter your age: ");
        if (scanner.hasNextInt()) {
            age = scanner.nextInt();
            if (age < 0 || age > 120) {
                System.out.println("Invalid age. Please enter a valid age between 0 and 120.");
            } else {
                System.out.println("Your age is: " + age);
            }
        } else {
            System.out.println("Invalid input. Please enter a number.");
        }

        scanner.close();
    }
}
```

### 12. Program to Display a Menu with Different Options and Handle User Choices

**Code Snippet**:
```java
import java.util.Scanner;

public class MenuExample {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int choice;

        System.out.println("Menu:");
        System.out.println("1. Option 1");
        System.out.println("2. Option 2");
        System.out.println("3. Option 3");
        System.out.println("4. Exit");
        System.out.print("Enter your choice: ");

        choice = scanner.nextInt();

        switch (choice) {
            case 1:
                System.out.println("You chose Option 1.");
                break;
            case 2:
                System.out.println("You chose Option 2.");
                break;
            case 3:
                System.out.println("You chose Option 3.");
                break;
            case 4:
                System.out.println("Exiting...");
                break;
            default:
                System.out.println("Invalid choice. Please select a valid option.");
                break;
        }

        scanner.close();
    }
}
```

### 13. Debugging Errors Related to Conditional Statements

To debug errors in conditional statements:
1. **Use Print Statements**: Print values and execution paths to understand what's happening.
2. **Check Conditions**: Verify if conditions are correct and cover all possible cases.
3. **Use Debugger**: Set breakpoints and step through code to observe behavior.
4. **Simplify Conditions**: Break down complex conditions into simpler parts.

**Code Snippet**:
```java
public class DebuggingExample {
    public static void main(String[] args) {
        int number = 15;

        System.out.println("Debugging: Number = " + number);

        if (number % 2 == 0) {
            System.out.println("Number is even.");
        } else {
            System.out.println("Number is odd.");
        }
    }
}
```

### 14. Common Mistakes with Conditionals

1. **Incorrect Condition Logic**: Using wrong logical operators or conditions.
2. **Missing `else` Clause**: Not handling all possible cases, leading to unexpected behavior.
3. **Unnecessary Nesting**: Overusing nested `if` statements which makes code harder to read.
4. **Not Checking All Cases**: Missing edge cases or unexpected values.

**Code Snippet**:
```java
public class CommonMistakes {
    public static void main(String[] args) {
        int number = -1;

        // Common mistake: Missing else for all cases
        if (number > 0) {
            System.out.println("Number is positive.");
        } // No handling for zero or negative numbers

        // Common mistake: Incorrect logic
        if (number % 2 = 0) { // Error: should use '=='
            System.out.println("Number is even.");
        }
    }
}
```

### 15. Improving Readability of Conditional Code

1. **Use Descriptive Variable Names**: Make variable names meaningful to the conditions.
2. **Break Down Complex Conditions**: Use helper variables or methods to simplify conditions.
3. **Avoid Deep Nesting**: Refactor to use `else if` or `switch` statements where possible.
4. **Use Comments**: Explain the purpose of complex conditions.

**Code Snippet**:
```java
public class ReadableConditions {
    public static void main(String[] args) {
        int score = 85;
        String grade;

        if (score >= 90) {
            grade = "A";
        } else if (score >= 80) {
            grade = "B";
        } else if (score >= 70) {
            grade = "C";
        } else {
            grade = "D";
        }

        System.out.println("Grade: " + grade);
    }
}
```

### 16. Ternary Operator in Java

The ternary operator is a shorthand for an `if-else` statement that returns one of two values based on a condition. It has the form: `condition ? value_if_true : value_if_false`.

**Code Snippet**:
```java
public class TernaryOperatorExample {
    public static void main(String[] args) {
        int number = 10;

        // Using ternary operator to determine if number is positive or negative
        String result = (number >= 0) ? "Positive" : "Negative";
        System.out.println("The number is: " + result);
    }
}
```

### 17. Short-Circuiting Evaluation with Logical Operators

Short-circuiting occurs when the evaluation of a logical expression stops as soon as the result is determined:

- **AND (`&&`)**: If the first condition is `false`, the second condition is not evaluated.
- **OR (`||`)**: If the first condition is `true`, the second condition is not evaluated.

**Code Snippet**:
```java
public class ShortCircuiting {
    public static void main(String[] args) {
        int x = 5;
        int y = 10;

        // Short-circuit AND: Second condition is not evaluated if the first is false
        if (x > 10 && y > 5) {
            System.out.println("Both conditions are true.");
        } else {
            System.out.println("Short-circuiting in action.");
        }

        // Short-circuit OR: Second condition is not evaluated if the first is true
        if (x < 10 || y < 5) {
            System.out.println("At least one condition is true.");
        }
    }
}
```