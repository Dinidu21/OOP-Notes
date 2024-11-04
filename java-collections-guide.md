# Java Collections and Data Structures: A Comprehensive Guide

## 1. Enums vs Final Static Classes

### Enums
Enums in Java provide a way to define a type-safe collection of constants. They were introduced in Java 5.0.

#### Benefits of Enums:
1. **Type Safety**
   - Compile-time checking prevents invalid values
   - Can't create new instances at runtime
   - Can't extend enums

2. **Built-in Functionality**
   - `values()` method to get all constants
   - `valueOf()` method for string conversion
   - `ordinal()` for position in enum
   - Built-in `toString()`

3. **Special Features**
   - Can have methods and fields
   - Can implement interfaces
   - Can have constructors (private only)
   - Thread-safe singleton pattern by default

```java
public enum Direction {
    NORTH(0), SOUTH(180), EAST(90), WEST(270);
    
    private final int degrees;
    
    Direction(int degrees) {
        this.degrees = degrees;
    }
    
    public int getDegrees() {
        return degrees;
    }
}
```

### Final Static Class vs Enum

#### Final Static Class Approach:
```java
public final class Direction {
    public static final Direction NORTH = new Direction(0);
    public static final Direction SOUTH = new Direction(180);
    
    private final int degrees;
    
    private Direction(int degrees) {
        this.degrees = degrees;
    }
}
```

#### Key Differences:
1. **Serialization**
   - Enums have built-in serialization support
   - Static classes need custom serialization

2. **Instance Control**
   - Enums prevent new instance creation
   - Static finals can be bypassed using reflection

3. **Memory Usage**
   - Enums are more memory-efficient
   - Each enum constant is instantiated only once

## 2. HashMap vs TreeMap

### HashMap
A hash table based implementation of Map interface.

#### Characteristics:
1. **Storage Mechanism**
   - Uses hash function to store key-value pairs
   - Maintains array of buckets (Node<K,V>[] table)
   - Uses linked lists or balanced trees for collision resolution

2. **Performance**
   - Average case: O(1) for get/put/remove
   - Worst case: O(n) if many collisions
   - Load factor affects performance (default 0.75)

```java
HashMap<String, Integer> map = new HashMap<>();
map.put("key", 1);  // O(1) average case
map.get("key");     // O(1) average case
```

### TreeMap
A Red-Black tree based NavigableMap implementation.

#### Characteristics:
1. **Storage Mechanism**
   - Self-balancing Red-Black tree
   - Maintains sorted order of keys
   - Binary search tree properties

2. **Performance**
   - O(log n) for all operations
   - Consistent performance
   - No concept of load factor

```java
TreeMap<String, Integer> map = new TreeMap<>();
map.put("key", 1);  // O(log n)
map.get("key");     // O(log n)
```

## 3. Array List vs LinkedList

### Array List
Dynamic array implementation.

#### Characteristics:
1. **Memory**
   - Contiguous memory
   - Resizable array
   - Capacity grows by 50% when full

2. **Performance**
   - O(1) for random access
   - O(n) for insertion/deletion in middle
   - O(1) amortized for append

```java
ArrayList<String> list = new ArrayList<>();
list.add("item");        // O(1) amortized
list.get(0);            // O(1)
list.remove(0);         // O(n)
```

### LinkedList
Doubly-linked list implementation.

#### Characteristics:
1. **Memory**
   - Non-contiguous memory
   - Each element has references to next/previous
   - No capacity issues

2. **Performance**
   - O(n) for random access
   - O(1) for insertion/deletion at known position
   - O(1) for add/remove at ends

```java
LinkedList<String> list = new LinkedList<>();
list.addFirst("item");  // O(1)
list.get(5);           // O(n)
list.remove(0);        // O(1)
```

## 4. HashSet vs TreeSet

### HashSet
Set implementation backed by HashMap.

#### Characteristics:
1. **Storage**
   - Uses HashMap internally
   - Elements stored using hash codes
   - No guaranteed order

2. **Performance**
   - O(1) average case for add/remove/contains
   - No duplicate elements allowed

```java
HashSet<String> set = new HashSet<>();
set.add("item");     // O(1) average
set.contains("item"); // O(1) average
```

### TreeSet
NavigableSet implementation backed by TreeMap.

#### Characteristics:
1. **Storage**
   - Uses TreeMap internally
   - Elements stored in sorted order
   - Self-balancing tree structure

2. **Performance**
   - O(log n) for all operations
   - Natural ordering or custom Comparator

```java
TreeSet<String> set = new TreeSet<>();
set.add("item");     // O(log n)
set.contains("item"); // O(log n)
```

## 5. LinkedList as Stack and Queue

### LinkedList as Stack
```java
LinkedList<String> stack = new LinkedList<>();
stack.push("item");    // addFirst() internally
stack.pop();          // removeFirst() internally
stack.peek();         // getFirst() internally
```

### LinkedList as Queue
```java
LinkedList<String> queue = new LinkedList<>();
queue.offer("item");   // add to tail
queue.poll();         // remove from head
queue.peek();         // view head
```

### When to Use Which Implementation

1. **Use HashMap when:**
   - Need fastest general-purpose key-value storage
   - Order doesn't matter
   - Keys are simple or have good hash function

2. **Use TreeMap when:**
   - Need sorted keys
   - Need range operations on keys
   - Need ceiling/floor operations

3. **Use ArrayList when:**
   - Random access is frequent
   - List size changes infrequently
   - Iteration is primary operation
   
4. **Use LinkedList when:**
   - Frequent insertions/deletions at ends
   - Implementing stack/queue
   - Size changes frequently

5. **Use HashSet when:**
   - Need unique elements
   - Order doesn't matter
   - Fast lookup required

6. **Use TreeSet when:**
   - Need unique elements in sorted order
   - Need range operations
   - Need closest match operations

## Best Practices

1. **Choose Based on Primary Operations**
   - Consider most frequent operations
   - Consider data size
   - Consider memory constraints

2. **Consider Thread Safety**
   - All these collections are not thread-safe
   - Use Collections.synchronizedXXX() or concurrent versions if needed

3. **Initial Capacity**
   - Set initial capacity when size is known
   - Avoid excessive resizing
   - Consider load factor for hash-based collections

4. **Comparators**
   - Implement Comparable for natural ordering
   - Use Comparator for flexible ordering
   - Ensure consistent equals() implementation
