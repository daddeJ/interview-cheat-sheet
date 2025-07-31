# Java Programming Terminology Guide

## Abstract class
✅ **Definition**: A class that cannot be instantiated and is meant to be subclassed, often containing abstract methods that subclasses must implement.

🔍 **Example**:
```java
abstract class Animal {
    abstract void makeSound();
    void sleep() { System.out.println("Sleeping..."); }
}

class Dog extends Animal {
    void makeSound() { System.out.println("Woof!"); }
}
```

👍 **When to use / Benefit**: Use when you want to share common code among related classes while forcing subclasses to implement specific methods. Great for template method pattern.

👎 **Common mistake / Pitfall**: Trying to instantiate an abstract class directly (`new Animal()` would cause compilation error). Also, forgetting to implement abstract methods in subclasses.

---

## Abstract method
✅ **Definition**: A method without a body that subclasses of an abstract class must implement.

🔍 **Example**:
```java
abstract class Shape {
    abstract double calculateArea(); // No method body
    abstract void draw();
}
```

👍 **When to use / Benefit**: Forces consistent method signatures across subclasses while allowing different implementations. Ensures contract compliance.

👎 **Common mistake / Pitfall**: Abstract methods cannot be private, static, or final. Forgetting to implement them in concrete subclasses causes compilation errors.

---

## Access modifier
✅ **Definition**: A keyword that defines the scope and visibility of a class, method, or variable (for example, public, private, or protected).

🔍 **Example**:
```java
public class MyClass {
    private int privateVar;      // Only within this class
    protected int protectedVar;  // Same package + subclasses
    public int publicVar;        // Everywhere
    int defaultVar;              // Same package only
}
```

👍 **When to use / Benefit**: Encapsulation and security. Controls what parts of your code other classes can access. Follows principle of least privilege.

👎 **Common mistake / Pitfall**: Making everything public breaks encapsulation. Using protected when private would suffice exposes unnecessary implementation details.

---

## Annotation
✅ **Definition**: A metadata tag in code that provides information to the compiler or at runtime and is often used for configuration or code generation.

🔍 **Example**:
```java
@Override
public String toString() { return "MyObject"; }

@Deprecated
public void oldMethod() { }

@SuppressWarnings("unchecked")
List<String> list = (List<String>) rawList;
```

👍 **When to use / Benefit**: Reduces boilerplate code, provides compile-time checks, enables framework magic (Spring, JUnit), improves code documentation.

👎 **Common mistake / Pitfall**: Overusing annotations can make code hard to understand. Some annotations have runtime overhead. Forgetting retention policies in custom annotations.

---

## Application Programming Interface (API)
✅ **Definition**: A set of rules and tools that allow different software applications to communicate with each other.

🔍 **Example**:
```java
// Using Java Collections API
List<String> names = new ArrayList<>();
names.add("John");  // API method

// Using custom API
PaymentProcessor processor = new PaymentProcessor();
processor.processPayment(amount, cardNumber);  // Your API
```

👍 **When to use / Benefit**: Enables code reusability, abstraction, and integration. Well-designed APIs hide complexity and provide clear contracts.

👎 **Common mistake / Pitfall**: Breaking API compatibility in updates, poor documentation, inconsistent naming conventions, exposing too much internal complexity.

---

## Applet
✅ **Definition**: A small Java program that runs within a web browser or applet viewer.

🔍 **Example**:
```java
import java.applet.Applet;
import java.awt.Graphics;

public class HelloApplet extends Applet {
    public void paint(Graphics g) {
        g.drawString("Hello World!", 20, 20);
    }
}
```

👍 **When to use / Benefit**: Once popular for interactive web content. Platform-independent client-side programming.

👎 **Common mistake / Pitfall**: Largely deprecated due to security concerns. Modern browsers don't support applets. Use modern web technologies instead.

---

## Argument
✅ **Definition**: A value that is passed to a function or method when it is called.

