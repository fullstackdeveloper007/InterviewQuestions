## Hello Developer .. 👋 Lets brush up the skills.

### Major Topic of Interview 
- Nice Intro
- Company Introduction
- Project Overview and Tech stack with version like C# .net or react version
- Security
- Design Pattern
- EF Core
- .Net core
- Azure Service
- Caching
- Microservices
- -Unit Testing Framewrok
- 

## Security: **How to Secure APIs / Applications**

The security can be implemented on multiple level. like 

1. **Authentication & Authorization**

   * Use **OAuth 2.0 / JWT tokens** for API authentication.
   * Ensure **role-based access control (RBAC)** to limit what each user or service can do.

2. **Transport Security**

   * Enforce **HTTPS / TLS 1.2+** for all communication.
   * Use **mTLS** for highly sensitive internal services. mTLS (Mutual TLS) is an enhanced version of TLS where both the client and server authenticate each other using certificates, not just the server.

3. **Input Validation & Sanitization**

   * Validate all incoming requests to prevent **SQL injection, XSS, and other attacks**.
   * Use framework-provided validation (like ASP.NET Core Model Validation).

4. **CSRF Protection**

   * For web applications with cookies, implement **anti-CSRF tokens**.
   * For SPAs(React, Angular, etc.), using JWT in headers, CSRF is less of a concern.
      Authorization: Bearer <JWT_TOKEN>
  - Since JWTs are typically stored in localStorage or sessionStorage, a malicious site cannot read them (same-origin policy).
  - CSRF protection is mainly for cookie-based authentication, where the browser automatically attaches credentials.
5. **Rate Limiting & Throttling**
   * Protect APIs from abuse and DDoS attacks using **rate limits**.
   * Implementation in .NET Core
```
    using Microsoft.AspNetCore.RateLimiting;
    using System.Threading.RateLimiting;

    var builder = WebApplication.CreateBuilder(args);

    // Add rate limiting services
    builder.Services.AddRateLimiter(options =>
    {
        options.AddFixedWindowLimiter("Fixed", limiterOptions =>
      {
          limiterOptions.PermitLimit = 100; // max 100 requests
        limiterOptions.Window = TimeSpan.FromMinutes(1); // per 1 minute
        limiterOptions.QueueProcessingOrder = QueueProcessingOrder.OldestFirst;
        limiterOptions.QueueLimit = 20; // optional queue for extra requests
      });
  });

  var app = builder.Build();

  // Apply rate limiting globally
  app.UseRateLimiter();
  app.MapGet("/", () => "Hello World!");
  app.Run();
```
     
*Rate Limiting Per Endpoint
```
app.MapGet("/api/data", () => "Data")
   .RequireRateLimiting("Fixed"); // Apply limiter by name

```
6. **Data Protection**

   * Encrypt sensitive data **in transit** (HTTPS) and **at rest** (database encryption).
   * Mask or redact sensitive fields in logs.

7. **Logging & Monitoring**

   * Track API access, authentication failures, and unusual patterns.
   * Integrate with **SIEM or monitoring tools** for alerts.

8. **Secure Development Practices**

   * Keep dependencies updated.
   * Conduct **regular security testing** (static analysis, penetration testing).
   * Follow **OWASP API Security Top 10**.

9. **API Gateway / Middleware**
   * Use a gateway to centralize authentication, rate limiting, logging, and request validation.

---

💡 **Optional Short Version for Interviews:**

*"I secure APIs by enforcing HTTPS, using OAuth2/JWT for authentication, applying role-based access control, validating inputs, protecting against CSRF and XSS, encrypting sensitive data, implementing rate limiting, and monitoring all traffic through logging and API gateways. I also follow secure development practices and regularly test APIs for vulnerabilities."*

---

If you want, I can also **draft a 30-second spoken version** that sounds natural for an interview without sounding like you’re reading a script.

Do you want me to do that?

<table>
  <tbody>
  <tr>
    <td>      1    </td>
     <td> <a title="Click me" href="https://github.com/fullstackdeveloper007/InterviewQuestions/blob/main/DotNetCore.md">  Asp.net </a>   </td>
  </tr>
  <tr>
    <td>     2    </td>
     <td>   C#    </td>
  </tr>
   <tr>
    <td>     3    </td>
     <td>   <a href="https://github.com/fullstackdeveloper007/InterviewQuestions/blob/main/DotNetCore.md"> .Net Core </a>   </td>
  </tr>
  <tr>
    <td>     4    </td>
     <td>   Micro services    </td>
  </tr>
  <tr>
    <td>     5    </td>
     <td>  <a href="https://github.com/fullstackdeveloper007/InterviewQuestions/blob/main/DesignPatterns.md"> Design Patterns </a>    </td>
  </tr>
   <tr>
    <td>     6   </td>
     <td>   WEB API    </td>
  </tr>
  <tr>
    <td>     7   </td>
     <td>  Programing Skills    </td>
  </tr>
    <tr>
    <td>     8   </td>
     <td>  Oops concept   </td>
  </tr>
     <tr>
    <td>     9   </td>
     <td>  PL/SQL    </td>
  </tr>
     <tr>
    <td>     10  </td>
     <td>  Angular    </td>
  </tr>
  </tbody>
</table>


  
 
 
