---
title: "Samples"
draft: false
chapter: false
pre: "<b>7. </b>"
weight: 7
icon: ""
---

### Evolve ASP.NET Core

This sample demonstrates how to use **Evolve** to migrate a database in a ASP.NET Core environment.

<i class="fa fa-hand-o-right"></i> You can find this sample on [GitHub](https://github.com/lecaillon/Evolve/tree/master/samples/Evolve/AspNetCoreSample)

#### Key points

- Different migration locations depending the environment (exclude **db/datasets** migration folder from production)
- Use of a placeholder to replace a string **${table4}** in a migration script (cf. `V1_0_4__Create_table4_with_trigger.sql`)
- Use `Microsoft.Extensions.Logging` to trace Evolve activity
- Ensure Evolve erase command is disabled

### Evolve MSBuild ASP.NET Core

This ASP.NET Core sample demonstrates how to use **Evolve MSBuild** to migrate a database in an environment optimized for the development.

<i class="fa fa-hand-o-right"></i> You can find this sample on [GitHub](https://github.com/lecaillon/Evolve/tree/master/samples/Evolve.MSBuild/AspNetCoreSample2)

#### Key points

- Use `OutOfOrder` to apply migrations without taking care of their versions. Usefull when you work in a team where a lot of people are adding new scripts.
- Use `EraseOnValidationError` to erase database schemas and applied migrations from scratch, when Evolve validation fails. Usefull in developement, when your SQL scripts can still be updated.  
- Use of a placeholder to replace a string **${table4}** in a migration script (cf. `V1_0_4__Create_table4_with_trigger.sql`)
