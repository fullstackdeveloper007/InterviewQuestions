# C Sharp

<table>
  <tbody>
      <tr>  
     <td> Latest Version of C#, EF Core, .Net  </td>
  </tr>
  <tr>  
     <td> Accessibility Levels in C#  </td>
  </tr>
  <tr>    
     <td>  Diff btwn Partiall class and Extension method    </td>
  </tr>
   <tr> 
     <td> Threading </td>
  </tr>
     <tr>    
     <td> AdoDotNet </td>
  </tr>
  </tbody>
</table>

## 1. Accessibility Levels in C#

- **public**:
  - The type or member can be accessed by any other code in the same assembly or another assembly that references it.
  - The accessibility level of public members of a type is controlled by the accessibility level of the type itself.

- **private**:
  - The type or member can be accessed only by code in the same class or struct.

- **protected**:
  - The type or member can be accessed only by code in the same class, or in a class that is derived from that class.

- **internal**:
  - The type or member can be accessed by any code in the same assembly, but not from another assembly. In other words, internal types or members can be accessed from code that is part of the same compilation.

- **protected internal**:
  - The type or member can be accessed by any code in the assembly in which it's declared, or from within a derived class in another assembly.

- **private protected**:
  - The type or member can be accessed by types derived from the class that are declared within its containing assembly.

## 2. Diff btwn Partiall class and Extension method

* 🧱 Partial Class → Use when you want to organize a single class’s code across files.
Example: separating designer-generated UI code from developer logic.

* ✨ Extension Method → Use when you want to extend or add helper methods to an existing class (like adding .ToTitleCase() to string).

### Extension Method
  
```C#
public static class StringExtensions
{
    public static bool IsCapitalized(this string str)
    {
        if (string.IsNullOrEmpty(str)) return false;
        return char.IsUpper(str[0]);
    }
}

```
### Partial Class

```C#
public partial class Employee
{
    public string Name { get; set; }

    public void Display()
    {
        Console.WriteLine($"Employee: {Name}");
    }
}
public partial class Employee
{
    public void ShowDetails()
    {
        Console.WriteLine("Showing employee details...");
    }
}
```

## Threading
There are lot of ways to implement threading in .Net

* a) Thread t = new Thread(DoWork);
  t.Start();
* b) ThreadPool
    ThreadPool.QueueUserWorkItem(state => 
    {
        Console.WriteLine("Running in thread pool thread.");
    });
* c)   Task t = Task.Run(() => DoWork());
        await t;

* d) using parallel
        Parallel.For(0, 5, i =>
        {
            Console.WriteLine($"Iteration {i} running on thread {Task.CurrentId}");
        });
* e)  await Task.Run(() => LongRunningOperation());
        Console.WriteLine("Main thread free for other work");
* f)  BackgroundWorker worker = new BackgroundWorker();
        worker.DoWork += (s, e) => Console.WriteLine("Background work running...");
        worker.RunWorkerAsync();
     
