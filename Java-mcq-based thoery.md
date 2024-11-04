# Java Concepts and Questions

## 1. `throws` and `throw` in Java

  
- **`throw`:** This keyword is used to explicitly throw an exception in your code. When you use `throw`, you must provide an instance of the exception class you want to throw. This is typically used in scenarios where you want to indicate that a specific error condition has occurred.

- **`throws`:** This keyword is used in a method signature to declare that a method may throw one or more exceptions. By using `throws`, you inform the callers of the method that they need to handle these exceptions, either with a try-catch block or by declaring them in their own method signatures.

Certainly! Here's a detailed explanation of the difference between `throws` and `throw` in Java, including their usage and examples:


### Difference Between `throws` and `throw`
### 1. Definition

- **`throw`**: 
  - `throw` is a keyword used to explicitly throw an exception from a method or a block of code.
  - It is followed by an instance of an exception class (e.g., `throw new ExceptionType("Error message");`).

- **`throws`**: 
  - `throws` is a keyword used in a method declaration to indicate that the method may throw one or more exceptions during its execution.
  - It specifies the types of exceptions that can be thrown by the method.

### 2. Usage Context

- **`throw`**:
  - Used inside the method body to signal that an exceptional condition has occurred.
  - Can be used to throw checked and unchecked exceptions.

- **`throws`**:
  - Used in the method signature (declaration) to indicate that the method can propagate certain exceptions to its caller.
  - Only checked exceptions need to be declared with `throws`; unchecked exceptions do not require declaration.

### 3. Syntax

- **`throw`**:
  ```java
  public void exampleMethod() {
      if (someCondition) {
          throw new IllegalArgumentException("Invalid argument provided");
      }
  }
  ```

- **`throws`**:
  ```java
  public void anotherMethod() throws IOException {
      // Method implementation that may throw IOException
  }
  ```

### 4. Example

Here's a complete example to illustrate both `throw` and `throws`:

```java
public class ExceptionExample {
    // Method that declares it may throw an IOException
    public void readFile(String filePath) throws IOException {
        if (filePath == null) {
            throw new IOException("File path cannot be null"); // Using throw
        }
        // Code to read the file...
    }

    public static void main(String[] args) {
        ExceptionExample example = new ExceptionExample();
        try {
            example.readFile(null); // This will cause an IOException to be thrown
        } catch (IOException e) {
            System.out.println("Caught exception: " + e.getMessage());
        }
    }
}
```

### 5. Summary

- **`throw`** is used to throw an exception explicitly within a method, while **`throws`** is used in a method signature to declare that the method may throw exceptions to the caller.
- `throw` is followed by an exception instance, whereas `throws` is followed by the exception type(s) that can be thrown.

### 6. When to Use

- Use `throw` when you want to indicate an error or exceptional condition within your method.
- Use `throws` in the method declaration when your method might encounter an exceptional situation that it does not handle internally and needs to be passed up to the calling method.

This understanding helps to manage exceptions effectively in Java, promoting better error handling and program stability.

## 2. `assert` in Java

- The `assert` statement is used for debugging purposes to assert that a condition holds true at a particular point in your code. If the condition evaluates to false, it throws an `AssertionError`, which can help you identify logical errors during development. Assertions can be enabled or disabled at runtime through command-line options.


  ```java

  assert condition : "Assertion failed!";

  ```

## 3. Purpose of `hashCode()` method in Java

- The `hashCode()` method returns an integer value, which serves as the hash code for the object. This method is crucial for hash-based collections like `HashMap`, `HashSet`, and `Hashtable`. The hash code is used to determine the bucket in which the object will be stored, allowing for efficient retrieval. If two objects are considered equal (as per the `equals()` method), they must produce the same hash code.


  ```java

  @Override

  public int hashCode() {

      // Custom implementation

  }

  ```

## 4. `transient` keyword in Java

- The `transient` keyword is used in the context of serialization. When an object is serialized, its fields marked with the `transient` keyword are not included in the serialized representation. This is useful for fields that do not need to be saved (like sensitive information or temporary state).
  
  ```java

  transient int tempData; // This field will not be serialized

  ```

## 5. True statement about generics in Java

- **a) Generics enforce compile-time type safety**: **True**. Generics provide type safety by allowing you to specify the type of objects that a collection can hold, reducing the risk of `ClassCastException` at runtime.

- **b) Generics can be used with primitive data types**: **False**. Generics work only with reference types. Primitive types must be wrapped in their corresponding wrapper classes (e.g., `int` becomes `Integer`).

- **c) Generics are determined at runtime**: **False**. Generics are checked at compile time through type erasure, meaning that the generic type information is not available at runtime.

- **d) Generics only apply to classes, not methods**: **False**. Generics can be applied to both classes and methods, allowing for flexible and reusable code.

## 6. Serialization in Java

- **a) The process of converting an object into bytes for storage or transmission**: **True**. Serialization is the process of converting an object's state into a byte stream, enabling it to be saved to a file or sent over a network.

- **b) A method of sorting objects in a collection**: **False**. This does not describe serialization.

- **c) A way to execute multiple threads in sequence**: **False**. This describes a different concept related to threading.

- **d) The process of cloning an object**: **False**. Cloning is a separate concept that involves creating an exact copy of an object.

## 7. True statement about multithreading in Java

- **a) Threads in Java are started using the Thread.run() method**: **False**. Threads are started using the `start()` method. The `run()` method is called internally by the `start()` method.

- **b) A thread can be run only once in its lifecycle**: **True**. Once a thread has been started, it cannot be restarted; attempting to do so will throw an `IllegalThreadStateException`.

- **c) The synchronized keyword prevents race conditions by locking methods and variables**: **True**. The `synchronized` keyword is used to ensure that only one thread can execute a block of code or method at a time, preventing race conditions.

- **d) Threads cannot be interrupted once started**: **False**. Threads can be interrupted using the `interrupt()` method, allowing for graceful termination of a thread.

## 8. Reflection in Java

- **a) The ability of a class to invoke its own methods**: **False**. This does not accurately define reflection.

- **b) A feature that allows examination and modification of class behavior at runtime**: **True**. Reflection enables you to inspect classes, methods, fields, and modify their behavior at runtime.

- **c) A design pattern used for object creation**: **False**. Reflection is not a design pattern.

- **d) A technique to serialize objects**: **False**. Serialization is a separate process from reflection.  

## 9. Method Hiding in Java

- **a) When a child class method hides the parent class method using the same signature**: **True**. This occurs with static methods. If a child class declares a static method with the same name and parameters as a static method in the parent class, the child method hides the parent method.

- **b) When a parent class method hides the child class method**: **False**. This does not accurately describe method hiding.

- **c) When method overloading is not possible in child classes**: **False**. Method overloading is indeed possible in child classes.

- **d) When static methods in a class cannot be accessed by subclasses**: **False**. Static methods can be accessed by subclasses.

  ----------
  