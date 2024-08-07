# Basic Syntax

### 1. Different Data Types Available in Java

Java has two main categories of data types:

**Primitive Data Types:**
- **byte**: 8-bit integer.
- **short**: 16-bit integer.
- **int**: 32-bit integer.
- **long**: 64-bit integer.
- **float**: Single-precision 32-bit floating point.
- **double**: Double-precision 64-bit floating point.
- **char**: 16-bit Unicode character.
- **boolean**: Represents true or false.

**Reference Data Types:**
- **Objects**: Instances of classes.
- **Arrays**: Containers for holding a fixed number of values of a single type.
- **Strings**: Objects that represent a sequence of characters.

### 2. Declaring and Initializing Variables in Java

**Declaration**:
- Declaring a variable means specifying its type and name.
  ```java
  int number; // Declares an integer variable named 'number'
  ```

**Initialization**:
- Initializing a variable means assigning it a value.
  ```java
  number = 10; // Initializes 'number' with the value 10
  ```

**Declaration and Initialization**:
- You can declare and initialize a variable in a single line.
  ```java
  int number = 10; // Declares and initializes 'number' with the value 10
  ```

**Difference**:
- **Declaration** alone reserves memory for the variable but does not assign any value.
- **Initialization** assigns a specific value to the variable, making it ready for use.

### 3. Arithmetic Operators in Java

- **+**: Addition
  ```java
  int sum = 5 + 3; // sum is 8
  ```
- **-**: Subtraction
  ```java
  int difference = 5 - 3; // difference is 2
  ```
- **\***: Multiplication
  ```java
  int product = 5 * 3; // product is 15
  ```
- **/**: Division
  ```java
  int quotient = 5 / 2; // quotient is 2 (integer division)
  ```
- **%**: Modulus (remainder)
  ```java
  int remainder = 5 % 2; // remainder is 1
  ```

### 4. Comparison Operators in Java

- **==**: Equal to
  ```java
  boolean isEqual = (5 == 3); // isEqual is false
  ```
- **!=**: Not equal to
  ```java
  boolean isNotEqual = (5 != 3); // isNotEqual is true
  ```
- **>**: Greater than
  ```java
  boolean isGreater = (5 > 3); // isGreater is true
  ```
- **<**: Less than
  ```java
  boolean isLess = (5 < 3); // isLess is false
  ```
- **>=**: Greater than or equal to
  ```java
  boolean isGreaterOrEqual = (5 >= 3); // isGreaterOrEqual is true
  ```
- **<=**: Less than or equal to
  ```java
  boolean isLessOrEqual = (5 <= 3); // isLessOrEqual is false
  ```

### 5. Logical Operators in Java

- **AND (&&)**: Returns true if both operands are true.
  ```java
  boolean result = (5 > 3) && (2 < 4); // result is true
  ```
- **OR (||)**: Returns true if at least one operand is true.
  ```java
  boolean result = (5 > 3) || (2 > 4); // result is true
  ```
- **NOT (!)**: Inverts the boolean value.
  ```java
  boolean result = !(5 > 3); // result is false
  ```

### 6. Control Flow Statements in Java

**If-Else Statement**:
- Executes a block of code if a condition is true, and optionally another block if the condition is false.
  ```java
  if (temperature > 30) {
      System.out.println("It's hot outside.");
  } else {
      System.out.println("It's not too hot outside.");
  }
  ```

**Switch Statement**:
- Selects one of many code blocks to execute.
  ```java
  int day = 3;
  switch (day) {
      case 1:
          System.out.println("Monday");
          break;
      case 2:
          System.out.println("Tuesday");
          break;
      case 3:
          System.out.println("Wednesday");
          break;
      default:
          System.out.println("Weekend");
  }
  ```

### 7. Creating Loops in Java

**For Loop**:
- Executes a block of code a specific number of times.
  ```java
  for (int i = 0; i < 5; i++) {
      System.out.println(i); // Prints 0 to 4
  }
  ```

**While Loop**:
- Executes a block of code as long as a condition is true.
  ```java
  int i = 0;
  while (i < 5) {
      System.out.println(i); // Prints 0 to 4
      i++;
  }
  ```

**Functionality**:
- **For Loop**: Best when the number of iterations is known beforehand.
- **While Loop**: Best when the number of iterations is not known and depends on a condition evaluated during each iteration.

### 8. Different Types of Comments Used in Java Code

Java supports three types of comments:

1. **Single-line Comment**:
   - Begins with `//` and extends to the end of the line.
   ```java
   // This is a single-line comment
   int x = 10; // Comment after code
   ```

2. **Multi-line Comment**:
   - Begins with `/*` and ends with `*/`. It can span multiple lines.
   ```java
   /* This is a multi-line comment.
      It can span multiple lines. */
   int y = 20;
   ```

3. **Documentation Comment**:
   - Begins with `/**` and ends with `*/`. It is used for generating documentation using Javadoc.
   ```java
   /**
    * This is a documentation comment.
    * It is used to describe classes, methods, and fields.
    */
   public class Example {
       // Code here
   }
   ```

### 9. Concept of Keywords in Java

**Keywords** are reserved words that have a predefined meaning in Java. They cannot be used as identifiers (names for variables, classes, methods, etc.).

**Examples of Java Keywords**:
- `int` - Defines an integer type.
- `class` - Defines a class.
- `public` - Access modifier that makes members accessible from any other class.
- `static` - Indicates that a member belongs to the class rather than instances of the class.
- `void` - Specifies that a method does not return a value.
- `if`, `else`, `switch` - Control flow statements.
- `for`, `while`, `do` - Loop control statements.
- `try`, `catch`, `finally` - Exception handling.

**Code Snippet**:
```java
public class KeywordsExample {
    public static void main(String[] args) {
        int number = 10; // 'int' is a keyword
        System.out.println(number);
    }
}
```

### 10. Difference Between Primitive Data Types and Reference Data Types in Java

**Primitive Data Types**:
- Hold their values directly.
- Examples: `int`, `char`, `boolean`, `float`.
- **Code Snippet**:
  ```java
  int num = 5; // 'num' holds the value 5 directly
  char letter = 'A'; // 'letter' holds the value 'A' directly
  ```

**Reference Data Types**:
- Refer to objects or instances of classes.
- Examples: `String`, Arrays, User-defined classes.
- **Code Snippet**:
  ```java
  String message = "Hello"; // 'message' refers to a String object
  int[] numbers = {1, 2, 3}; // 'numbers' refers to an array object
  ```

### 11. Taking Input from the User in Java

You can use the `Scanner` class from `java.util` package to take input from the user.

**Code Snippet**:
```java
import java.util.Scanner;

