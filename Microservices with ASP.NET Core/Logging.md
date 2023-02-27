# 1️⃣Packages
---
|Name|Version|
|-|-|
|Serilog.AspNetCore|6.1.0|

# 2️⃣Steps
1. Program.cs
   ```csharp
using Semibox.Identity.API.Extensions;
using Serilog;

Log.Logger = new LoggerConfiguration()
    .WriteTo.Console()
    .CreateBootstrapLogger();

try
{
    var builder = WebApplication.CreateBuilder(args);

    builder.Host.UseSerilog((ctx, lc) => lc
        .WriteTo.Console(outputTemplate: "[{Timestamp:HH:mm:ss} {Level}] {SourceContext}{NewLine}{Message:lj}{NewLine}{Exception}{NewLine}")
        .Enrich.FromLogContext()
        .ReadFrom.Configuration(ctx.Configuration));

    var app = await builder
        .ConfigureBuilder()
        .ConfigurePipelineAsync();

    app.Run();
}
catch (Exception ex)
{
    Log.Fatal(ex, "Unhandled Exception");
}
finally
{
    Log.Information("Shut down complete");
    Log.CloseAndFlush();
}
```
2. appSettings.json
```json
{
  "Serilog": {
    "MinimumLevel": {
      "Default": "Debug",
      "Override": {
        "Microsoft": "Warning",
        "Microsoft.Hosting.Lifetime": "Information",
        "Microsoft.AspNetCore.Authentication": "Debug",
        "System": "Warning"
      }
    }
  }
}
```

