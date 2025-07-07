
# 🌐 ASP.NET Core API Fundamentals Cheat Sheet

---

## 🧱 Controller

**Definition:** A class that handles HTTP requests and returns responses.  
**Intent:** Organize request-handling logic for related endpoints (e.g., `/users`, `/auth`) in one place.

```csharp
[ApiController]
[Route("api/[controller]")]
public class AuthController : ControllerBase
{
    [HttpPost("login")]
    public IActionResult Login(LoginRequest request)
    {
        // Validate user and return JWT
    }
}
```

**Difference:**  
- `ControllerBase` is lighter and used for APIs (no view support).  
- `Controller` includes view support (MVC).

---

## 🔧 Startup.cs or Program.cs

**Definition:** The entry point where you configure services and the request pipeline.  
**Intent:** Set up your app — dependency injection, middleware, routing, etc.

```csharp
builder.Services.AddControllers();
builder.Services.AddScoped<IAuthService, AuthService>();
app.UseAuthentication();
app.UseAuthorization();
```

**Difference:**  
- In .NET 6+, everything is merged into `Program.cs` using the minimal hosting model.

---

## 🛠️ Dependency Injection (DI)

**Definition:** A built-in feature to inject dependencies (services, repositories) at runtime.  
**Intent:** Loosely couple components for better testability and maintainability.

```csharp
public class AuthController
{
    private readonly IAuthService _authService;
    public AuthController(IAuthService authService)
    {
        _authService = authService;
    }
}
```

**Difference:**
- `Scoped`: per request  
- `Transient`: new instance each time  
- `Singleton`: one instance across app

---

## 🔑 Authentication and Authorization

**Definition:**  
- **Authentication:** Who you are  
- **Authorization:** What you're allowed to do  

**Intent:** Secure endpoints in your API.

```csharp
[Authorize(Roles = "Admin")]
[HttpGet("dashboard")]
public IActionResult GetAdminDashboard() => Ok();
```

**Difference:**  
- Authenticate once  
- Authorize every request/resource

---

## 📦 Middleware

**Definition:** Software components that process requests and responses.  
**Intent:** Add cross-cutting features (logging, auth, error handling).

```csharp
app.UseMiddleware<ExceptionHandlingMiddleware>();
```

**Difference:**  
- **Order matters** — e.g., `app.UseRouting()` before `app.UseEndpoints()`.

---

## 🛡️ Model Validation (`[Required]`, `[EmailAddress]`, etc.)

**Definition:** Attributes that validate incoming model data.  
**Intent:** Prevent bad input before reaching business logic.

```csharp
public class LoginRequest
{
    [Required]
    public string Username { get; set; }

    [Required]
    [MinLength(6)]
    public string Password { get; set; }
}
```

**Difference:**  
- Automatic `400 BadRequest` if `[ApiController]` is used.

---

## 🔄 Model Binding vs DTOs

**Definition:**  
- **Model Binding:** Maps request to parameters or objects.  
- **DTO (Data Transfer Object):** Custom model exposing only needed fields.

**Intent:** Control the shape of data going in/out of your API.

```csharp
[HttpPost("register")]
public IActionResult Register(RegisterDto dto) { }
```

**Difference:**  
- DTOs hide domain models and reduce over-posting risks.

---

## 📃 AppSettings.json + IConfiguration

**Definition:** A config file for secrets, keys, connection strings.  
**Intent:** Centralized configuration outside of code.

```json
"Jwt": {
  "Secret": "supersecretkey"
}
```

```csharp
var secret = _configuration["Jwt:Secret"];
```

**Difference:**  
- Can also use User Secrets, Environment Variables, or Azure Key Vault.

---

## 🔌 HttpClient + Typed Clients

**Definition:** Used to call other APIs.  
**Intent:** Communicate between microservices.

```csharp
services.AddHttpClient<IUserService, UserService>();
```

**Difference:**  
- **Named**, **Typed**, and **Factory-created clients** — choose based on reuse/config needs.

---

## 🧪 Swagger (OpenAPI)

**Definition:** API documentation generator.  
**Intent:** Explore and test APIs via browser UI.

```csharp
builder.Services.AddEndpointsApiExplorer();
builder.Services.AddSwaggerGen();
app.UseSwagger();
app.UseSwaggerUI();
```

**Difference:**  
- Useful in dev/test; can be restricted in prod.

---
