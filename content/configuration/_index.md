---
title: "Configuration"
draft: false
chapter: false
pre: "<b>3. </b>"
weight: 3
icon: ""
---

### Versioned migration naming pattern

To be processed by Evolve your [versioned migrations](/concepts/#versioned-migration) must follow this file name structure: **V1_3_1_1__Create_table.sql**:

- **prefix**: configurable, default: **V**
- **version**: numbers separated by **_** (one underscore)
- **separator**: configurable, default: **__** (two underscores)
- **description**: words separated by single underscores
- **suffix**: configurable, default: **.sql** 

### Repeatable migration naming pattern

[Repeatable migrations](/concepts/#repeatable-migration) must follow this file name structure: **R__Create_views.sql**:

- **prefix**: configurable, default: **R**
- **separator**: configurable, default: **__** (two underscores)
- **description**: words separated by single underscores
- **suffix**: configurable, default: **.sql** 

### Options

_Note that you can also use them through your config file if you use [Evolve.MSBuild](/msbuild)_

| Name | Required | Default | Description |
|-------------------------------|:--------:|:-----------:|-------------------------------------------------------------------|
| Evolve.Locations | Yes/No <span style=color:red>*</span> | Sql_Scripts | Paths (separated by semicolon) to scan recursively for migrations. <span style=color:red>*</span>Mandatory only if **Evolve.EmbeddedResourceAssemblies** is empty. |
| Evolve.EmbeddedResourceAssemblies | Yes/No <span style=color:red>*</span> | | Assemblies (separated by semicolon) to scan to load embedded migration scripts. <span style=color:red>*</span>Mandatory only if **Evolve.Locations** is empty. |
| Evolve.EmbeddedResourceFilters | No | | Excludes embedded migration scripts that do not start with one of these filters (separated by semicolon). |
| Evolve.EraseDisabled | No |  | When true, ensures that Evolve will never erase schemas. **Highly recommended in production.** |
| Evolve.Command | No | | <ul><li>**migrate**: applies the migrations</li><li>**erase**: erases the database schema(s) if Evolve has created it or has found it empty</li><li>**repair**: corrects checksums of already applied migrations, with the ones from actual migration scripts</li></br><li>**when empty Evolve does nothing.**</li></ul> |
| Evolve.CommandTimeout | No |  | The time in seconds to wait for the migration to execute before terminating the command and generating an error. |
| Evolve.Schemas | No |  | A semicolon separated list of schema managed by Evolve.  If empty, the default schema for the datasource connection is used. |
| Evolve.EraseOnValidationError | No |  | When true, if validation phase fails, Evolve will erase the database schemas and will re-execute migration scripts from scratch. **Intended to be used in development only.** |
| Evolve.TargetVersion | No |  | Target version to reach. If empty it evolves all the way up. |
| Evolve.StartVersion | No | 0 | Version used as starting point for already existing databases. If empty, start version = 0. |
| Evolve.OutOfOrder | No | false | Allows migrations to be run "out of order". If you already have versions 1 and 3 applied, and now a version 2 is found, it will be applied too instead of being ignored. |
| Evolve.Encoding | No | UTF-8 | The encoding of SQL migration files. |
| Evolve.SqlMigrationPrefix | No | V | Migration file name prefix. |
| Evolve.SqlRepeatableMigrationPrefix | No | R | Repeatable migration file name prefix. |
| Evolve.SqlMigrationSeparator | No | __ | Migration file name separator. |
| Evolve.SqlMigrationSuffix | No | .sql | Migration file name suffix. |
| Evolve.MetadataTableSchema | No |  | The schema containing the metadata table. If empty, the first schema defined in Schemas or the one of the datasource connection. |
| Evolve.MetadataTableName | No | changelog | The metadata table name. |
| Evolve.PlaceholderPrefix | No | ${ | The prefix of the placeholders. |
| Evolve.PlaceholderSuffix | No | } | The suffix of the placeholders. |
| Evolve.Placeholder. | No |  | Placeholders are strings prefixed by: "Evolve.Placeholder." to replace in sql migrations. |
| Evolve.EnableClusterMode  | No | true | When true, Evolve will use a session level lock to coordinate the migrations on multiple nodes. This prevents two distinct Evolve executions from executing an Evolve command on the same database at the same time. |
