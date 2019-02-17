---
title: "Samples"
draft: false
chapter: false
pre: "<b>7. </b>"
weight: 7
icon: ""
---

### Evolve ASP.NET Core

This sample demonstrates how to use **Evolve** to migrate a database in a ASP.NET Core environment

<i class="fa fa-hand-o-right"></i> You can find this sample on [GitHub](https://github.com/lecaillon/Evolve/tree/master/samples/Evolve/AspNetCoreSample)

#### Key points

- Different migration locations depending the environment (exclude **db/datasets** migration folder from production)
- Use of a placeholder to replace a string **${table4}** in a migration script (cf. `V1_0_4__Create_table4_with_trigger.sql`)
- Use `Microsoft.Extensions.Logging` to trace Evolve activity
- Ensure Evolve erase command is disabled
