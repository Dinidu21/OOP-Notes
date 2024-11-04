
# Threads in Java

## 1. Thread Class vs Runnable Interface

### **Thread Class**:
- The `Thread` class in Java is used to create and manage threads. By extending the `Thread` class, we can create a new thread by overriding its `run()` method.
- **Example**:
    ```java
    class MyThread extends Thread {
        public void run() {
            System.out.println("Thread is running");
        }
    }

    public class Main {
        public static void main(String[] args) {
            MyThread thread = new MyThread();
            thread.start();  // Starts the thread
        }
    }
    ```
- **Advantages**:
    - Simple to use.
    - Methods like `start()`, `join()`, and `sleep()` are part of the `Thread` class.
  
- **Disadvantages**:
    - In Java, a class can only extend one class, so extending `Thread` restricts the class from extending other classes.

### **Runnable Interface**:
- The `Runnable` interface defines a single method `run()`. It is implemented by classes that wish to execute code in a separate thread.
- **Example**:
    ```java
    class MyRunnable implements Runnable {
        public void run() {
            System.out.println("Thread is running");
        }
    }

    public class Main {
        public static void main(String[] args) {
            Thread thread = new Thread(new MyRunnable());
            thread.start();  // Starts the thread
        }
    }
    ```

- **Advantages**:
    - Implements `Runnable`, so the class can extend other classes.
    - Recommended approach for creating threads.

---

## 2. Thread Lifecycle

Java threads have the following states, as defined in the Java Language Specification:

### 1. **New**:
- A thread is created but not yet started.
  
### 2. **Runnable**:
- The thread is ready to run or is already running. The JVM’s thread scheduler can schedule it.

### 3. **Blocked**:
- The thread is blocked and waiting to acquire a lock.

### 4. **Waiting**:
- The thread is waiting indefinitely until another thread performs a specific action (e.g., `notify()`, `notifyAll()`).

### 5. **Timed Waiting**:
- The thread is waiting for a specified amount of time (e.g., `Thread.sleep()`, `wait(long timeout)`).

### 6. **Terminated**:
- The thread has finished execution.

**Diagram**:
```
New --> Runnable <--> Blocked / Waiting / Timed Waiting --> Terminated
```

---

## 3. Thread Pool

- A thread pool reuses a group of threads instead of creating new ones for each task.
- Java provides the `ExecutorService` interface for managing thread pools.
  
**Example**:
```java
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

public class ThreadPoolExample {
    public static void main(String[] args) {
        ExecutorService executor = Executors.newFixedThreadPool(5);

        for (int i = 0; i < 10; i++) {
            Runnable worker = new WorkerThread("" + i);
            executor.execute(worker);
        }

        executor.shutdown();
    }
}

class WorkerThread implements Runnable {
    private String message;
    public WorkerThread(String s) {
        this.message = s;
    }

    public void run() {
        System.out.println(Thread.currentThread().getName() + " (Start) Message = " + message);
    }
}
```

---

## 4. Thread Priority

- Each thread has a priority, an integer value between `1` (MIN_PRIORITY) and `10` (MAX_PRIORITY). The default priority is `5`.
- Thread priorities affect the order in which threads are scheduled but do not guarantee any specific execution order.

```java
Thread t1 = new Thread();
t1.setPriority(Thread.MAX_PRIORITY);
```

---

## 5. Daemon Threads

- Daemon threads are low-priority threads running in the background to perform tasks such as garbage collection.
- When all non-daemon threads finish execution, the JVM terminates the program, stopping all daemon threads.
  
**Example**:
```java
class MyDaemonThread extends Thread {
    public void run() {
        if (Thread.currentThread().isDaemon()) {
            System.out.println("Daemon thread running");
        } else {
            System.out.println("User thread running");
        }
    }

    public static void main(String[] args) {
        MyDaemonThread t1 = new MyDaemonThread();
        MyDaemonThread t2 = new MyDaemonThread();
        t1.setDaemon(true);  // Now t1 is a daemon thread
        t1.start();
        t2.start();
    }
}
```

---

## 6. Lambda Expressions in Threads

Java 8 introduced lambda expressions, which allow for concise code when using functional interfaces like `Runnable`. The `Runnable` interface is a functional interface with a single method (`run()`), making it suitable for lambda expressions.

**Why Threads Can Use Lambda Expressions**:
- The `Runnable` interface has only one abstract method, `run()`. This allows lambda expressions to be used to represent the `run()` method without needing an explicit implementation class.

**Example**:
```java
public class LambdaThreadExample {
    public static void main(String[] args) {
        Thread t = new Thread(() -> {
            System.out.println("Thread using lambda expression");
        });
        t.start();
    }
}
```

---

## 7. Synchronization

- Synchronization ensures that multiple threads do not concurrently modify shared data in a way that leads to data inconsistency.
  
- **Synchronized Block**:
    - Ensures only one thread at a time can access the synchronized block of code.
    ```java
    synchronized (object) {
        // Critical section
    }
    ```

