# .Net Core

## .Net Version History

| **.NET Version** | **Release Date** | **C# Version**      | **.NET Major Features**                                                                                                                                                                                                                                                                                                                                                                                 | **C# Language Features**                                                                                                                                                                                           |
| ---------------- | ---------------- | ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **.NET 6 (LTS)** | Nov 2021         | **C# 10**           | - Long-Term Support (LTS)<br>- Unified platform (mobile, web, desktop)<br>- Hot Reload (edit code during runtime)<br>- `DateOnly` & `TimeOnly` structs<br>- Improved `System.Text.Json` (source generators, DOM API)<br>- File IO & GC performance boosts<br>- Single-file deployment & trimming<br>- HTTP/3 support (preview)<br>- Arm64 and Apple Silicon support                                     | - Global using directives<br>- File-scoped namespaces<br>- Record structs<br>- Constant interpolated strings<br>- Extended property patterns<br>- Improved lambda syntax<br>- `with` expressions for structs       |
| **.NET 7 (STS)** | Nov 2022         | **C# 11**           | - Short-Term Support (STS)<br>- Better Native AOT (Ahead-of-Time compilation)<br>- Generic Math and static abstract members in interfaces<br>- `Rate Limiting Middleware` in ASP.NET Core<br>- Enhanced MAUI (mobile & desktop)<br>- Performance improvements across runtime and APIs<br>- Minimal APIs improvements<br>- Container-friendly runtime                                                    | - Required members (`required` keyword)<br>- Raw string literals (`"""text"""`)<br>- List patterns (`[1,2,..]`)<br>- Generic attributes<br>- UTF-8 string literals (`"text"u8`)<br>- Nameof parameter expressions  |
| **.NET 8 (LTS)** | Nov 2023         | **C# 12**           | - LTS release (3 years)<br>- Unified Native AOT for apps<br>- Enhanced ASP.NET Core performance & Blazor SSR<br>- `System.Text.Json` improvements (Polymorphism & faster serialization)<br>- New collection expressions<br>- New `dotnet publish` simplifications<br>- On-stack replacement (OSR) for faster JIT<br>- Improved Linux and container support<br>- New features for `MAUI` and `EF Core 8` | - Collection expressions (`int[] arr = [1,2,3];`)<br>- Primary constructors for classes<br>- Interceptors (experimental)<br>- Default lambda parameters<br>- Alias any type<br>- Inline arrays (preview)           |
| **.NET 9 (STS)** | Nov 2024         | **C# 13 (Preview)** | - Short-Term Support (6 months STS)<br>- Focus on AI & cloud-native workloads<br>- Built-in ONNX and TensorFlow runtime support<br>- Enhanced Native AOT (faster startup)<br>- Unified HTTP stack improvements<br>- Better observability (OpenTelemetry built-in)<br>- Performance & memory footprint improvements<br>- Enhanced diagnostics for distributed systems                                    | - Partial properties (preview)<br>- Params collections (`params ReadOnlySpan<T>`)<br>- Lambda default parameter enhancements<br>- Better ref fields in `ref struct`<br>- New pattern matching extensions (preview) |



Perfect 👍 — I’ll create a **clean tabular format** with your listed points, correct them, and expand with more essentials that are frequently asked in interviews or needed for brushing up.

Here’s a **comprehensive .NET / .NET Core concepts table**:

---

# 📝 .NET & .NET Core
| **Topic**                                            | **Details**                                                                                                                                                                                                                               |
| ---------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **.NET Framework vs .NET Core / .NET 5+**            | **.NET Framework** → Windows-only, tightly coupled to IIS, mature but not cross-platform.<br> **.NET Core (now unified into .NET 5/6/7/8)** → Cross-platform, open source, modular, high performance, can host on Kestrel, Docker, Linux. |
| **Program Startup (Configure vs ConfigureServices)** | `ConfigureServices(IServiceCollection services)` → Register services (DI container).<br> `Configure(IApplicationBuilder app, IWebHostEnvironment env)` → Setup HTTP request pipeline (middleware).                                        |
| **CreateDefaultBuilder vs ConfigureWebHostDefaults** | `CreateDefaultBuilder()` → Sets up defaults (logging, config, Kestrel, DI).<br> `ConfigureWebHostDefaults()` → Used inside `CreateDefaultBuilder` to configure hosting (Kestrel, IIS integration, etc.).                                  |
| **Service Lifetimes**                                | - **Transient** → New instance every time (lightweight services).<br> - **Scoped** → Same instance per HTTP request (DB context).<br> - **Singleton** → Single instance for app lifetime (caching, logging).                              |
| **Routing in .NET Core APIs**                        | Uses **Endpoint Routing** (`app.UseRouting(); app.UseEndpoints(...)`).<br>Attributes (`[Route]`, `[HttpGet]`) or convention-based.<br>Supports RESTful APIs and MVC routing.                                                              |

