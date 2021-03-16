---
title: ".NET library"
draft: false
weight: 1
---

#### Introduction

In a .NET project, the easiest way to keep the database schema up to date across all your environments, is to deploy the SQL migration scripts with your assemblies and to execute Evolve at startup. This way, the deployed application automatically applies migrations and therefore operates against a predictable database state.

<i class="fa fa-info-circle"></i> Note you can even embed your migration scripts **into** assemblies not to expose intrisics of your application to the outside (see [EmbeddedResourceAssemblies](/configuration/#options) option).

#### Installation

Evolve is available on [NuGet](https://www.nuget.org/packages/Evolve).

```
Install-Package Evolve
```

#### Quick Start

<i class="fa fa-hand-o-right"></i> Initialize and [configure](/configuration/#options) Evolve to **migrate** the schema to the latest version when you start your application:

```C#
try
{
    var cnx = new SqliteConnection(Configuration.GetConnectionString("MyDatabase"));
    var evolve = new Evolve.Evolve(cnx, msg => _logger.LogInformation(msg))
    {
        Locations = new[] { "db/migrations" },
        IsEraseDisabled = true,
    };

    evolve.Migrate();
}
catch (Exception ex)
{
    _logger.LogCritical("Database migration failed.", ex);
    throw;
}
```

<i class="fa fa-hand-o-right"></i> Create at least one folder at the root of your project for your migration scripts and named them following the pattern described [here](/configuration/#naming-pattern). For example: `V1_3_1_1__Create_table.sql`

<i class="fa fa-hand-o-right"></i> Make sure to set the property `Copy to output directory` to **Copy always** on each of your migration script, or modify your csproj file to automatically copy all the SQL files to the output build folder:

```xml
<ItemGroup>
  <Content Include="db\migrations\**\*.sql">
    <CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>
  </Content>
</ItemGroup>
```

<i class="fa fa-info-circle"></i> Samples can be found [here](/samples)