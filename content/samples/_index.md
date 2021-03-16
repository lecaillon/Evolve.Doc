---
title: "Samples"
draft: false
chapter: false
pre: "<b>5. </b>"
weight: 5
icon: ""
---

#### Evolve ASP.NET Core

This sample demonstrates how to use Evolve to migrate a database in a ASP.NET Core environment.

<i class="fa fa-hand-o-right"></i> You can find the sample based on **file** migration scripts [here](https://github.com/lecaillon/Evolve/tree/master/samples/AspNetCoreSample_Evolve)

<i class="fa fa-hand-o-right"></i> And a sample using **embedded** migration scripts [here](https://github.com/lecaillon/Evolve/tree/master/samples/AspNetCoreSample_Evolve_EmbeddedResources)

##### Key points

- Different migration locations depending the environment (exclude _db/datasets_ migration folder from production)
- Use of `Placeholders` to replace a string _${table4}_ in a migration script (cf. V1_0_4__Create_table4_with_trigger.sql)
- Use **Microsoft.Extensions.Logging** to trace Evolve activity
- Ensure Evolve erase command is disabled
- Use of `Locations` or `EmbeddedResourceAssemblies` depending the sample you have chosen.