---

# 📝 MVC Concepts

| **Topic**                       | **Details**                                                                                                                                                                                   |
| ------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **MVC vs ASP.NET Web Forms**    | - MVC → Separation of Concerns, testable, lightweight, HTML/CSS/JS friendly.<br> - Web Forms → ViewState heavy, tightly coupled, event-driven, not great for SPAs/APIs.                       |
| **Page Life Cycle in MVC**      | Simpler than Web Forms: **Routing → Controller Init → Action Execution → Result Execution → View Render**. No heavy ViewState/postback cycle.                                                 |
| **Routing in ASP.NET Core MVC** | Uses **Endpoint Routing**.<br> Example: `endpoints.MapControllerRoute(name: "default", pattern: "{controller=Home}/{action=Index}/{id?}");`.<br> Attributes like `[Route("api/[controller]")]`. |
| **Razor Pages**                 | Page-based model on top of MVC. Each `.cshtml` file has a PageModel (`.cshtml.cs`). Simplifies CRUD apps, less ceremony than controllers.                                                     

---

# 📝 API Security & Scaling

| **Topic**                          | **Details**                                                                                                                                                                 |
| ---------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Securing APIs**                  | - Use **JWT Authentication** (Bearer tokens).<br> - Enable **Authorization policies & roles**.<br> - Use **HTTPS/TLS**.<br> - Protect against **CSRF, XSS, SQL Injection**. |
| **API Throttling / Rate Limiting** | Restrict requests per user/IP (e.g., 100 requests/min).<br> Implement via **ASP.NET Core Middleware** or API Gateway (Azure API Mgmt, Nginx, Kong).                         |
| **Load Balancing APIs**            | Distribute requests across servers.<br> Use **Azure Load Balancer, AWS ELB, Nginx, HAProxy, Kubernetes Ingress**.<br> Ensures **scalability + high availability**.          |

---

# 📝 Additional Core Concepts (Good to Brush Up)

| **Topic**                      | **Details**                                                                                                                          |
| ------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------ |
| **Middleware**                 | Ordered pipeline handling requests/responses. Examples: Authentication, Logging, Exception Handling.                                 |
| **Dependency Injection (DI)**  | Built-in DI container. Register services via `AddTransient`, `AddScoped`, `AddSingleton`.                                            |
| **Kestrel Web Server**         | Cross-platform, lightweight, high-performance server used by .NET Core. Can run standalone or behind reverse proxies like Nginx/IIS. |
| **Configuration in .NET Core** | Uses `appsettings.json`, environment variables, secrets, Azure Key Vault.                                                            |
| **Logging**                    | Built-in logging with providers (Console, Debug, Azure App Insights, Serilog, NLog).                                                 |
| **Entity Framework Core**      | ORM for .NET Core. Supports LINQ queries, migrations, change tracking. Works with SQL Server, PostgreSQL, MySQL, etc.                |
| **gRPC Support**               | High-performance RPC framework, alternative to REST for microservices.                                                               |
| **Hosting Models**             | - **In-process** (better perf).<br> - **Out-of-process** (via Kestrel + reverse proxy).                                              |

---

✅ This way, you can revise quickly **concept-by-concept** and be ready for interviews or deep dives.

Do you also want me to extend this into a **Q&A cheat sheet** (like common interview questions with crisp answers for each of these)?


## Say Hello to .Net core .. 👋 
>Click :star:if you like the work 



**4. Describe the structure and purpose of the Startup.cs file in an ASP.NET Core application**
<div>
The Startup.cs file establishes the entry point and environment for your ASP.NET Core application; it creates services and injects dependencies so that the rest of the app can use them. The three methods in a default Startup.cs file each handle a different part of setting up the environment:

>**The constructor Startup()** allows us to setup or include the configuration values.

>**ConfigureServices()** allows us to add services to the Dependency Injection container.

