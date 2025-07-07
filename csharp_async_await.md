# ⚙️ C# `async/await` and `delegate` (with Microservice Context)

---

## ⚡ `async` / `await` — Asynchronous Programming

### 1. `async`
- ✅ **Definition**: Marks a method that contains `await` and will run asynchronously.
- 🎯 **Intent**: Prevent blocking of threads (like the request thread in web APIs).
- 🔀 **Difference**:
  - `async` by itself does *not* make a method run in the background; it enables `await` to be used inside.
  - Works with `Task`, `Task<T>`, and `ValueTask`.

---

### 2. `await`
- ✅ **Definition**: Pauses execution until the awaited task completes, without blocking the thread.
- 🎯 **Intent**: Wait for a non-blocking operation like I/O (e.g., database, API call).
- 🔀 **Difference**:
  - Unlike `.Wait()` or `.Result`, `await` doesn't block the thread and avoids deadlocks in ASP.NET.

---

### 💡 Example: Login + JWT + Audit Logging

```csharp
public class AuthController : ControllerBase
{
    private readonly IAuthService _authService;

    public AuthController(IAuthService authService)
    {
        _authService = authService;
    }

    [HttpPost("login")]
    public async Task<IActionResult> Login([FromBody] LoginRequestDto request)
    {
        // 🎯 Non-blocking database validation
        var user = await _authService.ValidateUserAsync(request.Username, request.Password);

        if (user == null)
            return Unauthorized();

        // 🎯 Non-blocking JWT generation and email sending
        var token = await _authService.GenerateJwtTokenAsync(user);
        await _authService.SendLoginNotificationEmailAsync(user);

        return Ok(new { token });
    }
}
```
## 🧬 delegate — Method Reference Type

### 3. `delegate`
- ✅ **Definition**: A type that holds a reference to a method with a matching signature.
- 🎯 **Intent**: Allow flexible execution of callbacks, strategies, or event handlers.
- 🔀 **Difference**:
  - Unlike interfaces, you can pass methods as parameters directly.
  - Basis for `event`, `Func<>`, `Action<>`, and `Predicate<>`.

---

### 💡 Example: Login + JWT + Audit Logging

```csharp
// Step 1: Declare delegate
public delegate void AuditLogger(string message);

// Step 2: Define reusable logger methods
public class LoggerStrategies
{
    public static void LogToFile(string message) => File.AppendAllText("audit.log", message + "\n");

    public static void LogToDatabase(string message)
    {
        // simulate insert log into Audit table
        Console.WriteLine("Saved to DB: " + message);
    }
}

// Step 3: Use delegate to switch behavior
public class LoginAuditService
{
    private readonly AuditLogger _logger;

    public LoginAuditService(AuditLogger logger)
    {
        _logger = logger;
    }

    public void LogLogin(string username)
    {
        _logger($"User {username} logged in at {DateTime.UtcNow}");
    }
}
```

### 💡 Example Usage

```csharp
var auditToDb = new LoginAuditService(LoggerStrategies.LogToDatabase);
auditToDb.LogLogin("johndoe");

var auditToFile = new LoginAuditService(LoggerStrategies.LogToFile);
auditToFile.LogLogin("janedoe");
```

## 🔄 Related Delegates

### 1. `delegate`
  - Signature Example: `public delegate int MathOp(int x, int y)`
  - Description: Custom delegate type

### 2. `Action<T>`
  - Signature Example: `Action<string> log = Console.WriteLine`
  - Description: No return type

### 3. `Func<T>`
  - Signature Example: `Func<int, int, int> add = (x, y) => x + y`
  - Description: Returns a value

### 4. `Predicate<T>`
  - Signature Example: `Predicate<string> check = x => x.Contains("auth")`
  - Description: Returns `bool`
