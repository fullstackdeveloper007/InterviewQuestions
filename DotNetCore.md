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

**1. .Net Core Basics**
* **.net core**  - It is open source,cross Platform, light and dependency injection is an added advantage.

* **Dependency Injection** - It is a design pattern that allows to pass dependency to objects instead of creating it inside, This way the classes will be loosly copuled and easy to change, test and reuse the code.
   By exposing dependencies in the constructor, you expose public information about the needs of your code, further explaining what it does and what it's needs are..

# 🔹 `ConfigureServices` vs `Configure` in ASP.NET Core

Both live in `Startup.cs` (or in `Program.cs` in minimal hosting model after .NET 6). They serve **different purposes** in app startup:

---

## 1. **ConfigureServices(IServiceCollection services)**

* Purpose: **Register dependencies & services** with the built-in Dependency Injection (DI) container.
* Called **at application startup**, before the pipeline is built.
* Adds things that your app needs later (DB, Identity, Logging, Authentication, etc.).

### Example:

```csharp
public void ConfigureServices(IServiceCollection services)
{
    // Register MVC / API controllers
    services.AddControllers();

    // Register Entity Framework DbContext
    services.AddDbContext<AppDbContext>(options =>
        options.UseSqlServer(Configuration.GetConnectionString("DefaultConnection")));

    // Add Authentication (JWT for example)
    services.AddAuthentication("Bearer")
        .AddJwtBearer(...);

    // Register custom services
    services.AddScoped<IEmailService, EmailService>();
}
```

✅ Think: **“What my app needs to run?” → Register here.**

---

## 2. **Configure(IApplicationBuilder app, IWebHostEnvironment env)**

* Purpose: **Build the HTTP request pipeline (Middleware pipeline).**
* Defines how an HTTP request is handled and what components are executed in sequence.
* Runs **after services are registered**.

### Example:

```csharp
public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
{
    if (env.IsDevelopment())
    {
        app.UseDeveloperExceptionPage();
    }
    else
    {
        app.UseExceptionHandler("/Home/Error");
        app.UseHsts();
    }

    // Middleware pipeline
    app.UseHttpsRedirection();
    app.UseStaticFiles();

    app.UseRouting();

    app.UseAuthentication();  // Must come before Authorization
    app.UseAuthorization();

    app.UseEndpoints(endpoints =>
    {
        endpoints.MapControllers();  // Map API controllers
        endpoints.MapRazorPages();   // If Razor Pages are used
    });
}
```

✅ Think: **“How my app should handle requests?” → Define here.**

---

# 🔑 Quick Summary

| Method                | Purpose                            | Examples                                                               |
| --------------------- | ---------------------------------- | ---------------------------------------------------------------------- |
| **ConfigureServices** | Register services (DI container)   | `AddDbContext`, `AddControllers`, `AddAuthentication`, custom services |
| **Configure**         | Define middleware request pipeline | `UseRouting`, `UseAuthentication`, `UseAuthorization`, `UseEndpoints`  |

---

👉 A simple way to remember:

* **ConfigureServices → What you need**
* **Configure → How you handle requests**

---

Do you want me to also show how this changed in **.NET 6+ minimal hosting model** (where `ConfigureServices` & `Configure` are merged into `Program.cs`)?

##Program.cs file

<pre class="notranslate">
<code>
public class Program
    {
        public static void Main(string[] args)
        {
            CreateHostBuilder(args).Build().Run();
        }

        public static IHostBuilder CreateHostBuilder(string[] args) =>
            Host.CreateDefaultBuilder(args)
                .UseSerilog((hostingContext, loggerConfiguration) => loggerConfiguration
            .ReadFrom.Configuration(hostingContext.Configuration))
                .ConfigureWebHostDefaults(webBuilder =>
                {
                    webBuilder.UseStartup<Startup>();
                    
                });
    }
</code></pre>

##Starup.cs
<pre>
	<code>
	public void ConfigureServices(IServiceCollection services)
        {
            services.AddMemoryCache(); 
            services.AddTransient<IClientService, ClientService>(); 
            services.AddControllers();            
            services.AddSwaggerGen(c =>
            {
                c.SwaggerDoc("v1", new OpenApiInfo { Title = "Test.Title", Version = "v1" });
                c.ResolveConflictingActions(a => a.First());
            });
        }
		    
>>>>>> Configure Method.
		    
	public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
        {
            if (env.IsDevelopment() || _ebsConfiguration.EnableSwagger )
            {
                app.UseDeveloperExceptionPage();
                app.UseSwagger();
                app.UseSwaggerUI(c =>
                {
                    c.ConfigObject.AdditionalItems["syntaxHighlight"] = new Dictionary<string, object>
                    {
                        ["activated"] = false
                    };
                    c.SwaggerEndpoint("/swagger/v1/swagger.json", "EBS.Core v1");
                });
            }

            app.UseHttpsRedirection();
            app.UseRouting();
            app.UseAuthorization();
            app.UseEndpoints(endpoints =>
            {
                endpoints.MapControllers();
            });
        }
	</code>
</pre>

**2. AddTransient Vs AddScoped Vs AddSingleton In ASP.NET Core**

 
<table>
<tr>
	<th>Service Type </th>
	<th>In scope of given Http request </th>
	<th>In different Http request</th>
