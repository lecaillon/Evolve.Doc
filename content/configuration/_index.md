---
title: "Configuration"
draft: false
chapter: false
pre: "<b>3. </b>"
weight: 3
icon: ""
---

### Options

You can set all the options in the config file or directly access them  via properties in your code (cf. [In-App mode](/execution-modes/#in-app)).

| Name | Required | Default | Description |
|-------------------------------|:--------:|:-----------:|-------------------------------------------------------------------|
| Evolve.ConnectionString | Yes <span style=color:red>*</span> |  | The connection string to the database (can also be the name of a key in a connectionStrings section of your config file). Must have the necessary privileges to execute ddl. |
| Evolve.Driver | Yes <span style=color:red>*</span> |  | One of the following supported drivers: <ul><li>Npgsql</li><li>Microsoft.Data.Sqlite</li><li>System.Data.SQLite</li><li>SqlClient (SQL Server)</li><li>MySql.Data</li></ul> |
| Evolve.Locations | Yes | Sql_Scripts | Paths (separated by semicolon) to scan recursively for migrations |
| Evolve.EraseDisabled | No |  | When true, ensures that Evolve will never erase schemas. **Highly recommended in production.** |
| Evolve.Command | No | | <ul><li>**migrate**: migrates the database</li><li>**erase**: erases the database schema(s) Evolve has created or has found it empty</li><li>**repair**: corrects checksums of applied migrations, with the ones from migration scripts</li></ul> **When empty Evolve does nothing.** |
| Evolve.EraseOnValidationError | No |  | When true, if validation phase fails, Evolve will erase the database schemas and will re-execute migration scripts from scratch. **Intended to be used in development only.** |
| Evolve.Encoding | No | UTF-8 | The encoding of SQL migration files. |
| Evolve.SqlMigrationPrefix | No | V | Migration file name prefix. |
| Evolve.SqlMigrationSeparator | No | __ | Migration file name separator. |
| Evolve.SqlMigrationSuffix | No | .sql | Migration file name suffix. |
| Evolve.Schemas | No |  | A semicolon separated list of schema managed by Evolve.  If empty, the default schema for the datasource connection is used. |
| Evolve.MetadataTableSchema | No |  | The schema containing the metadata table. If empty, the first schema defined in Schemas or the one of the datasource connection. |
| Evolve.MetadataTableName | No | changelog | The metadata table name. |
| Evolve.PlaceholderPrefix | No | ${ | The prefix of the placeholders. |
| Evolve.PlaceholderSuffix | No | } | The suffix of the placeholders. |
| Evolve.Placeholder. | No |  | Placeholders are strings prefixed by: "Evolve.Placeholder." to replace in sql migrations. |
| Evolve.TargetVersion | No |  | Target version to reach. If empty it evolves all the way up. |
| Evolve.StartVersion | No | 0 | Version used as starting point for already existing databases. If empty, start version = 0. |
| Evolve.EnableClusterMode | No | true | When true, Evolve will use a session level lock to coordinate the migrations on multiple nodes. |

<span style=color:red>*</span> *Only required in [MSBuild mode](/execution-modes/#msbuild-dotnet-build).*