- **Synchronized Method**:
    - Only one thread can execute a synchronized method at a time.
    ```java
    public synchronized void myMethod() {
        // Critical section
    }
    ```

- **Intrinsic Locks**:
    - Each object in Java has an intrinsic lock. A thread can acquire the lock by entering a synchronized block or method.

---

## 8. Deadlock

Deadlock occurs when two or more threads are blocked forever, each waiting on the other to release a resource.

**Example**:
```java
class DeadlockExample {
    String resource1 = "Resource1";
    String resource2 = "Resource2";

    Thread t1 = new Thread(() -> {
        synchronized (resource1) {
            System.out.println("Thread 1 locked Resource 1");
            try { Thread.sleep(100); } catch (Exception e) {}

            synchronized (resource2) {
                System.out.println("Thread 1 locked Resource 2");
            }
        }
    });

    Thread t2 = new Thread(() -> {
        synchronized (resource2) {
            System.out.println("Thread 2 locked Resource 2");
            try { Thread.sleep(100); } catch (Exception e) {}

            synchronized (resource1) {
                System.out.println("Thread 2 locked Resource 1");
            }
        }
    });

    public static void main(String[] args) {
        DeadlockExample example = new DeadlockExample();
        example.t1.start();
        example.t2.start();
    }
}
```
In the example, thread `t1` locks `resource1` and waits for `resource2`, while thread `t2` locks `resource2` and waits for `resource1`, creating a deadlock.

---

## 9. Thread Synchronization and Avoiding Deadlock

- **Avoid Nested Locks**: Avoid acquiring locks on multiple resources at once.
- **Use Lock Timeout**: Use a timeout to avoid waiting indefinitely.
- **Use Deadlock Detection Algorithms**: Implement deadlock detection mechanisms where needed.

## 10. Thread.join()

### What is `Thread.join()`?

- The `join()` method in Java allows one thread to wait until another thread finishes its execution. When `join()` is called on a thread, the calling thread pauses its execution until the specified thread terminates.
  
- **Example**:
    ```java
    class MyThread extends Thread {
        public void run() {
            for (int i = 0; i < 5; i++) {
                System.out.println(Thread.currentThread().getName() + " running");
            }
        }
    }

    public class Main {
        public static void main(String[] args) throws InterruptedException {
            MyThread t1 = new MyThread();
            MyThread t2 = new MyThread();
            
            t1.start();
            t1.join();  // Main thread will wait until t1 completes
            t2.start(); // t2 starts after t1 finishes
        }
    }
    ```

### Why Use `join()`?

- Ensures sequential execution where one thread must complete before another can proceed.
- Useful in scenarios where you need to combine the results of multiple threads or maintain thread synchronization.
- Prevents premature execution of code that depends on the completion of another thread.

### Variants of `Thread.join()`

1. **`join()` without parameters**:
    - The calling thread waits indefinitely until the specified thread terminates.
    ```java
    thread.join();  // Waits indefinitely
    ```

2. **`join(long millis)`**:
    - The calling thread waits for a specified time (`millis` milliseconds). If the thread does not complete within the specified time, the calling thread resumes.
    ```java
    thread.join(1000);  // Waits for 1000 milliseconds
    ```

3. **`join(long millis, int nanos)`**:
    - A more precise variant where the thread waits for a combination of milliseconds and nanoseconds.
    ```java
    thread.join(1000, 500);  // Waits for 1000 milliseconds + 500 nanoseconds
    ```

### Real-world Use Case of `Thread.join()`

- **Example: Waiting for Data Processing**:
    Imagine a scenario where you're fetching data from multiple sources (e.g., calling several APIs in parallel), and you need to wait for all data to be fetched before proceeding with further processing.

    **Example**:
    ```java
    class FetchDataThread extends Thread {
        private String source;

        public FetchDataThread(String source) {
            this.source = source;
        }

        public void run() {
            System.out.println("Fetching data from " + source);
            try { Thread.sleep(2000); } catch (InterruptedException e) { }
        }
    }

    public class DataAggregator {
        public static void main(String[] args) throws InterruptedException {
            FetchDataThread api1 = new FetchDataThread("API1");
            FetchDataThread api2 = new FetchDataThread("API2");
            FetchDataThread api3 = new FetchDataThread("API3");

            api1.start();
            api2.start();
            api3.start();

            api1.join();  // Wait for API1 to complete
            api2.join();  // Wait for API2 to complete
            api3.join();  // Wait for API3 to complete

            System.out.println("All data fetched. Proceeding with processing...");
        }
    }
    ```

### Benefits of Using `Thread.join()`:

1. **Control Over Thread Execution**:
   - It allows you to control the flow of your program by making sure that one thread completes its execution before another proceeds.
   
2. **Combining Results**:
   - In multi-threaded environments, if multiple threads are performing different tasks, `join()` ensures that all tasks are completed before proceeding with the final result or further execution.

3. **Synchronization Without Locking**:
   - Unlike traditional synchronization using `synchronized` blocks, `join()` is a simpler mechanism to ensure the orderly completion of threads without explicit locks or waiting conditions.

---
