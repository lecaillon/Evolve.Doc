---
title: "Concepts"
draft: false
chapter: false
pre: "<b>4. </b>"
weight: 4
icon: ""
---

### Overview

In Evolve, each sql script is called a **migration**. There are two different types:

- [Versioned migration](#versioned-migration)
- [Repeatable migration](#repeatable-migration)

At startup Evolve will collect all migrations located in [Evolve.Locations](/configuration/#options), searching recursively for files with a specific file name structure. All migrations starting by a **V** are then sorted by version in ascending order, regardless their initial directory. **Each version of a migration must be unique**. If not, the validation phase fails.

Once executed, the same goes for repeatable migrations, starting by a **R**, except ordered by description.

When all migrations are applied, their name and checksum are saved into the Evolve metadata table. This table is checked every time Evolve runs, to see if the migration script has already been applied.

<i class="fa fa-info-circle"></i> _Repeatable migration is available since Evolve 2.2.0._

### Versioned migration

A versioned migration is composed of a **version**, an informative **description** and a **checksum**. The first numbers that make up the version of your migration may be the release version of your application followed by a counter.

<i class="fa fa-exclamation-triangle"></i> A versioned migration is executed only once.

<i class="fa fa-hand-o-right"></i> The version must be unique.

<i class="fa fa-hand-o-right"></i> They are applied in the order of their versions.

<i class="fa fa-hand-o-right"></i> The checksum is stored in the Evolve metadata table and used to detect accidental changes.

#### Naming

Versioned migration must follow this file name structure: **V1_3_1_1__Create_table.sql**:

- **prefix**: configurable, default: **V**
- **version**: numbers separated by **_** (one underscore)
- **separator**: configurable, default: **__** (two underscores)
- **description**: words separated by single underscores
- **suffix**: configurable, default: **.sql** 

### Repeatable migration

Unlike the versioned migration above, repeatable migrations are applied whenever their content changes. They do not have a version and are executed sorted by name.
You can use them to manage database objects you can create or update such as views and stored procedures, or to insert seed data that can evolve and grow over time.

<i class="fa fa-exclamation-triangle"></i> A repeatable migration is executed each time its content (checksum) changes.

<i class="fa fa-hand-o-right"></i> They are applied **after** versioned migrations.

<i class="fa fa-hand-o-right"></i> They are applied in the order of their description.

#### Naming

Repeatable migrations must follow this file name structure: **R__Create_views.sql**:

- **prefix**: configurable, default: **R**
- **separator**: configurable, default: **__** (two underscores)
- **description**: words separated by single underscores
- **suffix**: configurable, default: **.sql** 

### Commands

Evolve has 3 execution commands to interact with your database:

<i class="fa fa-hand-o-right"></i> **migrate**: applies the migrations. It's the main command. 

<i class="fa fa-hand-o-right"></i> **erase**: erases the database schema(s) if Evolve has created it or has found it empty (cf. [Metadata table](#metadata-table)). Otherwise Evolve will not do anything. This command is intended to be use in development to start with a new clean database.

<i class="fa fa-hand-o-right"></i> **repair**: updates checksums of previously applied migrations with those of the currently available migration scripts.

### Transactions

Each migration is executed in a separate database transaction. Thus each script will either succeed or fail completely and Evolve will stop on the first error. If your database supports DDL statements within a transaction, failed migrations will always be rolled back, otherwise you will have to manually fix your database state.

### Placeholders

Placeholders are strings prefixed by: *Evolve.Placeholder.* that will be replaced in sql migrations before their execution. They make it possible to get dynamic migrations depending on the environment.

```xml
<add key="Evolve.Placeholder.schema1" value="my_schema" />
<add key="Evolve.Placeholder.database" value="my_db" />
```

```sql
SELECT * FROM ${database}.${schema1}.TABLE_1; -- SELECT * FROM my_db.my_schema.TABLE_1;
```

### Metadata table

During its initial execution, Evolve creates a table with a default name of **changelog**, to keep track of all migrations (applied or failed) and to store their checksums. Example:

| id | type | version | description | name | checksum | installed_by | installed_on | success |
|----|:----:|---------|-------------|------|----------|-------------|--------------|:-------:|
| 1 | 2 | 0 | Empty schema found: dbo. | dbo | | sa | 22/02/2019 20:45:15 | True |
| 2 | 0 | 1.0.0.0 | create table calendrier and constraints | V1_0_0_0__create_table_calendrier_and_constraints.sql | D4AAF08FBF70D3B327A9A3D3B4E0E21A | sa | 22/02/2019 20:45:15 | True |
| 3 | 0 | 1.0.0.1 | create triggers | V1_0_0_1__create_triggers.sql | A4AA367C92B99C56E881324726882B9B | sa | 22/02/2019 20:45:16 | True |
| 4 | 4 | | Create views | R__Create_views.sql | Z6AA3T7C92B549C56E8813TA726882B9T | sa | 22/02/2019 20:45:18 | True |

<i class="fa fa-hand-o-right"></i> The `type` column is used to identify which type of metadata is stored:

- 0: versioned migration.
- 1: new schema. Indicates that Evolve created the schema and thus can **drop** it if `Evolve.Command = "erase"`.
- 2: empty schema. Indicates that the schema was empty before Evolve applied the first migration and thus can **erase** it if `Evolve.Command = "erase"`. 
- 3: start version. Used by Evolve to store the version from which to take migrations (cf. `Evolve.StartVersion`).
- 4: repeatable version.
