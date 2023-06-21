## Say Hello to .Net core .. 👋 
>Click :star:if you like the work 

**1. .Net Core Basics**
* **.net core**  - It is open source,cross Platform, light and dependency injection is an added advantage.

* **Dependency Injection** - It is a design pattern that allows to pass dependency to objects instead of creating it inside, This way the classes will be loosly copuled and easy to change, test and reuse the code.

   By exposing dependencies in the constructor, you expose public information about the needs of your code, further explaining what it does and what it's needs are..

**2. AddTransient Vs AddScoped Vs AddSingleton In ASP.NET Core**

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
It .Net core we inject the middle ware inside Configure method of startup class.<br/>
 
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
