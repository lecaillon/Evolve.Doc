---
title: "Evolve MSBuild"
draft: false
chapter: false
pre: "<b>5. </b>"
weight: 5
icon: ""
---

### Introduction

Since Evolve 2.0, the MSBuild mode comes in a completely separate NuGet package with no dependency against Evolve. 
As usual Evolve.MSBuild will be executed at build time and automatically ensure that your database is up-to-date. If the migration fails, the MSBuild process will stop with an error. 

This mode is the easiest way to start with Evolve. No need to add code. Moreover it avoids adding a reference to Evolve in your project dependencies. Evolve.MSBuild is declared as `PrivateAssets` in your csproj file, this way it will be consumed but won't flow to the parent project.

Evolve.MSBuild is a great tool to keep a development or even an CI environment up-to-date. But in this mode you will certainly need the [CLI](/cli) to run your migration scripts in production.

### Installation

Evolve.MSBuild is available as a single [NuGet package](https://www.nuget.org/packages/Evolve.MSBuild.Windows.x64).

```
Install-Package Evolve.MSBuild.Windows.x64
```

### Quick Start

<i class="fa fa-hand-o-right"></i> Create at least one folder at the root of your project for your migration scripts and named them following the pattern described [here](/configuration/#naming-pattern). For example: `V1_3_1_1__Create_table.sql`

<i class="fa fa-hand-o-right"></i> In a **.NET Framework project**, add the following minimum configuration to your `app.config` or `web.config` file:

```xml
<appSettings>
  <add key="Evolve.Database" value="postgresql" /> <!-- or sqlite or sqlserver or mysql or mariadb or cassandra -->
  <add key="Evolve.ConnectionString" value="Server=127.0.0.1;Port=5432;Database=my_db;User Id=postgres;Password=postgres;" />
  <add key="Evolve.Locations" value="Sql_Scripts" />
  <add key="Evolve.Command" value="migrate" />
</appSettings>
```

<i class="fa fa-hand-o-right"></i> In a **.NET Core project**, add a new `evolve.json` file at the root of your project with the following minimum configuration:

```json
{
  "Evolve.Database": "sqlserver",
  "Evolve.ConnectionString": "Server=127.0.0.1;Database=Northwind;User Id=sa;Password=Password12!;",
  "Evolve.Locations": "Sql_Scripts/SQLServer/Sql",
  "Evolve.Command": "migrate"
}
```

### Configuration

All the options declared in the main [configuration](/configuration#options) page are available, as well as these 2 new mandatory ones:

| Name | Required | Description |
|-------------------------------|:--------:|-------------------------------------------------------------------|
| Evolve.Database | Yes | The type of database server: postgresql, sqlite, sqlserver, mysql, mariadb, cassandra or cockroachdb |
| Evolve.ConnectionString | Yes | The connection string to the database (can also be the name of a key in a connectionStrings section of your config file). Must have the necessary privileges to execute ddl. |