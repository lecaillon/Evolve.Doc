---
title: "Concepts"
draft: false
chapter: false
pre: "<b>4. </b>"
weight: 4
icon: ""
---

### Overview

In Evolve, each sql script is called a **migration**. A migration is composed of an unique version, an informative description and a checksum.

At startup Evolve will collect all migrations that are in the configured directories (cf. [Evolve.Locations](/configuration/#options)) searching recursively for files with a specific file name structure. All files are then sorted by version in ascending order, regardless their initial directory. **Each version of a migration must be unique**. If not, the validation phase fails.

Once executed, the name and the checksum of the migration is saved in the Evolve metadata table in your database (changelog by default). This table is checked everytime Evolve is run, to see if the migration script has already been executed.

### Migration

A migration is composed of a *version*, a *description* and a *checksum*.

#### Version

The version must be unique. It is used to ordered the execution of migrations. *The first numbers that make up the version of your migration may be the release version of your application followed by a counter.*

To be processed by Evolve your migration scripts must follow this file name structure: *V1_3_1__Create_table.sql*:

- **prefix**: configurable, default: **V**
- **version**: numbers separated by _ (one underscore)
- **separator**: configurable, default: **__** (two underscores)
- **description**: words separated by underscores
- **suffix**: configurable, default: **.sql** 

#### Description

The description is informative and allow you to remember what the migration was about.

#### Checksum

The checksum is stored in the Evolve metadatatable and used to detect accidental changes.

### Transactions

Each migration is executed in a separate database transaction. Thus each script will either succeed or fail completely and Evolve will stop on the first error. If your database supports DDL statements within a transaction, failed migrations will always be rolled back, otherwise you will have to manually cleanup the mess.

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

