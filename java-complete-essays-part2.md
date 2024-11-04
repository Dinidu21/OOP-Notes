## Section 3: Advanced Java Concepts

### A. Constructor Overloading and Object Initialization

#### Basic Constructor Concepts
```java
public class Student {
    private String name;
    private int age;
    private String id;
    
    // Default constructor
    public Student() {
        this("Unknown", 0, "000");
    }
    
    // Parameterized constructor
    public Student(String name) {
        this(name, 0, "000");
    }
    
    // Full constructor
    public Student(String name, int age, String id) {
        this.name = name;
        this.age = age;
        this.id = id;
    }
}
```

Constructor Chaining:
```java
public class Employee {
    private String name;
    private double salary;
    private String department;
    
    public Employee() {
        this("New Employee"); // Calls single parameter constructor
    }
    
    public Employee(String name) {
        this(name, 50000.0); // Calls two parameter constructor
    }
    
    public Employee(String name, double salary) {
        this(name, salary, "General"); // Calls three parameter constructor
    }
    
    public Employee(String name, double salary, String department) {
        this.name = name;
        this.salary = salary;
        this.department = department;
    }
}
```

### B. to String() Method Implementation

#### Default Implementation
```java
public class DefaultToString {
    // Default toString() returns: getClass().getName() + '@' + Integer.toHexString(hashCode())
    // Example output: "DefaultToString@15db9742"
}
```

#### Custom Implementation
```java
public class Person {
    private String name;
    private int age;
    private String email;
    
    @Override
    public String toString() {
        return String.format("Person[name='%s', age=%d, email='%s']",
            name, age, email);
    }
}
```

#### Advanced to String() with Builder Pattern
```java
public class ComplexObject {
    private List<String> items;
    private Map<String, Integer> properties;
    
    @Override
    public String toString() {
        StringBuilder sb = new StringBuilder();
        sb.append("ComplexObject{\n");
        sb.append("  items=").append(items).append(",\n");
        sb.append("  properties={\n");
        properties.forEach((key, value) -> 
            sb.append("    ").append(key).append(": ").append(value).append(",\n"));
        sb.append("  }\n");
        sb.append("}");
        return sb.toString();
    }
}
```

### C. Memory Management and Garbage Collection

#### Memory Allocation
```java
public class MemoryExample {
    public static void main(String[] args) {
        // Stack memory allocation
        int localVar = 5;
        
        // Heap memory allocation
        Object obj = new Object();
        
        // Object eligible for GC
        obj = null;
        
        // Force garbage collection (not recommended in production)
        System.gc();
    }
}
```

#### Garbage Collection Process
```java
public class GarbageCollectionDemo {
    private static class Resource {
        private final String name;
        
        public Resource(String name) {
            this.name = name;
        }
        
        @Override
        protected void finalize() {
            System.out.println("Resource " + name + " is being garbage collected");
        }
    }
    
    public static void main(String[] args) {
        // Create objects
        Resource r1 = new Resource("R1");
        Resource r2 = new Resource("R2");
        
        // Make objects eligible for GC
        r1 = null;
        r2 = null;
        
        // Suggest garbage collection
        System.gc();
    }
}
```

### D. Interfaces and Abstract Classes

#### Abstract Class Example
```java
public abstract class Vehicle {
    protected String brand;
    protected String model;
    
    // Constructor in abstract class
    public Vehicle(String brand, String model) {
        this.brand = brand;
        this.model = model;
    }
    
    // Abstract method
    public abstract void start();
    
    // Concrete method
    public void stop() {
        System.out.println("Vehicle stopping");
    }
}
```

#### Interface Example
```java
public interface PaymentProcessor {
    void processPayment(double amount);
    
    // Default method (Java 8+)
    default boolean validatePayment(double amount) {
        return amount > 0;
    }
    
    // Static method (Java 8+)
    static String getVersion() {
        return "1.0";
    }
}
```

#### Implementation Example
```java
public class Car extends Vehicle implements Maintainable, Insurable {
    public Car(String brand, String model) {
        super(brand, model);
    }
    
    @Override
    public void start() {
        System.out.println("Car starting");
    }
    
    @Override
    public void performMaintenance() {
        System.out.println("Performing car maintenance");
    }
    
    @Override
    public double calculateInsurance() {
        return 1000.0;
    }
}
```

### E. Method Overloading

#### Basic Overloading
```java
public class Calculator {
    // Method overloading based on number of parameters
    public int add(int a, int b) {
        return a + b;
    }
    
    public int add(int a, int b, int c) {
        return a + b + c;
    }
    
    // Method overloading based on parameter types
    public double add(double a, double b) {
        return a + b;
    }
    
    // Method overloading based on parameter order
    public String concat(String str, int num) {
        return str + num;
    }
    
    public String concat(int num, String str) {
        return num + str;
    }
}
```

#### Advanced Overloading
```java
public class DataProcessor {
    // Array processing
    public void process(int[] data) {
        // Process integer array
    }
    
    // List processing
    public void process(List<Integer> data) {
        // Process integer list
    }
    
    // Varargs
    public void process(int... numbers) {
        // Process variable number of integers
    }
    
    // Generic type
    public <T> void process(T data) {
        // Process generic type
    }
}
```

### F. Static vs Instance Methods

#### Static Methods
```java
public class MathUtils {
    // Static method - utility function
    public static int square(int number) {
        return number * number;
    }
    
    // Static method with static variable
    private static int counter = 0;
    
    public static int getNextCounter() {
        return ++counter;
    }
}
```

#### Instance Methods
```java
public class BankAccount {
    private double balance;
    
    // Instance method - operates on object state
    public void deposit(double amount) {
        if (amount > 0) {
            this.balance += amount;
        }
    }
    
    // Instance method using both instance and static methods
    public void applyInterest(double rate) {
        double interest = MathUtils.calculateInterest(this.balance, rate);
        deposit(interest);
    }
}
```

### G. Final Keyword Usage

#### Final Variables
```java
public class Constants {
    // Final instance variable
    private final String id;
    
    // Final static variable (constant)
    public static final double PI = 3.14159;
    
    public Constants(String id) {
        this.id = id; // Can only be assigned once
    }
}
```

#### Final Methods
```java
public class Parent {
    // Final method cannot be overridden
    public final void secureMethod() {
        // Implementation
    }
}
```

#### Final Classes
```java
// Final class cannot be inherited
public final class ImmutableClass {
    private final int value;
    
    public ImmutableClass(int value) {
        this.value = value;
    }
    
    public int getValue() {
        return value;
    }
}
```

### H. Exception Handling

#### Checked Exceptions
```java
public class FileProcessor {
    public void readFile(String path) throws IOException {
        try (BufferedReader reader = new BufferedReader(new FileReader(path))) {
            String line;
            while ((line = reader.readLine()) != null) {
                processLine(line);
            }
        } catch (IOException e) {
            logger.error("Error reading file: " + path, e);
            throw e;
        }
    }
}
```

#### Unchecked Exceptions
```java
public class ArrayProcessor {
    public int getElement(int[] array, int index) {
        // Runtime exception - no throws clause needed
        if (array == null) {
            throw new NullPointerException("Array cannot be null");
        }
        
        if (index < 0 || index >= array.length) {
            throw new ArrayIndexOutOfBoundsException("Invalid index: " + index);
        }
        
        return array[index];
    }
}
```

This comprehensive guide covers all the major topics in your questions with detailed examples and explanations based on the Java Language Specification.