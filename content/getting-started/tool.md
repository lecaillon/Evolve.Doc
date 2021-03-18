---
title: ".NET tool"
draft: false
weight: 2
---

#### Introduction

If you prefer to manage your database migrations outside your application, Evolve is also available as a .NET tool. **Evolve.Tool** is a special NuGet package that contains a console application which requires .NET Core SDK 3.0 or later.

#### Installation

{{< tabs groupId="tool-installation" >}}
{{% tab name=".NET global tool" %}}
```powershell
dotnet tool install --global Evolve.Tool
```
{{% /tab %}}
{{% tab name=".NET local tool" %}}
```powershell
dotnet new tool-manifest
dotnet tool install Evolve.Tool
```
{{% /tab %}}
{{< /tabs >}}

#### Command structure

Evolve.Tool command structure consists of a [Command](#command-verb), a [Database](#database) and a list of [options](#options).

##### Command ("verb")

The command (or "verb") is simply a command that performs an action:

- `migrate`: applies the migrations.
- `erase`: erases the database schema(s) if Evolve has created it or has found it empty.
- `repair`: corrects checksums of already applied migrations, with the ones from actual migration scripts.
- `info`: displays the details and status information about all the migrations.

##### Database

The database is the name of the database management system to which the command will be applied:

- `postgresql`
- `sqlite`
- `sqlserver`
- `mysql`
- `mariadb`
- `cassandra`
- `cockroachdb`

##### Options

The options you pass on the command line are the options to the command invoked. They are the same that the one available in Evolve at the [configuration](/configuration/options) section, but with more suitable names for a CLI. Below the main options:

```xxx
Options:
  -?|-h|--help                 Show help information
  -c|--connection-string       The connection string to the target database engine.
  -l|--location                Paths to scan recursively for migration scripts. Default: Sql_Scripts
  -s|--schema                  A list of schemas managed by Evolve. If empty, the default schema is used.
  -p|--placeholder             Placeholders are strings to replace in scripts. Format for commandline is "key:value".
  --metadata-table             The name of the metadata table. Default: changelog
```

##### Options file

Evolve treats arguments beginning with **@** as a configuraiton file that contains additional options that will be treated as if they were passed in on the command line. This feature is very useful to avoid the repetition of parameters such as the database or the connection string.

#### Examples

<i class="far fa-hand-point-right"></i> A simple example of a PostgreSQL migration:

```powershell
evolve migrate postgresql -c "Server=127.0.0.1;Database=db1;User Id=postgres;Password=postgres;" -l "C:\db\migrations" -s public -s unittest -p schema1:unittest
```

<i class="far fa-hand-point-right"></i> The same example using a configuration file called `args.txt` located in the current directory:

```powershell
evolve migrate '@args.txt'
```

<i class="fa fa-file-o"></i> Content of `args.txt`

```powershell
postgresql -c "Server=127.0.0.1;Database=db1;User Id=postgres;Password=postgres;" -l "C:\db\migrations" -s public -s unittest -p schema1:unittest
```