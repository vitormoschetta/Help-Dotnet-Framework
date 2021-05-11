## Host Generico

<https://docs.microsoft.com/pt-br/aspnet/core/fundamentals/host/generic-host?view=aspnetcore-5.0>




## Host Web

<https://docs.microsoft.com/pt-br/aspnet/core/fundamentals/host/web-host?view=aspnetcore-5.0>
```
public static void Main(string[] args)
{
    CreateWebHostBuilder(args).Build().Run();
}

public static IWebHostBuilder CreateWebHostBuilder(string[] args)
{
    var config = new ConfigurationBuilder()
        .SetBasePath(Directory.GetCurrentDirectory())
        .AddJsonFile("hostsettings.json", optional: true)
        .AddCommandLine(args)
        .Build();

    return WebHost.CreateDefaultBuilder(args)
        .UseUrls("http://localhost:5000")
        .UseConfiguration(config)
        .Configure(app =>
        {
            app.Run(context =>
                context.Response.WriteAsync("Hello, World!"));
        });
}
```

