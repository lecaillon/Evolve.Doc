---
title: "Samples"
draft: false
chapter: false
pre: "<b>5. </b>"
weight: 5
icon: ""
---

### ASP.NET Core sample

This sample targetting ASP.NET Core 2 and available [here](https://github.com/lecaillon/Evolve/tree/master/samples/AspNetCoreSample), demonstrates how to use Evolve to have a test database with specific datasets for your development environment, your CI and to keep up-to-date the production database at runtime.

#### Key points

- SQLite
- ASP.NET Core 2
- Use both MSBuild and In-App mode in the same project
- Different migration locations depending the Evolve mode used (**db/datasets** is excluded from production database environment)
- Use `Microsoft.Extensions.Logging` to trace Evolve activity
- Use of a placeholder in `evolve.json` to replace a string **${table4}** in a migration script (cf. `V1_0_4__Create_table4_with_trigger.sql`) 
- Use `evolve.json` configuration file in In-App mode
- Ensure Evolve erase command is disabled in production