🔍 **Example**:
```java
public void greet(String name, int age) {  // name, age are parameters
    System.out.println("Hello " + name + ", age " + age);
}

greet("Alice", 25);  // "Alice" and 25 are arguments
```

👍 **When to use / Benefit**: Allows methods to work with different data. Makes methods flexible and reusable.

👎 **Common mistake / Pitfall**: Confusing arguments (actual values passed) with parameters (variable names in method signature). Passing wrong types or null values.

---

## Array
✅ **Definition**: A data structure that holds a fixed number of elements of the same type in a contiguous memory location.

🔍 **Example**:
```java
int[] numbers = new int[5];  // Array of 5 integers
numbers[0] = 10;
numbers[1] = 20;

String[] names = {"Alice", "Bob", "Charlie"};  // Initialize with values
System.out.println(names.length);  // 3
```

👍 **When to use / Benefit**: Fast random access (O(1)), memory efficient, good cache locality. Perfect when size is known and fixed.

👎 **Common mistake / Pitfall**: ArrayIndexOutOfBoundsException when accessing invalid indices. Fixed size after creation. Arrays are objects but feel like primitives.

---

## Autoboxing
✅ **Definition**: The automatic conversion of a primitive data type into its corresponding wrapper class object.

🔍 **Example**:
```java
int primitive = 42;
Integer wrapper = primitive;  // Autoboxing: int → Integer

List<Integer> list = new ArrayList<>();
list.add(5);  // Autoboxing: int → Integer

// Unboxing: Integer → int
int value = wrapper;  // Automatic unboxing
```

👍 **When to use / Benefit**: Seamless integration between primitives and collections. Cleaner, more readable code. Enables use of primitives with generics.

👎 **Common mistake / Pitfall**: Performance overhead from boxing/unboxing. NullPointerException when unboxing null wrapper objects. Hidden object creation.

---

## Boolean
✅ **Definition**: A data type that represents one of the two values: true or false.

🔍 **Example**:
```java
boolean isValid = true;
boolean isEmpty = false;

if (isValid && !isEmpty) {
    System.out.println("Processing data");
}

Boolean wrapper = Boolean.valueOf(true);  // Wrapper class
```

👍 **When to use / Benefit**: Perfect for flags, conditions, and binary states. Makes code self-documenting and readable.

👎 **Common mistake / Pitfall**: Using == with Boolean wrapper objects instead of .equals(). Confusing assignment (=) with comparison (==) in conditions.

---

## Break statement
✅ **Definition**: A control flow statement that is used to exit a loop or switch statement prematurely.

🔍 **Example**:
```java
for (int i = 0; i < 10; i++) {
    if (i == 5) {
        break;  // Exit loop when i equals 5
    }
    System.out.println(i);  // Prints 0, 1, 2, 3, 4
}

switch (grade) {
    case 'A': System.out.println("Excellent"); break;
    case 'B': System.out.println("Good"); break;
    default: System.out.println("Try harder");
}
```

👍 **When to use / Benefit**: Early exit from loops when condition is met. Prevents fall-through in switch statements. Improves performance by avoiding unnecessary iterations.

👎 **Common mistake / Pitfall**: Forgetting break in switch cases causes fall-through. Using break in nested loops only exits innermost loop (use labeled break for outer loops).

---

## Bytecode
✅ **Definition**: A low-level, platform-independent code generated by the Java compiler that runs on the Java Virtual Machine (JVM).

🔍 **Example**:
```java
// Java source code
public class Hello {
    public static void main(String[] args) {
        System.out.println("Hello World");
    }
}

// Compiled to bytecode (simplified representation)
// Bytecode instructions like: aload_0, invokevirtual, return
```

👍 **When to use / Benefit**: Platform independence ("write once, run anywhere"), security through JVM verification, optimization opportunities.

👎 **Common mistake / Pitfall**: Bytecode is not human-readable. Reverse engineering is possible. Performance overhead compared to native code.

