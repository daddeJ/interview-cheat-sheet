# Java Glossary with Examples, Benefits, and Pitfalls

---

## ✅ Immutable Object

**📘 Definition**  
An object whose state cannot be changed after creation.

**🔍 Example**
```java
public final class Person {
    private final String name;

    public Person(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }
}
```

**👍 When to use**
- When you want **thread safety** without synchronization
- Ideal for **value objects** like `Money`, `Point`, etc.
- Helps avoid bugs due to unintended side effects

**👎 Common pitfalls**
- Forgetting defensive copies for mutable fields (like `List`, `Date`)
- Misunderstanding `final` as immutability (only makes the reference constant)

---

## ✅ Iterator

**📘 Definition**  
An object that provides a way to traverse elements in a collection sequentially.

**🔍 Example**
```java
List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
Iterator<String> it = names.iterator();

while (it.hasNext()) {
    System.out.println(it.next());
}
```

**👍 When to use**
- When you need a generic way to loop through a collection
- Useful for hiding collection implementation details

**👎 Common pitfalls**
- Using `next()` without checking `hasNext()` → may cause `NoSuchElementException`
- Modifying a collection while iterating without using `Iterator.remove()` → `ConcurrentModificationException`

---

## ✅ Abstract Class

**📘 Definition**  
A class that cannot be instantiated and is meant to be subclassed. May contain abstract methods.

**🔍 Example**
```java
public abstract class Animal {
    public abstract void makeSound();
}

public class Dog extends Animal {
    public void makeSound() {
        System.out.println("Bark");
    }
}
```

**👍 When to use**
- When you want to define a common template but allow custom behavior in subclasses
- Good for partial implementations

**👎 Common pitfalls**
- Confusing with interfaces — use abstract class when shared code is needed
- Trying to instantiate an abstract class directly (compiler error)

---

## ✅ Mutable Object

**📘 Definition**  
An object whose internal state can be changed after it is created.

**🔍 Example**
```java
public class Person {
    private String name;

    public void setName(String name) {
        this.name = name;
    }
}
```

**👍 When to use**
- When object data must change over time (like UI settings, models in a form)

**👎 Common pitfalls**
- Can lead to bugs if shared across threads or methods carelessly
- Unintentional side effects due to hidden state changes

---

## ✅ Autoboxing

**📘 Definition**  
The automatic conversion of a primitive type to its wrapper class.

**🔍 Example**
```java
List<Integer> nums = new ArrayList<>();
nums.add(10); // 10 is autoboxed from int to Integer
```

**👍 When to use**
- Allows primitive types to work with collections and generics

**👎 Common pitfalls**
- Can lead to unnecessary object creation and performance hits in tight loops

---