>**Configure()** allows us to add middleware and services to the HTTP pipeline.
</div>

**5. Action Result**
Actions are the methods in controller class which are responsible for returning the view or Json data.

**Refrence Article:** https://www.c-sharpcorner.com/article/actionresult-in-asp-net-core-mvc/
<table>
<tbody style="outline: 0px;">
         <tr style="outline: 0px;" bgcolor="#0270bf">
             <td style="border: 1px dashed #ababab;">
             <div><span style="color: #ffffff;">Action Method</span></div>
             </td>
             <td style="border: 1px dashed #ababab;">
             <div><span style="color: #ffffff;">Description</span></div>
             </td>
         </tr>
         <tr>
             <td style="border: 1px dashed #ababab;">
             <div>IActionResult</div>
             </td>
             <td style="border: 1px dashed #ababab;">
             <div>Defines a contract that represents the result of an action method.</div>
             </td>
         </tr>
         <tr>
             <td style="border: 1px dashed #ababab;">
             <div>ActionResult</div>
             </td>
             <td style="border: 1px dashed #ababab;">
             <div>A default implementation of IActionResult.</div>
             </td>
         </tr>
         <tr>
             <td style="border: 1px dashed #ababab;">
             <div>ContentResult</div>
             </td>
             <td style="border: 1px dashed #ababab;">
             <div>Represents a text result.</div>
             </td>
         </tr>
         <tr>
             <td style="border: 1px dashed #ababab;">
             <div>EmptyResult</div>
             </td>
             <td style="border: 1px dashed #ababab;">
             <div>Represents an ActionResult that when executed will do nothing.</div>
             </td>
         </tr>
         <tr>
             <td style="border: 1px dashed #ababab;">
             <div>JsonResult</div>
             </td>
             <td style="border: 1px dashed #ababab;">
             <div>An action result which formats the given object as JSON.</div>
             </td>
         </tr>
         <tr>
             <td style="border: 1px dashed #ababab;">
             <div>PartialViewResult</div>
             </td>
             <td style="border: 1px dashed #ababab;">
             <div>Represents an ActionResult that renders a partial view to the response.</div>
             </td>
         </tr>
         <tr>
             <td style="border: 1px dashed #ababab;">
             <div>ViewResult</div>
             </td>
             <td style="border: 1px dashed #ababab;">
             <div>Represents an ActionResult that renders a view to the response.</div>
             </td>
         </tr>
         <tr>
             <td style="border: 1px dashed #ababab;">
             <div>ViewComponentResult</div>
             </td>
             <td style="border: 1px dashed #ababab;">
             <div>An IActionResult which renders a view component to the response.</div>
             </td>
         </tr>
     </tbody></table>
<pre class="notranslate">
<code>   
public IActionResult Index()  
{  
      return View();  
} 
public ActionResult About()  
{  
     return View();  
}
public ContentResult ContentResult()  
{  
      return Content("I am ContentResult");  
} 
public EmptyResult EmptyResult()  
{  
   return new EmptyResult();  
}
</code>
</pre> 

**5.How does routing work in ASP.NET Core MVC ?**

Routing in ASP.NET Core MVC is the mechanism through which incoming requests are mapped to controllers and their actions. This is achieved by adding Routing middleware to the pipeline and using IRouteBuilder to map URL pattern (template) to a controller and action.
Add HomeController to demonstrate the conventional routing (see discussion).

**Refrence Article:** https://www.c-sharpcorner.com/article/asp-net-core-2-0-mvc-routing/

<pre class="notranslate">
<code>
public class HomeController :controlller
{
	public IActionResult Index()
	{
	}	
	[HttpGet]
	public IActionResult PageTwo()
	{
	}
	[HttpGet]
	public IActionResult PageTwo(int id)
	{
	}
}
</code>
</pre> 

>Attribute Routing

<pre class="notranslate">
<code>
[Route("Work")]
public class HomeController :controlller
{
	public IActionResult Index()
	{
	}	
	[Route("One")]
	public IActionResult PageTwo()
	{
	}
	[Route("Two")]
	public IActionResult PageTwo(int id)
	{
	}
}</code>
</pre>

**Razor Pages**
It supports cross-platform, hence it can be deployed on Windows, Unix, and Mac operating systems.
It is easy to learn.
Lightweight and flexible framework so it can fit with any application you want to build.
Can work with C# programming language with Razor markup.
More organized with code behind page like asp.net web forms.