public class InputExample {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.print("Enter your name: ");
        String name = scanner.nextLine(); // Read a string input
        System.out.println("Hello, " + name);

        System.out.print("Enter your age: ");
        int age = scanner.nextInt(); // Read an integer input
        System.out.println("You are " + age + " years old.");
        
        scanner.close(); // Close the scanner
    }
}
```

### 12. Syntax for Creating a Simple Java Program

A basic Java program consists of a class definition, a `main` method, and statements inside the `main` method.

**Code Snippet**:
```java
public class SimpleProgram {
    public static void main(String[] args) {
        System.out.println("Hello, World!"); // Output message to console
    }
}
```

**Explanation**:
- `public class SimpleProgram` - Defines a class named `SimpleProgram`.
- `public static void main(String[] args)` - The entry point of the program.
- `System.out.println("Hello, World!");` - Prints text to the console.

### 13. Main Method in Java and Its Significance

The `main` method is the entry point of any standalone Java application. It must be declared as `public static void` and accept a single argument of type `String[]`.

**Code Snippet**:
```java
public class MainMethodExample {
    public static void main(String[] args) {
        System.out.println("This is the main method.");
    }
}
```

**Significance**:
- The Java Virtual Machine (JVM) calls the `main` method when the program is run.
- It serves as the starting point for execution.

### 14. Access Modifiers in Java

**Public**:
- Accessible from any other class.
- **Code Snippet**:
  ```java
  public class PublicClass {
      public int publicField; // Can be accessed from any other class
  }
  ```

**Private**:
- Accessible only within the same class.
- **Code Snippet**:
  ```java
  public class PrivateClass {
      private int privateField; // Cannot be accessed from outside this class

      public void setPrivateField(int value) {
          privateField = value;
      }

      public int getPrivateField() {
          return privateField;
      }
  }
  ```

**Protected**:
- Accessible within the same package and subclasses (even if they are in different packages).
- **Code Snippet**:
  ```java
  public class ProtectedClass {
      protected int protectedField; // Accessible within the package and by subclasses
  }
  ```