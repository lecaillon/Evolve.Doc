---
title: "CockroachDB"
draft: false
weight: 7
icon: "/images/CockroachDB.png"
---

#### Versions
- 2.0 and later

#### Limitations
- **No concurrent migration officially supported** because CockroachDB does not implement `pg_try_advisory_lock`. Evolve uses an alternative (but not battle tested) method discussed here: https://forum.cockroachlabs.com/t/alternatives-to-pg-advisory-locks/742.