</tr>
	<tbody>
	<tr>
		<td>Scope Service </td>
		<td>Same Instance </td>
		<td>New Instance </td>			
	</tr>
	<tr>
		<td>Transient Service </td>
		<td>New Instance </td>
		<td>New Instance </td>			
	</tr>	
	<tr>
		<td>Singleton Service </td>
		<td>Same Instance </td>
		<td>Same Instance </td>			
	</tr>		
	</tbody>
</table>

** AddScoped : In scoped, in the given http request same instnace of object will be provided thourout the request.
** AddTransient : In transient, with in the same request if that object is injected in more then one class different instance will be provided but in case of scoped same will be provided.

![NetCore](https://github.com/fullstackdeveloper007/InterviewQuestions/assets/96370256/8795f7b8-9331-4f5c-a418-a9ed70ed4d83)
* **AddTransient** - Transient lifetime services are created each time they are requested. This lifetime works best for lightweight, stateless services.

* **AddScoped** -
Scoped lifetime services are created once per request.

* **AddSingleton** -
Singleton lifetime services are created the first time they are requested (or when ConfigureServices is run if you specify an instance there) and then every subsequent request will use the same instance.

  **Example :**
  In startup.cs 
  <div> 
  <pre class="notranslate">
      <code> 
      public void ConfigureServices(IServiceCollection services)
      {
           services.AddScoped<ClassName>();
           services.AddTransient<IInterface, ClassName>();
          services.AddTransient<IInterface, ClassName>();
      } 
  </code></pre>
 </div>
 
**3. Understanding Middleware In ASP.NET Core**
<p>**Refrence Article :**  https://www.c-sharpcorner.com/article/overview-of-middleware-in-asp-net-core/</p>
<div>
Middle ware is injected in application pipeline to handle the request and responses.For instance, There can have one middleware component to authenticate users, another piece of middleware to handle errors, and another middleware to serve static files such as JavaScript, CSS, images, etc.
It .Net core we inject the middle ware inside **Configure method** of startup class.<br/>
 
<pre class="notranslate">
<code>
public void Configure(IApplicationBuilder app, IWebHostEnvironment env)    
{    
    if (env.IsDevelopment())    
    {    
        //This middleware is used reports app runtime errors in development environment.  
        app.UseDeveloperExceptionPage();    
    }    
    else    
    {    
        **//This middleware is catches exceptions thrown in production environment. **  
        app.UseExceptionHandler("/Error");   
        // The default HSTS value is 30 days. You may want to change this for production scenarios, .    
        app.UseHsts(); //adds the Strict-Transport-Security header.    
    }    
    //This middleware is used to redirects HTTP requests to HTTPS.  
    app.UseHttpsRedirection();   
    
    //This middleware is used to returns static files and short-circuits further request processing.   
    app.UseStaticFiles();  
    
    //This middleware is used to route requests.   
    app.UseRouting();   
    
    //This middleware is used to authorizes a user to access secure resources.  
    app.UseAuthorization();    
    
    //This middleware is used to add Razor Pages endpoints to the request pipeline.    
    app.UseEndpoints(endpoints =>    
    {    
        endpoints.MapRazorPages();               
    });    
} 
</code></pre> 
</div>

**a) app.Run()** -
This middleware component may expose Run[Middleware] methods that are executed at the end of the pipeline. Generally, this acts as a terminal middleware and is added at the end of the request pipeline, as it cannot call the next middleware.

**b) app.Use()**
This is used to configure multiple middleware. Unlike app.Run(), We can include the next parameter into it, which calls the next request delegate in the pipeline. We can also short-circuit (terminate) the pipeline by not calling the next parameter. 
<pre>
<code>
 public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
{
      if (env.IsDevelopment() || _ebsConfiguration.EnableSwagger )
      {
         app.UseDeveloperExceptionPage();
          app.UseSwagger();
          app.UseSwaggerUI(c =>
          {
              c.ConfigObject.AdditionalItems["syntaxHighlight"] = new Dictionary<string, object>
              {
                  ["activated"] = false
              };
              c.SwaggerEndpoint("/swagger/v1/swagger.json", "Test.Core v1");
          });
      }
      app.UseHttpsRedirection();
      app.UseRouting();
      app.UseAuthorization();
      app.UseEndpoints(endpoints =>
      {
         endpoints.MapControllers();
      });
}
</code>
</pre>

**c) app.Map()**- These extensions are used as a convention for branching the pipeline. The map branches the request pipeline based on matches of the given request path. If the request path starts with the given path, the branch is executed.

<pre class="notranslate">
<code>
public void Configure(IApplicationBuilder app, IWebHostEnvironment env)  
{  
    app.Map("/m1", HandleMapOne);  
    app.Map("/m2", appMap => {  
        appMap.Run(async context =>  
        {  
            await context.Response.WriteAsync("Hello from 2nd app.Map()");  
        });  
    });  
    app.Run(async (context) =>  
    {  
        await context.Response.WriteAsync("Hello from app.Run()");  
    });  
}  
private static void HandleMapOne(IApplicationBuilder app)  
{  
    app.Run(async context =>  
    {  
        await context.Response.WriteAsync("Hello from 1st app.Map()");  
    });   
}
</code>
</pre> 

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
