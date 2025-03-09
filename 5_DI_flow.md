# How DI Works When You Call an API in .NET

Let me explain the execution flow when a request hits your .NET API application, using simple terms and showing the steps:

## Setup Phase (When App Starts)

1. **Program.cs runs first**
   ```
   Your app starts → Program.cs executes
   ```

2. **Service registration happens**
   ```
   Program.cs registers services:
   builder.Services.AddScoped<IOrderService, OrderService>();
   builder.Services.AddSingleton<ILogger, Logger>();
   ```

3. **DI container is built**
   ```
   DI container gets filled with all your registered services
   (like filling a toolbox with tools before starting work)
   ```

## Request Phase (When API is Called)

1. **Request arrives**
   ```
   Someone calls GET /api/orders → Request hits your API
   ```

2. **Pipeline processes request**
   ```
   Request → Middleware (auth, logging) → Routing → Controller selection
   ```

3. **Controller is created**
   ```
   DI container checks: "What does OrderController need?"
   Sees: "It needs IOrderService and ILogger"
   ```

4. **Dependencies are resolved**
   ```
   DI container:
   • Creates/retrieves IOrderService (new one if Transient/Scoped, existing one if Singleton)
   • Retrieves the singleton ILogger
   • Injects both into OrderController
   ```

5. **Method executes**
   ```
   OrderController.GetOrders() runs with all dependencies available
   ```

6. **Response returns**
   ```
   Result → Middleware → Client
   ```

7. **Cleanup**
   ```
   Scoped services are disposed when request ends
   Transient services are disposed when they're no longer used
   Singleton services live on for next request
   ```

## Visual Flow

```
START → Program.cs (register services) → Build DI container
       ↓
REQUEST → Middleware → Routing → Find controller
       ↓
       DI container resolves dependencies:
       "OrderController needs IOrderService and ILogger"
       ↓
       Create/retrieve dependencies based on lifetime
       ↓
       Inject dependencies into controller
       ↓
       Run controller method
       ↓
       Return response
       ↓
END → Dispose scoped/transient services
```

This is the behind-the-scenes magic that happens with every API request in your .NET application!
