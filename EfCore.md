# Lazy Loading, Eager Loading, Explicit loading

### 1. Lazy Loading
Lazy loading in Entity Framework Core (EF Core) is a mechanism that defers the loading of related entities from the database until they are explicitly accessed in the code. This means that initially, only the main entity is retrieved, and associated entities are fetched only when their navigation properties are accessed.

**Enabling Lazy Loading:** **.UseLazyLoadingProxies() in**

```
    dotnet add package Microsoft.EntityFrameworkCore.Proxies

protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
    {
        optionsBuilder.UseLazyLoadingProxies()
                      .UseSqlServer("YourConnectionString");
    }

```


**How Lazy Loading Works in EF Core:**
Virtual Navigation Properties:  For lazy loading to work, the navigation properties (representing relationships to other entities) in your entity classes must be marked as virtual. 
This allows EF Core to create proxy objects that can intercept access to these properties.
```
public class Employee
{
    public int Id { get; set; }
    public string Name { get; set; }

    // Navigation property
    public virtual ICollection<Order> Orders { get; set; }
    public virtual Customer Customer { get; set; }
}

public class Order
{
    public int Id { get; set; }
    public string Product { get; set; }
    public int EmployeeId { get; set; }
}

public class Customer
{
    public int Id { get; set; }
    public string CompanyName { get; set; }
}

```
Example:
```
using (var context = new AppDbContext())
{
    var emp = context.Employees.FirstOrDefault(e => e.Id == 1);

    // At this point, only Employee data is loaded

    var orders = emp.Orders;    // EF will run a query here automatically
    var customer = emp.Customer; // Another query runs here
}
```
- That is lazy loading — EF loads related entities when accessed.
- Note: Orders and Customer will trigger separate SQL queries (can cause N+1 issue if used in loops).

**Disadvantages and Considerations:**
- N+1 Problem: If you iterate over a collection of entities and access a lazy-loaded navigation property on each one, it can lead to multiple individual database queries (the "N+1 problem"), potentially impacting performance.
- Performance Overhead: Each lazy-loaded access incurs a separate database round trip, which can be slower than eager loading if many related entities are needed.
- Serialization Issues: Lazy-loaded proxies can sometimes cause issues during serialization if not handled carefully.

### 2. Eager Loading:(Include / ThenInclude)
- Use the .Include() method in your queries to explicitly load related entities along with the main entity in a single query.
- Good for: APIs, dashboards, reports → when you know you’ll need related data.
- ❌ Bad for: Very large graphs (too much data in one query).

### 3. Explicit Loading:(Load())
- You manually load related data when needed.
- ❌ Bad for: Lots of boilerplate if used everywhere.
- Manually load related entities using Entry(entity).Collection(c => c.RelatedCollection).Load() or Entry(entity).Reference(r => r.RelatedEntity).Load().