---

## Casting
✅ **Definition**: The process of converting one data type into another.

🔍 **Example**:
```java
// Implicit casting (widening)
int num = 42;
double d = num;  // int → double (automatic)

// Explicit casting (narrowing)
double pi = 3.14159;
int rounded = (int) pi;  // double → int (manual, loses precision)

// Object casting
Object obj = "Hello";
String str = (String) obj;  // Downcast
```

👍 **When to use / Benefit**: Enables type flexibility, working with inheritance hierarchies, interfacing with APIs that require specific types.

👎 **Common mistake / Pitfall**: ClassCastException with invalid object casts. Data loss in narrowing conversions. Not checking instanceof before casting.

---

## catch block
✅ **Definition**: A block of code used to handle exceptions in a try-catch structure.

🔍 **Example**:
```java
try {
    int result = 10 / 0;  // ArithmeticException
} catch (ArithmeticException e) {
    System.out.println("Cannot divide by zero: " + e.getMessage());
} catch (Exception e) {
    System.out.println("General error: " + e.getMessage());
}
```

👍 **When to use / Benefit**: Graceful error handling, prevents program crashes, allows recovery from errors, provides user-friendly error messages.

👎 **Common mistake / Pitfall**: Catching Exception too broadly, empty catch blocks that hide errors, not logging exceptions, catching and rethrowing without adding value.

---

## Checked exception
✅ **Definition**: An exception must be declared in the method signature or handled using a try-catch block.

🔍 **Example**:
```java
// Must handle or declare
public void readFile() throws IOException {
    FileReader file = new FileReader("data.txt");  // IOException is checked
}

// Or handle with try-catch
public void safeReadFile() {
    try {
        FileReader file = new FileReader("data.txt");
    } catch (IOException e) {
        System.out.println("File not found");
    }
}
```

👍 **When to use / Benefit**: Forces explicit error handling, makes potential failures visible, encourages robust code design.

👎 **Common mistake / Pitfall**: Leads to verbose code, sometimes forces unnecessary exception handling, can be overused making code cluttered.

---

## Class
✅ **Definition**: A blueprint for creating objects and defining attributes (fields) and behaviors (methods).

🔍 **Example**:
```java
public class Car {
    // Fields (attributes)
    private String brand;
    private int year;
    
    // Constructor
    public Car(String brand, int year) {
        this.brand = brand;
        this.year = year;
    }
    
    // Methods (behaviors)
    public void start() {
        System.out.println(brand + " is starting");
    }
}

Car myCar = new Car("Toyota", 2023);  // Create object from class
```

👍 **When to use / Benefit**: Encapsulation, code reusability, modeling real-world entities, organizing related functionality.

👎 **Common mistake / Pitfall**: Creating classes that are too large (violates Single Responsibility Principle), improper encapsulation, not following naming conventions.

---

## ClassLoader
✅ **Definition**: A part of the Java Runtime Environment (JRE) responsible for dynamically loading classes into memory.

🔍 **Example**:
```java
// Getting the ClassLoader
ClassLoader classLoader = MyClass.class.getClassLoader();

// Loading a class dynamically
try {
    Class<?> clazz = classLoader.loadClass("com.example.MyClass");
    Object instance = clazz.newInstance();
} catch (ClassNotFoundException e) {
    System.out.println("Class not found");
}
```

👍 **When to use / Benefit**: Dynamic loading, plugin architectures, hot deployment, custom class loading strategies.

👎 **Common mistake / Pitfall**: ClassNotFoundException, memory leaks with custom ClassLoaders, security issues, complex debugging.

---

## Constructor
✅ **Definition**: A special method that is used to initialize objects when a class is instantiated.

🔍 **Example**:
```java
public class Person {
    private String name;
    private int age;
    
    // Default constructor
    public Person() {
        this.name = "Unknown";
        this.age = 0;
    }
    
    // Parameterized constructor
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
}

Person p1 = new Person();           // Uses default constructor
Person p2 = new Person("Alice", 25); // Uses parameterized constructor
```

