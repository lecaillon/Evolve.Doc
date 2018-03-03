---
title: "Getting Started"
draft: false
chapter: false
pre: "<b>2. </b>"
weight: 2
icon: ""
---

### Installation

Evolve is available as a single [NuGet package](https://www.nuget.org/packages/Evolve).

```
Install-Package Evolve
```

### Quick Start

Evolve can use 2 different (but complementary) execution modes: [**MSBuild**](/getting-started/#msbuild-mode) or [**In-App**](/getting-started/#in-app-mode). Whatever you choose first, you will have to:

<i class="fa fa-hand-o-right"></i> Create at least one folder at the root of your project for your sql files.

<i class="fa fa-hand-o-right"></i> Name your sql files following the pattern described [here](/configuration/#naming-pattern). For example: `V1_3_1__Create_table.sql`

#### MSBuild mode

**This mode is recommanded for development and CI**. Evolve will be executed at build time and automatically ensure your database is up-to-date. If the migration fails, the entire MSBuild process is stopped in error.

##### .NET project

To configure Evolve in a .NET project, use your project configuration file (`app.config` or `web.config`) with at least those variables:

```xml
<appSettings>
  <add key="Evolve.ConnectionString" value="Server=127.0.0.1;Port=5432;Database=my_db;User Id=postgres;Password=postgres;" />
  <add key="Evolve.Driver" value="npgsql" /> <!-- or sqlserver or microsoftdatasqlite or sqlite or mysql or mariadb -->
  <add key="Evolve.Locations" value="Sql_Scripts" />
  <add key="Evolve.Command" value="migrate" />
</appSettings>
```

##### .NET Core project

To configure Evolve in a .NET Core project, add a new `evolve.json` file at the root of your project with at least those variables:

```json
{
  "Evolve.ConnectionString": "Server=127.0.0.1;Database=Northwind;User Id=sa;Password=Password12!;",
  "Evolve.Driver": "sqlserver",
  "Evolve.Locations": "Sql_Scripts/SQLServer/Sql",
  "Evolve.Command": "migrate"
}
```

#### In-app mode

In this mode Evolve will be executed at runtime. **It is the recommanded way to update the database in production**.

```C#
try
{
    var cnx = new SqliteConnection(Configuration.GetConnectionString("MyDatabase"));
    var evolve = new Evolve.Evolve(cnx, msg => _logger.LogInformation(msg))
    {
        Locations = new List<string> { "db/migrations" },
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

<i class="fa fa-hand-o-right"></i> For a complete list of options you can set in the configuration file, please refer to this [chapter] (/configuration/#options).
