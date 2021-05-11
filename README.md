# Help-Dotnet-Framework

## Formas de setar a porta de uma aplicaço dotnet

<https://stackoverflow.com/questions/37365277/how-to-specify-the-port-an-asp-net-core-application-is-hosted-on>    
<https://docs.microsoft.com/pt-br/aspnet/core/fundamentals/host/web-host?view=aspnetcore-5.0#server-urls>

#### Usando appsettings.json:
```
{
  "Urls": "http://localhost:5001"
}
```

Obs: O método `CreateHostBuilder` deve utilizar o retorno padrão `IHostBuilder` e não `IWebHostBuilder`.

<br>


#### Usando argumentos de linha de comando:
```
dotnet run --urls=http://localhost:9001/
```

Obs: serve tanto para executar o código fonte quanto o binário.

<br>


#### Usando UseUrls(), se preferir fazê-lo programaticamente: 
``` 
public static class Program
{
    ...

    public static IHostBuilder CreateHostBuilder(string[] args) =>
        Host.CreateDefaultBuilder(args)
            .ConfigureWebHostDefaults(builder =>
            {
                builder.UseStartup<Startup>();
                builder.UseUrls("http://localhost:5001/");
            });
}
```

Obs: O problema desse modelo é que se estivermos utilizando o Entity Framework como ORM, teremos um problema de design pattern para gerar as Migrations em um modelo DDD.

<br>


#### Usando o construtor de host da web em vez do construtor de host genérico: 

```
public class Program
{
    public static void Main(string[] args) =>
        new WebHostBuilder()
            .UseKestrel()
            .UseContentRoot(Directory.GetCurrentDirectory())
            .UseIISIntegration()
            .UseStartup<Startup>()
            .UseUrls("http://localhost:5001/")
            .Build()
            .Run();
}
```

Obs: Teremos o mesmo problema de Migrations apontado no item anterior.