👍 **When to use / Benefit**: Ensures objects are properly initialized, enforces required parameters, sets default values.

👎 **Common mistake / Pitfall**: Forgetting to call super() in inheritance, not handling constructor exceptions, creating too many constructor overloads.

---

## continue statement
✅ **Definition**: A control statement that skips the current iteration of a loop and proceeds with the next iteration.

🔍 **Example**:
```java
for (int i = 0; i < 10; i++) {
    if (i % 2 == 0) {
        continue;  // Skip even numbers
    }
    System.out.println(i);  // Prints only odd numbers: 1, 3, 5, 7, 9
}

// In while loop
int count = 0;
while (count < 5) {
    count++;
    if (count == 3) continue;
    System.out.println(count);  // Prints 1, 2, 4, 5
}
```

👍 **When to use / Benefit**: Cleaner code by avoiding nested if statements, skipping invalid data processing, filtering logic within loops.

👎 **Common mistake / Pitfall**: Infinite loops if continue prevents increment operation, confusing logic flow, overuse making code hard to follow.

---

## Data encapsulation
✅ **Definition**: The practice of restricting direct access to object data and allowing manipulation through methods.

🔍 **Example**:
```java
public class BankAccount {
    private double balance;  // Private - cannot be accessed directly
    
    public void deposit(double amount) {  // Controlled access through methods
        if (amount > 0) {
            balance += amount;
        }
    }
    
    public double getBalance() {  // Getter method
        return balance;
    }
}

BankAccount account = new BankAccount();
// account.balance = 1000;  // ERROR - direct access not allowed
account.deposit(1000);      // OK - controlled access
```

👍 **When to use / Benefit**: Data security, controlled access, validation of inputs, easier maintenance and debugging.

👎 **Common mistake / Pitfall**: Over-encapsulation making simple operations complex, not providing necessary getter/setter methods, breaking encapsulation with public fields.

---

## Data hiding
✅ **Definition**: The concept of making class variables private and accessible only through public methods to ensure security.

🔍 **Example**:
```java
public class User {
    private String password;  // Hidden from outside access
    private String email;
    
    public boolean authenticate(String inputPassword) {
        return this.password.equals(inputPassword);  // Controlled access
    }
    
    public void setEmail(String email) {
        if (isValidEmail(email)) {  // Validation before setting
            this.email = email;
        }
    }
    
    private boolean isValidEmail(String email) {
        return email.contains("@");  // Simple validation
    }
}
```

👍 **When to use / Benefit**: Security, prevents unauthorized modification, maintains data integrity, enables validation.

👎 **Common mistake / Pitfall**: Making everything private when some protection levels might be more appropriate, not providing necessary access methods.

---

## Deque (Double-ended queue)
✅ **Definition**: A data structure that allows insertion and deletion from both ends.

🔍 **Example**:
```java
Deque<String> deque = new ArrayDeque<>();

// Add to both ends
deque.addFirst("First");    // [First]
deque.addLast("Last");      // [First, Last]
deque.addFirst("New First"); // [New First, First, Last]

// Remove from both ends
String first = deque.removeFirst();  // "New First"
String last = deque.removeLast();    // "Last"
```

👍 **When to use / Benefit**: Flexible insertion/deletion, can be used as stack or queue, efficient for both operations, palindrome checking.

👎 **Common mistake / Pitfall**: Confusing addFirst/addLast with offer methods, null elements not allowed in some implementations, thread safety issues.

---

## do-while loop
✅ **Definition**: A control structure that executes a block of code at least once before checking the condition.

🔍 **Example**:
```java
int number;
Scanner scanner = new Scanner(System.in);

do {
    System.out.print("Enter a positive number: ");
    number = scanner.nextInt();
    
    if (number <= 0) {
        System.out.println("Please enter a positive number!");
    }
} while (number <= 0);  // Continues until positive number entered

System.out.println("You entered: " + number);
```

