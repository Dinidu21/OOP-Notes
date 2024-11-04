# Comprehensive Java Programming Guide

## 1. Fundamentals of Object-Oriented Programming (OOP)

### What is OOP?
Object-Oriented Programming is a programming paradigm based on the concept of "objects" that contain data (attributes) and code (methods). It provides a clear modular structure for programs, making it excellent for large, complex, and actively maintained software systems.

### Key Concepts

#### 1. Abstraction
- Definition: The process of hiding complex implementation details and showing only the necessary features of an object
- Implementation in Java:
  - Abstract classes
  - Interfaces
  - Method abstraction

#### 2. Encapsulation
- Definition: Bundling of data and the methods that operate on that data within a single unit (class)
- Implementation:
  - Access modifiers
  - Getter/setter methods
  - Data hiding

#### 3. Inheritance
- Definition: Mechanism that allows a class to inherit properties and methods from another class
- Types:
  - Single inheritance
  - Multiple inheritance (through interfaces)
  - Multilevel inheritance

#### 4. Polymorphism
- Definition: Ability of different classes to be treated as instances of the same class through base class reference
- Types:
  - Static (compile-time) polymorphism
  - Dynamic (runtime) polymorphism

### Benefits of OOP
1. Reusability through inheritance
2. Flexibility through polymorphism
3. Data hiding and abstraction
4. Code organization and maintainability
5. Code modularity and structure

## 2. Classes and Objects

### Class Structure
```java
public class ClassName {
    // Instance variables
    private int variableName;
    
    // Static variables
    private static int staticVariable;
    
    // Constructors
    public ClassName() {
        // Default constructor
    }
    
    // Methods
    public void methodName() {
        // Method implementation
    }
}
```

### Objects
- Creation using `new` keyword
- Memory allocation
- Object lifecycle
- Garbage collection

### Instance vs Class Variables
#### Instance Variables
- Unique to each instance
- Created when object is instantiated
- Accessed through object reference

#### Class Variables (Static)
- Shared across all instances
- Created when class is loaded
- Accessed through class name

### Methods and Constructors
#### Methods
- Instance methods
- Static methods
- Method overloading
- Method parameters and return types

#### Constructors
- Default constructor
- Parameterized constructor
- Constructor overloading
- Constructor chaining

### `this` Keyword
- References current instance
- Used to:
  - Differentiate instance variables from parameters
  - Call another constructor
  - Return current instance
  - Pass current instance as parameter

## 3. Encapsulation and Access Modifiers

### Access Modifiers
| Modifier  | Class | Package | Subclass | World |
|-----------|-------|---------|----------|-------|
| public    | Y     | Y       | Y        | Y     |
| protected | Y     | Y       | Y        | N     |
| default   | Y     | Y       | N        | N     |
| private   | Y     | N       | N        | N     |

### Getter/Setter Methods
```java
public class Person {
    private String name;
    private int age;
    
    public String getName() {
        return name;
    }
    
    public void setName(String name) {
        this.name = name;
    }
}
```

### Packages
- Organization of related classes
- Naming conventions
- Import statements
  - Single type import
  - On-demand type import
  - Static import

## 4. Inheritance

### Implementation
```java
public class Parent {
    protected int parentField;
    
    public void parentMethod() {
        // Implementation
    }
}

public class Child extends Parent {
    private int childField;
    
    @Override
    public void parentMethod() {
        // Overridden implementation
    }
}
```

### Method Overriding Rules
1. Method signature must be same
2. Return type must be same or covariant
3. Access level can't be more restrictive
4. Can't throw broader checked exceptions

### `super` Keyword
- Access parent class members
- Call parent class constructor
- Used in method overriding

## 5. Polymorphism

### Compile-time Polymorphism (Method Overloading)
```java
public class Calculator {
    public int add(int a, int b) {
        return a + b;
    }
    
    public double add(double a, double b) {
        return a + b;
    }
}
```

