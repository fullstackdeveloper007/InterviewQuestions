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


Sure 👍 — here’s a **brief and clear explanation** of each **loading type in Entity Framework (EF) Core**, including examples and when to use them 👇

---

## ⚙️ **1. Eager Loading**

### 📖 What it is:

Eager loading means **loading related data at the same time** as the main entity — in a **single query**.

### ✅ How it works:

You tell EF Core upfront which related entities to include using `.Include()` and `.ThenInclude()`.

### 🧩 Example:

```csharp
var orders = context.Orders
    .Include(o => o.Customer)
    .Include(o => o.OrderItems)
    .ThenInclude(i => i.Product)
    .ToList();
```

### 💡 When to use:

* When you **know you’ll need** the related data immediately.
* Reduces **number of database calls** (good for performance).

### ⚠️ Caution:

* Can lead to **large joins** and **heavy queries** if too many relationships are included.

---

## ⚙️ **2. Lazy Loading**

### 📖 What it is:

Lazy loading means EF Core **automatically loads related data** when you **access the navigation property** for the first time.

### ✅ How it works:

* Related data is **not loaded initially**.
* The first time you access the property, EF Core **makes another DB call** to fetch it.

### 🧩 Example:

```csharp
var order = context.Orders.First();
var customer = order.Customer; // Triggers DB call if not loaded
```

### ⚙️ Setup Required:

Lazy loading is **disabled by default**.
You must enable proxies and mark navigation properties `virtual`.

```csharp
protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
{
    optionsBuilder.UseLazyLoadingProxies()
                  .UseSqlServer("connection_string");
}
```

### 💡 When to use:

* When you **don’t always need** related data.
* For **simpler domain models** or **desktop apps** (not ideal for APIs).

### ⚠️ Caution:

* Can cause **N+1 query issues** (many small DB calls).
* Avoid in **high-traffic or API-based** systems.

---

## ⚙️ **3. Explicit Loading**

### 📖 What it is:

Explicit loading means you **manually load related data** later, **on demand**, using the `Entry()` API.

### ✅ How it works:

You first load the main entity, and then call `.Load()` when you decide to fetch related data.

### 🧩 Example:

```csharp
var order = context.Orders.First();

// Load related Customer only when needed
context.Entry(order).Reference(o => o.Customer).Load();

// Load collection (like OrderItems)
context.Entry(order).Collection(o => o.OrderItems).Load();
```

### 💡 When to use:

* When you want **fine-grained control** over what data loads and when.
* Useful when **working with large datasets**.

### ⚠️ Caution:

* You’re responsible for managing **when to load**, so can be **error-prone** if not handled carefully.

---

## 🧾 **Summary Table**

| Type                 | Loads When                           | Triggers Multiple DB Calls | Default in EF Core | Use When                           |
| -------------------- | ------------------------------------ | -------------------------- | ------------------ | ---------------------------------- |
| **Eager Loading**    | Immediately (in query)               | ❌ No (single query)        | ❌                  | You always need related data       |
| **Lazy Loading**     | When navigation property is accessed | ✅ Yes                      | ❌ Disabled         | You sometimes need related data    |
| **Explicit Loading** | When you call `.Load()` manually     | ✅ Yes                      | ❌                  | You want full control over loading |

---

### 🧠 Quick Analogy

| Type                 | Analogy                                                      |
| -------------------- | ------------------------------------------------------------ |
| **Eager Loading**    | Ordering a full meal at once 🍱                              |
| **Lazy Loading**     | Ordering each dish only when you’re hungry 🍜                |
| **Explicit Loading** | You choose to go back to the kitchen for more food later 🍽️ |

---

Would you like me to add **performance comparison** between these loading types (query count, latency, and memory impact)?
