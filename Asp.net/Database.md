# 1️⃣Packages
---
| | Name | Version |
|-|-|-|
|1| Entity Framework | 6.4.4|
| 2 | Microsoft.AspNet.Identity.EntityFramework | 2.2.3|

# 2️⃣Steps
---
## 1. Create Model
- Entity interface
```csharp
public interface IEntity
{
	DateTime CreateDate { get; set; }
	Guid Id { get; set; }
}
```
- Base Entity
```csharp
public abstract class Entity : IEntity
{
	public Guid Id { get; set; } = Guid.NewGuid();
	public DateTime CreateDate { get; set; } = DateTime.UtcNow;
}
```

- AppUser model
```csharp
public class AppUser : IdentityUser
{
	[PersonalData]
	public string DisplayName { get; set; }

	public ICollection<FirstEntity> FirstEntities { get; set; }
}
```
## 2. Create DataContext class

```csharp
public class DataContext : IdentityDbContext<AppUser>
{

	public DataContext() : base(ConfigurationManager.ConnectionStrings["DefaultConnection"].ConnectionString)
	{
	}
	
	public DbSet<FirstEntity> FirstEntities { get; set; }
	public DbSet<SecondEntity> SecondEntities { get; set; }
}
```

## 3. Migrate Database

1. Step 1: Open the Pakage Manager Console 
	- Option 1: View -> Other Windows -> Package Manager Console
	- Option 2: Tools -> NuGet Package Manager -> Package Manager Console
2. Step 2: Type "Enable-Migrations" to the Console and Press Enter
	- Note: You should update the Entity Framework to version 6.4.4 to avoid the error.
3. Step 3: Type "Add-Migration /<Migration Name/>" to the console and press  Enter. A migration class will be generated.
4. Step 4: Type "Update-Database" to the Console and press Enter. The migration will be applied to your database.

# 🟢 If you update the entity classes, you can just pass the step 1 and continue.