---
title: "CockroachDB"
draft: false
weight: 7
icon: "/images/CockroachDB.png"
---

### Versions
- 2.0 and later

### Limitations
- **No official support to coordinate the migrations on multiple nodes** because CockroachDB does not implement `pg_try_advisory_lock`. Evolve uses an alternative method discussed here: https://forum.cockroachlabs.com/t/alternatives-to-pg-advisory-locks/742, but not battle tested yet.
