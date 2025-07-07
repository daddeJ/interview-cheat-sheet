# 🔐 C# Access Modifiers & Common Keywords (with Microservice Context)

This cheat sheet explains access modifiers and keywords in C# through the lens of a real-world microservice, such as `UserAuthMicroservice`.

Each item includes:
- ✅ Definition
- 🎯 Intent (why it's used)
- 🔀 Difference (vs similar terms)
- 💡 Real Example (applied to `UserAuthMicroservice`)

---

## 🧱 Access Modifiers

### 1. `public`
- ✅ Allows access from anywhere.
- 🎯 Used for API endpoints, service interfaces, or DTOs shared across projects.
- 🔀 Most open access modifier.
- 💡 **Example**:
```csharp
public class AuthController : ControllerBase
{
    [HttpPost("login")]
    public IActionResult Login([FromBody] LoginRequestDto request)
    {
        // Call authentication service
    }
}
```
### 2. `private`
- ✅ Restricts access to the same class.
- 🎯 Hides implementation details like helper methods or internal state.
- 🔀 Most restrictive.
- 💡 **Example**:
```csharp
public class JwtTokenService
{
    private string GenerateSecretKey()
    {
        // Hidden logic for security reasons
    }
}
```
### 3. `protected`
- ✅ Access from within class and derived classes.
- 🎯 Allow customization by inheritance but keep encapsulation.
- 🔀 More open than private, but not public.
- 💡 **Example**:
```csharp
public abstract class BaseAuthHandler
{
    protected ClaimsPrincipal DecodeToken(string token)
    {
        // Shared by all auth handlers
    }
}
```
### 4. `internal`
- ✅ Access within the same assembly only.
- 🎯 Limit visibility to the project scope (e.g., hide service from consumers).
- 🔀 Invisible from other projects even if referenced.
- 💡 **Example**:
```csharp
internal class PasswordHasher
{
    public string Hash(string password) { ... }
}
```
### 5. `protected internal`
- ✅ Accessible within the same assembly or from derived types in other assemblies.
- 🎯 Flexibly expose logic for reuse in other services within the company.
- 🔀 More open than `protected` or `internal` alone.
- 💡 **Example**:
```csharp
protected internal void LogAudit(string action) { ... }
```
### 6. `private protected`
- ✅ Accessible only in the same assembly and only by derived types.
- 🎯 Restrict usage even more tightly to internal inheritance scenarios.
- 🔀 C# 7.2 feature.
- 💡 **Example**:
```csharp
private protected void TrackSecurityBreach() { ... }
```

## 🔑 Common Keywords

### 7. `static`
- ✅ Belongs to the type, not instance.
- 🎯 Share utility functions or global state.
- 🔀 Cannot access instance members.
- 💡 **Example**:
```csharp
public static class PasswordPolicy
{
    public static int MinimumLength => 8;
}
```
### 8. `const`
- ✅ Compile-time constant.
- 🎯 Store settings that don’t change (e.g., claim keys).
- 🔀 Must assign at declaration.
- 💡 **Example**:
```csharp
public class ClaimsConstants
{
    public const string Role = "role";
}
```
### 9. `readonly`
- ✅ Can only be set during declaration or constructor.
- 🎯 For immutable fields like tokens, keys, or service IDs.
- 🔀 Can be runtime-defined.
- 💡 **Example**:
```csharp
public class JwtTokenService
{
    private readonly IConfiguration _config;

    public JwtTokenService(IConfiguration config)
    {
        _config = config;
    }
}
```
### 10. `virtual`
- ✅ Allows override in derived classes.
- 🎯 Support polymorphic behavior (custom login flows, etc.).
- 🔀 Optional override.
- 💡 **Example**:
```csharp
public class UserAuthService
{
    public virtual bool ValidateUser(string username, string password)
    {
        return true;
    }
}
```
### 11. `override`
- ✅ Replaces base class method.
- 🎯 Provide custom behavior (e.g., extend validation).
- 🔀 Must match a virtual/abstract method.
- 💡 **Example**:
```csharp
public class AdvancedUserAuthService : UserAuthService
{
    public override bool ValidateUser(string username, string password)
    {
        // Additional MFA validation
        return base.ValidateUser(username, password) && CheckMFA();
    }
}
```
### 12. `abstract`
- ✅ Forces implementation in derived class.
- 🎯 Base contracts for services.
- 🔀 Cannot be instantiated.
- 💡 **Example**:
```csharp
public abstract class TokenGenerator
{
    public abstract string Generate(string userId);
}
```
### 13. `sealed`
- ✅ Prevents inheritance or further overrides.
- 🎯 Lock down security-sensitive classes.
- 🔀 Opposite of virtual.
- 💡 **Example**:
```csharp
public sealed class TokenEncryptionService
{
    public string Encrypt(string token) => ...;
}
```
### 14. `new` (method hiding)
- ✅ Hides base class member.
- 🎯 Use only when intentional.
- 🔀 No runtime polymorphism.
- 💡 **Example**:
```csharp
public class UserLogger
{
    public void Log(string msg) => Console.WriteLine(msg);
}

public class SecureUserLogger : UserLogger
{
    public new void Log(string msg) => Console.WriteLine("SECURE: " + msg);
}
```