👍 **When to use / Benefit**: Guarantees at least one execution, perfect for input validation, menu-driven programs, processing that must happen once.

👎 **Common mistake / Pitfall**: Forgetting the semicolon after while condition, infinite loops due to unchanging condition, less common than regular while loop.

---

## Dynamic binding
✅ **Definition**: The process of resolving method calls at runtime instead of compile time.

🔍 **Example**:
```java
abstract class Animal {
    abstract void makeSound();
}

class Dog extends Animal {
    void makeSound() { System.out.println("Woof!"); }
}

class Cat extends Animal {
    void makeSound() { System.out.println("Meow!"); }
}

Animal pet = new Dog();  // Reference type Animal, object type Dog
pet.makeSound();  // "Woof!" - method resolved at runtime (dynamic binding)

pet = new Cat();
pet.makeSound();  // "Meow!" - different method called at runtime
```

👍 **When to use / Benefit**: Enables polymorphism, flexible code design, runtime decision making, supports design patterns like Strategy.

👎 **Common mistake / Pitfall**: Slight performance overhead, can make debugging harder, method resolution might not be obvious from code inspection.

---

## Enumeration (enum)
✅ **Definition**: A special data type used to define a set of named constants.

🔍 **Example**:
```java
public enum Day {
    MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY
}

public enum Priority {
    LOW(1), MEDIUM(2), HIGH(3);
    
    private int value;
    Priority(int value) { this.value = value; }
    public int getValue() { return value; }
}

Day today = Day.MONDAY;
Priority taskPriority = Priority.HIGH;

switch (today) {
    case MONDAY: System.out.println("Start of work week"); break;
    case FRIDAY: System.out.println("TGIF!"); break;
}
```

👍 **When to use / Benefit**: Type safety, readable code, prevents invalid values, compile-time checking, can have methods and fields.

👎 **Common mistake / Pitfall**: Using ordinal() for business logic (fragile), comparing with == instead of equals() when overridden, serialization issues.

---

## Exception
✅ **Definition**: An event that disrupts the normal execution of a program, requiring special handling.

🔍 **Example**:
```java
public class Calculator {
    public int divide(int a, int b) throws ArithmeticException {
        if (b == 0) {
            throw new ArithmeticException("Division by zero not allowed");
        }
        return a / b;
    }
}

try {
    Calculator calc = new Calculator();
    int result = calc.divide(10, 0);  // Throws ArithmeticException
} catch (ArithmeticException e) {
    System.out.println("Error: " + e.getMessage());
}
```

👍 **When to use / Benefit**: Robust error handling, separates error handling from business logic, provides meaningful error information.

👎 **Common mistake / Pitfall**: Catching too broad exceptions, empty catch blocks, using exceptions for control flow, not cleaning up resources.

---

## Exception handling
✅ **Definition**: A programming mechanism for handling runtime errors and ensuring smooth program execution.

🔍 **Example**:
```java
public void processFile(String filename) {
    FileReader file = null;
    try {
        file = new FileReader(filename);
        // Process file
    } catch (FileNotFoundException e) {
        System.out.println("File not found: " + filename);
    } catch (IOException e) {
        System.out.println("Error reading file: " + e.getMessage());
    } finally {
        if (file != null) {
            try {
                file.close();
            } catch (IOException e) {
                System.out.println("Error closing file");
            }
        }
    }
}
```

👍 **When to use / Benefit**: Prevents crashes, graceful degradation, better user experience, separates normal and error code paths.

👎 **Common mistake / Pitfall**: Swallowing exceptions, not logging properly, resource leaks, over-catching exceptions, poor error messages.

---

## Explicit casting
✅ **Definition**: A type conversion that requires the programmer to specify the target type.

