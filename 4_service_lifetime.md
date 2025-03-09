# Service Lifetimes in C# Dependency Injection

When you register services in a C# application (especially in ASP.NET Core), there are three main service lifetimes:

## 1. Transient
- **Created every time**: A new instance is created each time it's requested
- **Example use**: For lightweight services with no shared state
- **Code example**:
  ```csharp
  services.AddTransient<IExampleService, ExampleService>();
  ```

## 2. Scoped
- **Created once per scope**: Same instance within a request, new instance for different requests
- **Example use**: Most common for web applications - services that should be consistent during a web request
- **Code example**:
  ```csharp
  services.AddScoped<IOrderProcessor, OrderProcessor>();
  ```

## 3. Singleton
- **Created once only**: Same instance for the entire application lifetime
- **Example use**: Services that are expensive to create or need to maintain state
- **Code example**:
  ```csharp
  services.AddSingleton<ILogger, Logger>();
  ```

## Simple Comparison

```
Transient: New toy every time you ask
Scoped:    Same toy during one play session, new toy next time
Singleton: Same toy forever - everyone shares one
```

Be careful with Singleton services that maintain state or with Scoped services used in Singleton services, as this can cause unexpected behavior.
