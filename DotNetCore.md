## .Net core .. 👋 

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
<div>
Middle ware is injected in application pipeline to handle the request and responses.For instance, There can have one middleware component to authenticate users, another piece of middleware to handle errors, and another middleware to serve static files such as JavaScript, CSS, images, etc.
It .Net core we inject the middle ware inside Configure method of startup class.

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
