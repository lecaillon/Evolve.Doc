---
title: "SQL Server"
draft: false
weight: 2
icon: "/images/SQLServer.png"
---

#### Versions
- 2008 and later

#### Limitations
- `USE (Transact-SQL)` : Because it changes the database context of the connection string to the specified database, it releases the lock Evolve uses to coordinate the migrations on multiple nodes. So to safely use this statement you can either:
    - use the **fully qualified name of your database objects** in your migration scripts (ex: mydb.dbo.table1)
    - disable option `EnableClusterMode`, because you run Evolve manually with the CLI or the Tool, or because you only have 1 instance of your app running Evolve at the same time.

