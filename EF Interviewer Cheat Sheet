# EF Interviewer Cheat Sheet

## ✅ Entity Framework Core (EF)

### Important EF Core Packages

| Package                                 | Purpose                                                   |
| --------------------------------------- | --------------------------------------------------------- |
| Microsoft.EntityFrameworkCore           | Core ORM functionality                                    |
| Microsoft.EntityFrameworkCore.SqlServer | SQL Server provider                                       |
| Microsoft.EntityFrameworkCore.Tools     | CLI tools for migration, scaffolding                      |
| Microsoft.EntityFrameworkCore.Design    | Needed for design-time services (scaffolding, migrations) |
| Microsoft.EntityFrameworkCore.InMemory  | For unit testing                                          |

### EF Core Terms

| Term         | Intention                               | Comparison                   | Example                                 | Simple Interview Definition                                         |
| ------------ | --------------------------------------- | ---------------------------- | --------------------------------------- | ------------------------------------------------------------------- |
| `DbContext`  | Represents a session with the database. | vs direct SQL or ADO.NET     | `public class AppDbContext : DbContext` | “`DbContext` is like a gatekeeper for the database.”                |
| `DbSet<T>`   | Represents a collection/table.          | like a table in a database   | `DbSet<User> Users { get; set; }`       | “`DbSet` maps your entity class to a table.”                        |
| Migration    | Tracks schema changes over time.        | vs manual DB changes         | `Add-Migration InitialCreate`           | “Migrations update your database structure through code.”           |
| Fluent API   | Configure entity behavior via code.     | vs Data Annotations          | `.HasKey(e => e.Id)`                    | “Fluent API configures database rules in C# instead of attributes.” |
| Lazy Loading | Delay loading related data.             | vs eager or explicit loading | `virtual ICollection<Post> Posts`       | “Lazy loading only loads related data when needed.”                 |

---

## 🔄 EF Core Lifecycle (Commands)

| Step             | Command                         | Intention                               |
| ---------------- | ------------------------------- | --------------------------------------- |
| Add Migration    | `dotnet ef migrations add Init` | Create migration based on model changes |
| Apply Migration  | `dotnet ef database update`     | Apply pending migrations to DB          |
| Remove Migration | `dotnet ef migrations remove`   | Undo last migration (before update)     |
| Scaffold Model   | `dotnet ef dbcontext scaffold`  | Reverse engineer (DB-first)             |

---

## ⚙️ LINQ & Querying

| Query              | Purpose                 | Example                                   |
| ------------------ | ----------------------- | ----------------------------------------- |
| `Where()`          | Filter data             | `db.Users.Where(u => u.Age > 18)`         |
| `Select()`         | Project specific fields | `db.Users.Select(u => u.Name)`            |
| `Include()`        | Eager loading           | `db.Posts.Include(p => p.Comments)`       |
| `FirstOrDefault()` | Get first match         | `db.Users.FirstOrDefault(u => u.Id == 1)` |

---

## 🧪 EF Core in Unit Testing

| Tool                      | Purpose                              |
| ------------------------- | ------------------------------------ |
| `InMemoryDatabase`        | Simulate DB in memory for fast tests |
| `DbContextOptionsBuilder` | Configure test context               |
| Mocking Repositories      | Decouple logic from EF for testing   |

---

## 🔐 EF Relationships

| Type         | Example            | Configuration                                       |
| ------------ | ------------------ | --------------------------------------------------- |
| One-to-Many  | Author -> Posts    | `modelBuilder.Entity<Post>().HasOne(p => p.Author)` |
| Many-to-Many | Student <-> Course | Implicit with collection properties                 |
| One-to-One   | User -> Profile    | Use `.WithOne()` and `.HasForeignKey<>()`           |

---

## ⚠️ Common EF Core Errors & Troubleshooting

| Error                                           | Cause                            | Fix                                                    |
| ----------------------------------------------- | -------------------------------- | ------------------------------------------------------ |
| "No parameterless constructor"                  | EF can’t create object           | Add default constructor or inject via DI               |
| "The instance of entity type cannot be tracked" | Multiple instances being tracked | Use `.AsNoTracking()` or attach manually               |
| "Unable to create object of type DbContext"     | Missing design-time factory      | Implement `IDesignTimeDbContextFactory` for migrations |

---

## 🆚 Code-First vs Database-First

| Approach   | Pros                            | Cons                               |
| ---------- | ------------------------------- | ---------------------------------- |
| Code-First | Full control, versioned in code | Needs discipline with migrations   |
| DB-First   | Quick setup if DB exists        | Harder to customize, less flexible |

---