### Runtime Polymorphism
```java
class Animal {
    void makeSound() {
        System.out.println("Some sound");
    }
}

class Dog extends Animal {
    @Override
    void makeSound() {
        System.out.println("Woof");
    }
}

// Usage
Animal animal = new Dog(); // Upcasting
animal.makeSound(); // Outputs "Woof"
```

### Dynamic Method Dispatch
- Runtime binding of method calls
- Based on actual object type
- Enables polymorphic behavior

## 6. Abstraction

### Abstract Classes
```java
public abstract class Shape {
    abstract double calculateArea();
    
    // Concrete method
    public void display() {
        System.out.println("Area: " + calculateArea());
    }
}
```

### Interfaces
```java
public interface Drawable {
    void draw(); // implicitly public abstract
    
    default void print() {
        System.out.println("Printing");
    }
}
```

### Abstract Classes vs Interfaces

| Feature           | Abstract Class                | Interface                    |
|-------------------|------------------------------|------------------------------|
| Multiple Inheritance | No                        | Yes                         |
| Constructor      | Can have                     | Cannot have                  |
| State            | Can have                     | Only constants               |
| Methods          | Both abstract and concrete   | Abstract, default, static    |
| Access Modifiers | All allowed                  | Only public                  |

## 7. Exception Handling

### Exception Hierarchy
```
Throwable
├── Error
└── Exception
    ├── RuntimeException (Unchecked)
    └── Other Exceptions (Checked)
```

### Try-Catch-Finally
```java
try {
    // Code that might throw exception
} catch (SpecificException e) {
    // Handle specific exception
} catch (Exception e) {
    // Handle general exception
} finally {
    // Always executed
}
```

### Custom Exceptions
```java
public class CustomException extends Exception {
    public CustomException(String message) {
        super(message);
    }
}
```

## 8. Java Collections Framework

### Core Interfaces
- Collection
  - List
  - Set
  - Queue
- Map

### Common Implementations

#### List
```java
List<String> arrayList = new ArrayList<>();
List<String> linkedList = new LinkedList<>();
```

#### Set
```java
Set<String> hashSet = new HashSet<>();
Set<String> treeSet = new TreeSet<>();
```

#### Map
```java
Map<String, Integer> hashMap = new HashMap<>();
Map<String, Integer> treeMap = new TreeMap<>();
```

## 9. File Handling and I/O

### File Operations
```java
// Reading file
try (BufferedReader reader = new BufferedReader(new FileReader("file.txt"))) {
    String line;
    while ((line = reader.readLine()) != null) {
        // Process line
    }
}

// Writing file
try (BufferedWriter writer = new BufferedWriter(new FileWriter("file.txt"))) {
    writer.write("Content");
}
```

## 10. Important Keywords and Concepts

### final Keyword
- Variables: Cannot be changed after initialization
- Methods: Cannot be overridden
- Classes: Cannot be inherited

### finally Block
- Always executed after try-catch
- Used for cleanup operations
- Executes even if exception occurs

### finalize() Method
- Called by garbage collector
- Not guaranteed to be called
- Deprecated in newer versions

### Static
- Belongs to class, not instance
- Shared across all instances
- Memory allocation at class loading

### Hiding vs Shadowing
#### Hiding
- Occurs with static methods
- Based on reference type
```java
class Parent {
    static void method() {}
}
class Child extends Parent {
    static void method() {} // hides Parent's method
}
```

#### Shadowing
- Occurs with instance variables
- Based on scope
```java
class Example {
    int x = 10;
    void method() {
        int x = 20; // shadows class field
    }
}
```

### Best Practices
1. Follow naming conventions
2. Use appropriate access modifiers
3. Implement proper exception handling
4. Write clean, maintainable code
5. Document code using Javadoc
6. Use collections appropriately
7. Handle resources properly
8. Follow SOLID principles

This guide covers the core concepts of Java programming based on the Java Language Specification. For more detailed information on specific topics, refer to the official Java documentation and JLS.