🔍 **Example**:
```java
// Narrowing primitive conversion
double pi = 3.14159;
int whole = (int) pi;  // Explicit cast, loses decimal part

// Object casting
Object obj = "Hello World";
String str = (String) obj;  // Explicit downcast

// Potential data loss
long bigNum = 300L;
byte small = (byte) bigNum;  // May overflow, explicit cast required

// Safe casting with instanceof
if (obj instanceof String) {
    String safeStr = (String) obj;  // Safe explicit cast
}
```

👍 **When to use / Benefit**: Precise control over conversions, working with polymorphism, interfacing with legacy code.

👎 **Common mistake / Pitfall**: ClassCastException without instanceof check, data loss in numeric conversions, unnecessary casting.

---

## Extends keyword
✅ **Definition**: A keyword used in Java for class inheritance, allowing a subclass to inherit from a superclass.

🔍 **Example**:
```java
class Vehicle {
    protected String brand;
    
    public void start() {
        System.out.println("Vehicle starting");
    }
}

class Car extends Vehicle {  // Car inherits from Vehicle
    private int doors;
    
    public Car(String brand, int doors) {
        this.brand = brand;  // Inherited field
        this.doors = doors;
    }
    
    @Override
    public void start() {  // Override inherited method
        System.out.println(brand + " car starting");
    }
}

Car myCar = new Car("Toyota", 4);
myCar.start();  // "Toyota car starting"
```

👍 **When to use / Benefit**: Code reusability, "is-a" relationships, polymorphism, hierarchical organization of classes.

👎 **Common mistake / Pitfall**: Deep inheritance hierarchies, violating Liskov Substitution Principle, using inheritance when composition is better.

---

## final class
✅ **Definition**: A class that cannot be extended or subclassed.

🔍 **Example**:
```java
final class ImmutablePoint {
    private final int x, y;
    
    public ImmutablePoint(int x, int y) {
        this.x = x;
        this.y = y;
    }
    
    public int getX() { return x; }
    public int getY() { return y; }
}

// class ExtendedPoint extends ImmutablePoint { }  // Compilation error!

// Famous examples: String, Integer, etc.
final class String { /* ... */ }  // Cannot be subclassed
```

👍 **When to use / Benefit**: Security, immutability, performance optimizations, API design (like String class).

