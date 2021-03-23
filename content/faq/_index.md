---
title: "FAQ"
draft: false
chapter: false
pre: "<b>6. </b>"
weight: 6
icon: ""
---

##### <i class="fas fa-check"></i> Can I modify the content of a migration after it has been applied ?
- Yes, in development. The `MustEraseOnValidationError` option is provided specifically for this use case. 
- No, in production. The checksum validation performed by Evolve will fail. Since we're in production, erasing the data and starting over will likely not be an option.

##### <i class="fas fa-check"></i> Can multiple nodes migrate in parallel ?
Yes! Evolve will use the session level lock of your database to coordinate the migrations on multiple nodes. This prevents two distinct Evolve executions from running an Evolve command on the same database at the same time.

##### <i class="fas fa-check"></i> Can I mark a migration as already executed ?
Yes! Sometimes a hotfix is quickly applied in production without a proper Evolve migration. To ensure consistency across all environments, a migration matching those changes must be added to version control but skip in production. Use the option `SkipNextMigrations` to fix this issue.

##### <i class="fas fa-check"></i> Can I control how Evolve manages SQL transactions ?
Yes! By default each migration script is executed in a separate database transaction. But you can either wrap all your migrations in a single transaction using the option `TransactionMode` with the value `CommitAll` in a "all or nothing" mode, or disable transaction for one specific script writing **-- evolve-tx-off** at the beginning of the file.

##### <i class="fas fa-check"></i> Can I test a migration without commit any changes ?
Yes! Sometimes it is usefull to run Evolve and trigger a rollback without error after the last successful script. That way upgrades can be tested against an existing database prior to doing the real thing. Keep in mind that all databases do not support DDL instructions in transaction. In this case Evolve won’t be able to perform a clean rollback. That is why **it is absolutely not recommended to use this option with MySQL/MariaDB, CockroachDB and Cassandra**.

To run Evolve in a _dry run_ mode, use the option `TransactionMode` with the value `RollbackAll`

##### <i class="fas fa-check"></i> Can I preview the changes Evolve will make to the database ?
Yes! Evolve **info** command displays the details and status information about all past and future migrations.
