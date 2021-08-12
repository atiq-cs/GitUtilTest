Title: dotnet core Hello World with Entity Framework and Database
Published: 8/12/2021
Tags:
  - dotnet core
  - entity framework
---

## Razor Pages App
localdb mdf files are usually stored at `$HOME` (for example, `C:\Users\YOUR_NAME`)

    dotnet new webapp -n P03_ContosoUniversity_RP
    cd P03_ContosoUniversity_RP

    dotnet add package Microsoft.VisualStudio.Web.CodeGeneration.Design
    dotnet add package Microsoft.EntityFrameworkCore.SQLite
    dotnet add package Microsoft.EntityFrameworkCore.SqlServer
    dotnet add package Microsoft.EntityFrameworkCore.Design
    dotnet add package Microsoft.EntityFrameworkCore.Tools

    dotnet add package Microsoft.AspNetCore.Diagnostics.EntityFrameworkCore

    dotnet aspnet-codegenerator razorpage -m Student -dc ContosoUniversity.Data.SchoolContext -udl -outDir Pages\Students --referenceScriptLibraries -sqlite

And, we keep following the documentation, https://docs.microsoft.com/en-us/aspnet/core/data/ef-rp/intro

We refactor all `P03_ContosoUniversity_RP` with `ContosoUniversity`.

Scaf

    dotnet tool update --global dotnet-ef
    dotnet ef database update

    $Env:ASPNETCORE_ENVIRONMENT = "Development"
    dotnet run


## MVC App
Steps

    dotnet new mvc -n P03_ContosoUniversity

Replace `P03_ContosoUniversity` with 'Contoso University'.

    dotnet add package Microsoft.AspNetCore.Diagnostics.EntityFrameworkCore

we keep following,
https://docs.microsoft.com/en-us/aspnet/core/data/ef-mvc/intro

add default connection in `appsettings.Development.json`


## Razor Pages App (net core)
This is a test to be able to run the EF Core Razor App with .net core,

We require following packages,

    dotnet new webapp -n P03_ContosoUniversity_netcore
    dotnet add package Microsoft.EntityFrameworkCore.Design
    dotnet add package Microsoft.EntityFrameworkCore
    dotnet add package Microsoft.EntityFrameworkCore.SQLite

We add all the scaffolding files from a previous project that target .net6

We end up finding that,

    // in ConfigureServices
    // services.AddDatabaseDeveloperPageExceptionFilter();
    // in Configure
    // app.UseMigrationsEndPoint();

requires,

    dotnet add package Microsoft.AspNetCore.Diagnostics.EntityFrameworkCore
    Determining projects to restore...
    Writing C:\Users\atiq\AppData\Local\Temp\tmp6CF5.tmp
    info : Adding PackageReference for package 'Microsoft.AspNetCore.Diagnostics.EntityFrameworkCore' into project 'D:\Code\CS\P03_ContosoUniversity_netcore\P03_ContosoUniversity_netcore.csproj'.
    info :   GET https://api.nuget.org/v3/registration5-gz-semver2/microsoft.aspnetcore.diagnostics.entityframeworkcore/index.json
    info :   OK https://api.nuget.org/v3/registration5-gz-semver2/microsoft.aspnetcore.diagnostics.entityframeworkcore/index.json 419ms
    info : Restoring packages for D:\Code\CS\P03_ContosoUniversity_netcore\P03_ContosoUniversity_netcore.csproj...
    error: NU1202: Package Microsoft.AspNetCore.Diagnostics.EntityFrameworkCore 5.0.9 is not compatible with netcoreapp3.1 (.NETCoreApp,Version=v3.1). Package Microsoft.AspNetCore.Diagnostics.EntityFrameworkCore 5.0.9 supports: net5.0 (.NETCoreApp,Version=v5.0)
    error: Package 'Microsoft.AspNetCore.Diagnostics.EntityFrameworkCore' is incompatible with 'all' frameworks in project 'D:\Code\CS\P03_ContosoUniversity_netcore\P03_ContosoUniversity_netcore.csproj'

Also, the old version (3.1.18 supports .net core) of `Diagnostics.EntityFrameworkCore` doesn't have the definitions mentioned above.
