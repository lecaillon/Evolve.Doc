---
title: "PostgreSQL"
draft: false
weight: 1
icon: "/images/PostgreSQL.png"
---

#### Versions
- 9.0 and later

#### Limitations
> Instructions that do not support being embedded in a transaction are not yet supported in migration scripts:

- CREATE INDEX CONCURRENTLY
- CREATE/DROP DATABASE
- COPY FROM STDIN
- VACUUM
