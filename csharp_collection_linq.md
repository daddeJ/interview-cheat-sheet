# 📚 C# Collections & LINQ Cheat Sheet  

---

## 🧺 C# COLLECTION TYPES

### 1. `List<T>`
- ✅ A dynamic array that grows as needed.
- 🎯 Store ordered, index-accessible collections like user sessions.
- 🔀 Unlike arrays, `List<T>` is resizable and has many helper methods.
- 💡 **Example**:
```csharp
var activeUsers = new List<string> { "alice", "bob" };
activeUsers.Add("charlie");
```

### 2. `Dictionary<TKey, TValue>`
- ✅ A key-value pair collection for fast lookups.
- 🎯 Map user IDs to their session tokens.
- 🔀 Faster lookup than `List<T>` for search by key.
- 💡 **Example**:
```csharp
var tokenStore = new Dictionary<string, string>();
tokenStore["user1"] = "jwt-token-abc123";
```

### 3. `HashSet<T>`
- ✅ An unordered collection that contains only unique values.
- 🎯 Track unique logins or blocked IPs.
- 🔀 No duplicate values, faster for existence checks than `List<T>`.
- 💡 **Example**:
```csharp
var tokenStore = new Dictionary<string, string>();
tokenStore["user1"] = "jwt-token-abc123";
```

### 4. `Queue<T>`
- ✅ FIFO (first-in, first-out) collection.
- 🎯 Process email verifications or login events in order.
- 🔀 Opposite of `Stack<T>` (LIFO).
- 💡 **Example**:
```csharp
var loginQueue = new Queue<string>();
loginQueue.Enqueue("user1");
var nextLogin = loginQueue.Dequeue();
```

### 5. `Stack<T>`
- ✅ LIFO (last-in, first-out) collection.
- 🎯 Store undo history or temporary roles.
- 🔀 Opposite of `Queue<T>`.
- 💡 **Example**:
```csharp
var mfaStack = new Stack<string>();
mfaStack.Push("OTP1");
mfaStack.Push("OTP2");
var latestOTP = mfaStack.Pop();
```

## 🔍 LINQ (Language Integrated Query)

### 6. `Where`
- ✅ Filters a collection based on a condition.
- 🎯 Get only active users, or only users with a certain role.
- 🔀 Similar to SQL `WHERE`.
- 💡 **Example**:
```csharp
var activeUsers = users.Where(u => u.IsActive);
```

### 7. `Select`
- ✅ Projects each element into a new form.
- 🎯 Convert user entities into DTOs or just get usernames.
- 🔀 Similar to SQL `SELECT`.
- 💡 **Example**:
```csharp
var activeUsers = users.Where(u => u.IsActive);
```

### 8. `FirstOrDefault`
- ✅ Returns the first matching item or null if none.
- 🎯 Get first match safely.
- 🔀 Safer than `First` which throws if not found.
- 💡 **Example**:
```csharp
var user = users.FirstOrDefault(u => u.Email == input.Email);
```

### 9. `Any`
- ✅ Checks if any element matches a condition.
- 🎯 Check if a user exists or has a role.
- 🔀 Boolean return, fast check.
- 💡 **Example**:
```csharp
bool hasAdmin = users.Any(u => u.Role == "admin");
```

### 10. `All`
- ✅ Checks if all elements match a condition.
- 🎯 Confirm all users passed MFA.
- 🔀 Returns true only if every item passes the condition.
- 💡 **Example**:
```csharp
bool allPassed = users.All(u => u.MfaVerified);
```

### 11. `Count`
- ✅ Returns how many items are in a collection (with or without condition).
- 🎯 Count number of logged-in users or failed attempts.
- 💡 **Example**:
```csharp
int failedLogins = loginAttempts.Count(a => !a.Success);
```

### 12. `GroupBy`
- ✅ Groups elements by a key.
- 🎯 Group users by role, status, or IP.
- 🔀 Returns `IGrouping<TKey, TElement>`.
- 💡 **Example**:
```csharp
var groupedByRole = users.GroupBy(u => u.Role);
foreach (var group in groupedByRole)
{
    Console.WriteLine($"Role: {group.Key} - Count: {group.Count()}");
}
```

### 13. `OrderBy` / `OrderByDescending`
- ✅ Sorts a collection based on a key.
- 🎯 Sort users by login time, activity level.
- 🔀 Use `ThenBy()` for secondary sorting.
- 💡 **Example**:
```csharp
var recentLogins = users.OrderByDescending(u => u.LastLoginDate);
```

# 🔄 C# Collections & LINQ Summary Table

## 📦 Collection Types

| **Type**              | **Use For**                            | **Unique?** | **Ordered?** | **Key Access** |
|-----------------------|----------------------------------------|-------------|---------------|----------------|
| `List<T>`             | General purpose lists                  | ❌          | ✅            | ❌              |
| `Dictionary<K,V>`     | Fast lookups by key                    | ✅          | ❌            | ✅              |
| `HashSet<T>`          | Uniqueness + fast existence check      | ✅          | ❌            | ❌              |
| `Queue<T>`            | FIFO processing queue                  | ❌          | ✅            | ❌              |
| `Stack<T>`            | LIFO behavior                          | ❌          | ✅            | ❌              |

---

## 🔍 LINQ Methods

| **LINQ Method**       | **Use For**                          | **Output Type**                |
|-----------------------|--------------------------------------|--------------------------------|
| `Where`               | Filtering                            | `IEnumerable<T>`               |
| `Select`              | Projection/transformation            | `IEnumerable<TResult>`         |
| `FirstOrDefault`      | Get first item or null               | `T`                            |
| `Any`                 | Boolean check for existence          | `bool`                         |
| `All`                 | Boolean check for universal match    | `bool`                         |
| `GroupBy`             | Aggregation/grouping                 | `IEnumerable<IGrouping>`       |
| `OrderBy`             | Sorting                              | `IOrderedEnumerable<T>`        |

---

### 📝 Quick Tips

- `List<T>` is great for dynamic arrays with order.
- `Dictionary<K,V>` provides fast lookup by key but does not preserve insertion order.
- `HashSet<T>` is best for ensuring no duplicates and quick `Contains` checks.
- `Queue<T>` is useful for background job queues.
- `Stack<T>` is great for undo operations or recursive-style logic.
- LINQ makes querying collections more expressive and readable.

