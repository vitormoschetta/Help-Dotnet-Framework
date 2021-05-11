# Help-Dotnet-Framework

## Formas de setar a porta de uma aplicaço dotnet

<https://stackoverflow.com/questions/37365277/how-to-specify-the-port-an-asp-net-core-application-is-hosted-on>

##### Usando appsettings.json:
```
{
  "Urls": "http://localhost:5001"
}
```

Obs: O método `CreateHostBuilder` deve utilizar o retorno padrão `IHostBuilder` e não `IWebHostBuilder`.



##### Usando argumentos de linha de comando:
```
dotnet run --urls=http://localhost:9001/
```

Obs: serve tanto para executar o código fonte quanto o binário.

