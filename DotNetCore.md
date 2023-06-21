## Say Hello to .Net core .. 👋 

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
The Startup.cs file establishes the entry point and environment for your ASP.NET Core application; it creates services and injects dependencies so that the rest of the app can use them. The three methods in a default Startup.cs file each handle a different part of setting up the environment:

The constructor Startup() allows us to setup or include the configuration values.
ConfigureServices() allows us to add services to the Dependency Injection container.
Configure() allows us to add middleware and services to the HTTP pipeline.

