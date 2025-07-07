
# ⚡ Func, Action, Predicate in C# (LINQ-style)

These are built-in delegates used heavily in **LINQ** and **functional programming**. Each has a different purpose:

---

## ✅ `Func<T, TResult>`

### 🔹 Definition
A delegate that **takes zero or more input parameters** and **returns a value**.

### 🎯 Intent
Used to **transform**, **filter**, or **project** data with a result.  
✅ Common in `.Select()`, `.Where()`, `.Aggregate()`, etc.

### 🧪 Syntax
```csharp
Func<int, string> toString = num => $"Value: {num}";
Console.WriteLine(toString(5)); // Output: Value: 5
```

### 🧰 LINQ Example
```csharp
var users = new List<User> {
    new User { Name = "Alice", Age = 25 },
    new User { Name = "Bob", Age = 30 }
};

var names = users.Select(user => user.Name).ToList();
// user => user.Name is a Func<User, string>
```

---

## 🔄 `Action<T>`

### 🔹 Definition
A delegate that **takes zero or more parameters** and **returns void**.

### 🎯 Intent
Used to perform **side-effects** (e.g., logging, printing) without returning a result.  
✅ Common in `.ForEach()` (on `List<T>`), not standard LINQ.

### 🧪 Syntax
```csharp
Action<string> print = message => Console.WriteLine(message);
print("Hello!"); // Output: Hello!
```

### 🧰 LINQ-style Example
```csharp
users.ForEach(user => Console.WriteLine(user.Name));
// user => Console.WriteLine(user.Name) is an Action<User>
```

---

## 🔍 `Predicate<T>`

### 🔹 Definition
A delegate that takes **one parameter** and returns a **bool**.

### 🎯 Intent
Used for **checking conditions** in filtering or matching scenarios.  
✅ Used in `.Find()`, `.Exists()`, or compatible with `Func<T, bool>` in LINQ.

### 🧪 Syntax
```csharp
Predicate<int> isEven = number => number % 2 == 0;
bool result = isEven(4); // true
```

### 🧰 LINQ-compatible Example
```csharp
var evenNumbers = numbers.Where(num => num % 2 == 0).ToList();
// num => num % 2 == 0 is a Func<int, bool>, compatible with Predicate<int>
```

---

## 🔁 Differences Summary Table

| **Delegate**      | **Parameters**     | **Returns** | **Use Case**                 | **LINQ Usage**                    |
|-------------------|--------------------|-------------|-------------------------------|------------------------------------|
| `Func<T, TResult>`| 0 or more          | ✅ Yes      | Transform or project data     | `.Select()`, `.Where()`, `.Any()`  |
| `Action<T>`       | 0 or more          | ❌ No       | Perform side-effects          | `.ForEach()` (on `List<T>`)        |
| `Predicate<T>`    | 1                  | ✅ `bool`   | Conditional filtering         | `.Find()`, `.Exists()`             |

---

### 📝 Tips

- `Func<T, TResult>` = "Input ➜ Output"
- `Action<T>` = "Just do something"
- `Predicate<T>` = "Check if true/false"
