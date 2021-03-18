---
title: "Naming"
weight: 1
---

#### Versioned migration

To be processed by Evolve your [versioned migrations](/concepts/#versioned-migration) must follow this file name structure: **V1_3_1_1__Create_table.sql**:

- **prefix**: configurable, default: **V**
- **version**: numbers separated by **_** (one underscore)
- **separator**: configurable, default: **__** (two underscores)
- **description**: words separated by single underscores
- **suffix**: configurable, default: **.sql** 

#### Repeatable migration

[Repeatable migrations](/concepts/#repeatable-migration) must follow this file name structure: **R__Create_views.sql**:

- **prefix**: configurable, default: **R**
- **separator**: configurable, default: **__** (two underscores)
- **description**: words separated by single underscores
- **suffix**: configurable, default: **.sql** 