👎 **Common mistake / Pitfall**: Overuse limits flexibility, makes testing harder (can't mock), reduces extensibility.

---

## final keyword
✅ **Definition**: A keyword used to define constants, prevent method overriding, or restrict class inheritance.

🔍 **Example**:
```java
class Example {
    // final variable (constant)
    private final int MAX_SIZE = 100;
    private final List<String> names = new ArrayList<>();  // Reference is final
    
    // final method (cannot be overridden)
    public final void criticalMethod() {
        System.out.println("This cannot be overridden");
    }
    
    public Example(int size) {
        // MAX_SIZE = size;  // Error - cannot reassign final variable
        names.add("John");   // OK - can modify object, not reference
    }
}

final class FinalClass { }  // Cannot be extended
```

👍 **When to use / Benefit**: Constants, immutable references, API design, performance hints for JVM, thread safety.

👎 **Common mistake / Pitfall**: Confusing final reference with immutable object, overusing final making code inflexible, blank final variables must be initialized.

---

## finally block
✅ **Definition**: A block of code that executes after a try-catch structure, regardless of whether an exception occurs.

🔍 **Example**:
```java
public void processFile(String filename) {
    FileInputStream file = null;
    try {
        file = new FileInputStream(filename);
        // Process file
        int data = file.read();
    } catch (IOException e) {
        System.out.println("Error: " + e.getMessage());
        return;  // Even with return, finally still executes
    } finally {
        // Always executes (unless JVM crash)
        if (file != null) {
            try {
                file.close();  // Cleanup resources
            } catch (IOException e) {
                System.out.println("Error closing file");
            }
        }
        System.out.println("Cleanup completed");
    }
}
```

👍 **When to use / Benefit**: Resource cleanup, logging, guaranteed execution of critical code, proper resource management.

👎 **Common mistake / Pitfall**: Exception in finally can mask original exception, returning from finally overrides try/catch returns, not handling exceptions in finally.

---

## Float
✅ **Definition**: A primitive data type that represents decimal numbers with single precision.

🔍 **Example**:
```java
float price = 19.99f;  // Note the 'f' suffix
float temperature = -15.5F;  // 'F' also works
float result = 10.0f / 3.0f;  // 3.3333333

// Wrapper class
Float wrapperFloat = Float.valueOf(25.5f);
float primitiveFloat = wrapperFloat.floatValue();

// Precision issues
float a = 0.1f;
float b = 0.2f;
float sum = a + b;  // May not exactly equal 0.3f
```

👍 **When to use / Benefit**: Memory efficient (4 bytes vs 8 for double), sufficient precision for many applications, graphics programming.

👎 **Common mistake / Pitfall**: Precision errors in calculations, comparing floats with ==, forgetting 'f' suffix, loss of precision in arithmetic.

---

## for loop
✅ **Definition**: A control structure used to iterate over a range of values with a specified condition.

🔍 **Example**:
```java
// Traditional for loop
for (int i = 0; i < 5; i++) {
    System.out.println("Count: " + i);
}

// Enhanced for loop (for-each)
String[] names = {"Alice", "Bob", "Charlie"};
for (String name : names) {
    System.out.println("Name: " + name);
}

// Multiple variables
for (int i = 0, j = 10; i < j; i++, j--) {
    System.out.println(i + " " + j);
}

// Nested loops
for (int row = 0; row < 3; row++) {
    for (int col = 0; col < 3; col++) {
        System.out.print("(" + row + "," + col + ") ");
    }
    System.out.println();
}
```

👍 **When to use / Benefit**: Clear iteration logic, compact syntax, enhanced for-each for collections, well-understood pattern.

👎 **Common mistake / Pitfall**: Off-by-one errors, infinite loops, modifying collection during for-each iteration, complex nested loops.

---

## Garbage collection
✅ **Definition**: The automatic process of reclaiming unused memory in Java to prevent memory leaks.

🔍 **Example**:
```java
public void createObjects() {
    for (int i = 0; i < 1000; i++) {
        String temp = new String("Object " + i);  // Objects created
        // temp goes out of scope, eligible for GC
    }
    // Suggest garbage collection (not guaranteed)
    System.gc();  // Usually not recommended
}

// Objects become eligible for GC when:
String str = new String("Hello");
str = null;  // Original "Hello" object now eligible for GC

List<String> list = new ArrayList<>();
list.add("Data");
list = null;  // ArrayList and its contents eligible for GC
```

👍 **When to use / Benefit**: Automatic memory management, prevents memory leaks, simplifies programming, handles complex object graphs.

👎 **Common mistake / Pitfall**: Assuming System.gc() forces collection, memory leaks through static references, performance impact during GC cycles.

---

## Generic class
✅ **Definition**: A class that can work with different data types using type parameters.

🔍 **Example**:
```java
// Generic class definition
public class Box<T> {
    private T content;
    
    public void set(T content) {
        this.content = content;
    }
    
    public T get() {
        return content;
    }
}

// Usage with different types
Box<String> stringBox = new Box<>();
stringBox.set("Hello");
String value = stringBox.get();  // No casting needed

Box<Integer> intBox = new Box<>();
intBox.set(42);
Integer number = intBox.get();

// Multiple type parameters
public class Pair<T, U> {
    private T first;
    private U second;
    
    public Pair(T first, U second) {
        this.first = first;
        this.second = second;
    }
}
```

👍 **When to use / Benefit**: Type safety at compile time, eliminates casting, code reusability, better documentation through types.

👎 **Common mistake / Pitfall**: Type erasure at runtime, cannot create arrays of generic types, complex wildcard syntax, raw type warnings.

---
