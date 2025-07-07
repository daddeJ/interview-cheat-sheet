# 🧵 C# Multi-threading (`Thread`, `Task`, `Parallel`) Cheat Sheet 

---

## 🧵 1. `Thread`

- ✅ **Definition**: Low-level representation of an OS thread in C#.
- 🎯 **Intent**: Manually manage threads (rarely needed with modern `Task`).
- 🔀 **Difference**:
  - More control but more error-prone and expensive.
  - Doesn’t return a value or support cancellation easily.

### 💡 Example:
```csharp
var thread = new Thread(() =>
{
    Console.WriteLine("Running audit on background thread");
    // Simulate heavy work
});
thread.Start();
```

## 🧵 2. `Task`

- ✅ **Definition**: Represents an asynchronous operation that may return a result (`Task<T>`).
- 🎯 **Intent**: Modern, scalable way to run concurrent operations without blocking threads.
- 🔀 **Difference**:
  - Preferred over `Thread`.
  - Integrates with `async/await`.
  - Supports cancellation, continuation, result returning.

### 💡 Example: Run background token cleanup
```csharp
public void StartTokenCleanupJob()
{
    Task.Run(() =>
    {
        Console.WriteLine("Cleaning up expired tokens...");
        Thread.Sleep(2000); // Simulate work
    });
}
```

## 🧵 3. `Parallel`

- ✅ **Definition**: Executes loop iterations in parallel using available CPU cores.
- 🎯 **Intent**: For CPU-bound tasks like hashing many passwords quickly.
- 🔀 **Difference**:
  - Easier for data-parallel scenarios.
  - Less control than `Task` or `Thread`.

### 💡 Example: Hash a batch of passwords
```csharp
var passwords = new[] { "pass1", "pass2", "pass3" };
Parallel.ForEach(passwords, password =>
{
    Console.WriteLine($"Hashing {password} on thread {Thread.CurrentThread.ManagedThreadId}");
});
```

## 🧵 4. `ThreadPool`

- ✅ **Definition**: Provides a pool of threads managed by the runtime for reuse.
- 🎯 **Intent**: Avoid cost of creating/destroying threads repeatedly.
- 🔀 **Difference**:
  - `Task` and `Parallel` use `ThreadPool` under the hood.
  - Less control than `Task` or `Thread`.

### 💡 Example: Hash a batch of passwords
```csharp
ThreadPool.QueueUserWorkItem(_ =>
{
    Console.WriteLine("Queued task for background audit logging");
});
```
## ⚡ Recap: `async` + `await`

- ✅ **Definition**: Allow non-blocking asynchronous code using `Task`.
- 🎯 **Intent**: Keep API fast and responsive (e.g., not block user login request).
- 🔀 **Difference**:
  - `await` makes a task pause without blocking a thread.

**💡 Already shown above — used in:**
```csharp
public async Task<IActionResult> Login(LoginDto dto)
{
    var user = await _authService.ValidateUserAsync(dto.Username, dto.Password);
    ...
}
```

## 🔒 5. `lock` — Synchronization Keyword

- ✅ **Definition**: Prevents multiple threads from accessing a resource simultaneously.
- 🎯 **Intent**: Protect shared state (like a cache or dictionary) from race conditions.
- 🔀 **Difference**:
  - Only works within the same process.
  - Cannot be used across services or distributed systems.

### 💡 Example: Prevent race condition in token cache
```csharp
private static object _lockObj = new();

public void AddToken(string token)
{
    lock (_lockObj)
    {
        // Prevent multiple threads adding to the cache at once
        _tokenCache.Add(token);
    }
}
```

# 🧵 C# Multi-threading Feature Comparison

| **Feature**     | **Use Case**                                  | **Returns Value** | **Auto Thread Management** | **Async Friendly** | **Low-Level Control** |
|-----------------|-----------------------------------------------|-------------------|-----------------------------|---------------------|------------------------|
| `Thread`        | Rare manual threading                         | ❌                | ❌                          | ❌                  | ✅                     |
| `Task`          | Async/await, background operations            | ✅                | ✅                          | ✅                  | ⚠ Medium              |
| `Parallel`      | CPU-bound loops (e.g., `Parallel.For`)        | ❌ (mostly)       | ✅                          | ❌                  | ❌                     |
| `ThreadPool`    | Fire-and-forget, short background operations  | ❌                | ✅                          | ❌                  | ❌                     |
| `async/await`   | I/O-bound operations (API, DB, file, etc.)    | ✅                | ✅                          | ✅                  | ❌                     |
| `lock`          | Protect shared in-memory resources            | N/A               | N/A                         | N/A                 | ✅                     |

---

### 🔎 Notes

- **`Thread`**: Offers full control, used rarely now due to complexity and lack of scalability.
- **`Task`**: Preferred for asynchronous work; integrates well with `async/await`.
- **`Parallel`**: Good for CPU-bound work using multiple cores, like processing large arrays.
- **`ThreadPool`**: Efficient for small background tasks; threads are reused.
- **`async/await`**: Simplifies asynchronous programming, best for I/O-bound operations.
- **`lock`**: Prevents race conditions when accessing shared memory in concurrent scenarios.

