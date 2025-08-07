# Java

## Overview
Java is a class-based, object-oriented programming language designed for portability across platforms. It follows the "Write Once, Run Anywhere" principle through the Java Virtual Machine (JVM).

## Core Concepts

### Basic Syntax
```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

### Data Types
```java
// Primitive Types
byte b = 127;              // 8-bit
short s = 32767;           // 16-bit
int i = 2147483647;        // 32-bit
long l = 9223372036854775807L;  // 64-bit
float f = 3.14f;           // 32-bit floating
double d = 3.14159265359;  // 64-bit floating
char c = 'A';              // 16-bit Unicode
boolean bool = true;       // true/false

// Reference Types
String str = "Hello";
Integer num = 42;  // Wrapper class
int[] array = {1, 2, 3, 4, 5};
```

### Control Flow
```java
// If-else
if (condition) {
    // code
} else if (anotherCondition) {
    // code
} else {
    // code
}

// Switch (traditional)
switch (day) {
    case 1:
        System.out.println("Monday");
        break;
    default:
        System.out.println("Other day");
}

// Switch expression (Java 14+)
String result = switch (day) {
    case 1, 2, 3, 4, 5 -> "Weekday";
    case 6, 7 -> "Weekend";
    default -> "Invalid";
};

// Loops
for (int i = 0; i < 10; i++) { }
for (String item : items) { }
while (condition) { }
do { } while (condition);
```

### Object-Oriented Programming
```java
// Class definition
public class Person {
    // Fields
    private String name;
    private int age;
    
    // Constructor
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
    
    // Getters and Setters
    public String getName() { return name; }
    public void setName(String name) { this.name = name; }
    
    // Methods
    public void introduce() {
        System.out.println("Hi, I'm " + name);
    }
    
    @Override
    public String toString() {
        return "Person{name='" + name + "', age=" + age + "}";
    }
}

// Inheritance
public class Employee extends Person {
    private String department;
    
    public Employee(String name, int age, String department) {
        super(name, age);
        this.department = department;
    }
}

// Interfaces
public interface Drawable {
    void draw();
    default void print() {
        System.out.println("Printing...");
    }
}

// Abstract Classes
public abstract class Shape {
    abstract double getArea();
    
    public void describe() {
        System.out.println("This is a shape");
    }
}
```

### Collections Framework
```java
import java.util.*;

// List
List<String> list = new ArrayList<>();
list.add("item");
list.get(0);
list.remove(0);

// Set
Set<Integer> set = new HashSet<>();
set.add(1);
set.contains(1);

// Map
Map<String, Integer> map = new HashMap<>();
map.put("key", 1);
map.get("key");
map.getOrDefault("key", 0);

// Queue
Queue<String> queue = new LinkedList<>();
queue.offer("item");
queue.poll();

// Iteration
for (String item : list) { }
list.forEach(item -> System.out.println(item));
```

### Streams API
```java
import java.util.stream.*;

List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

// Filter and Map
List<Integer> doubled = numbers.stream()
    .filter(n -> n % 2 == 0)
    .map(n -> n * 2)
    .collect(Collectors.toList());

// Reduce
int sum = numbers.stream()
    .reduce(0, Integer::sum);

// Grouping
Map<String, List<Person>> byCity = people.stream()
    .collect(Collectors.groupingBy(Person::getCity));

// Parallel streams
long count = numbers.parallelStream()
    .filter(n -> n > 2)
    .count();
```

### Exception Handling
```java
try {
    riskyOperation();
} catch (IOException e) {
    System.err.println("IO Error: " + e.getMessage());
} catch (Exception e) {
    System.err.println("Error: " + e.getMessage());
} finally {
    cleanup();
}

// Try-with-resources
try (FileReader reader = new FileReader("file.txt")) {
    // reader auto-closed
}

// Custom exception
public class CustomException extends Exception {
    public CustomException(String message) {
        super(message);
    }
}

// Throwing exceptions
public void validate(int age) throws IllegalArgumentException {
    if (age < 0) {
        throw new IllegalArgumentException("Age cannot be negative");
    }
}
```

### Generics
```java
// Generic class
public class Box<T> {
    private T content;
    
    public void set(T content) { this.content = content; }
    public T get() { return content; }
}

// Generic method
public <T> T firstElement(List<T> list) {
    return list.get(0);
}

// Bounded type parameters
public <T extends Comparable<T>> T max(T a, T b) {
    return a.compareTo(b) > 0 ? a : b;
}

// Wildcards
public void printList(List<?> list) { }
public void addNumbers(List<? super Integer> list) { }
public void processNumbers(List<? extends Number> list) { }
```

### Lambda Expressions
```java
// Functional interface
@FunctionalInterface
interface Calculator {
    int calculate(int a, int b);
}

// Lambda syntax
Calculator add = (a, b) -> a + b;
Calculator multiply = (a, b) -> a * b;

// Method references
list.forEach(System.out::println);
list.stream().map(String::toUpperCase);

// Built-in functional interfaces
Predicate<String> isEmpty = String::isEmpty;
Function<String, Integer> length = String::length;
Consumer<String> printer = System.out::println;
Supplier<String> supplier = () -> "Hello";
```

### Multithreading
```java
// Creating threads
Thread thread = new Thread(() -> {
    System.out.println("Running in thread");
});
thread.start();

// ExecutorService
ExecutorService executor = Executors.newFixedThreadPool(4);
executor.submit(() -> doWork());
executor.shutdown();

// CompletableFuture
CompletableFuture.supplyAsync(() -> fetchData())
    .thenApply(data -> process(data))
    .thenAccept(result -> save(result))
    .exceptionally(ex -> handleError(ex));

// Synchronized
public synchronized void increment() {
    count++;
}
```

## Best Practices

1. Follow **naming conventions** (camelCase, PascalCase)
2. Use **meaningful names** for variables and methods
3. Prefer **composition over inheritance**
4. Program to **interfaces, not implementations**
5. Use **try-with-resources** for auto-closing
6. Prefer **immutable objects** when possible
7. Use **Optional** to avoid null checks

## Resources
- Oracle Java Documentation
- Effective Java (book)
- Java Concurrency in Practice (book)
