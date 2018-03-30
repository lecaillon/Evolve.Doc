---
title: "Cassandra"
draft: false
weight: 6
icon: "/images/Cassandra.png"
---

### Versions
- 1.2+ of Cassandra with CQL v3 (dependent on the driver, see below)

### Drivers
- [CassandraCSharpDriver](https://github.com/datastax/csharp-driver)
  - Evolve uses the [ADO.NET capabilities of the drivers](https://github.com/datastax/csharp-driver/tree/master/src/Cassandra/Data); it is not recommended to use it, but it is good enough for our purpose with Evolve.

### Limitations

- The parser will divide scripts in commands by dividing it into lines and look for lines that finish with the ';' character; make sure all your commands end with a ';' that is the last character of a line.
  - If a line in a comment or a literal ends with ';', it will be an issue: avoid it.
- If Evolve has to create a keyspace because it does not exist, it will create it using the ```SimpleStrategy``` replication strategy with a replication factor of 1 (see [create keyspace documentation](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/create_keyspace_r.html)
)
  - You can alter that replication strategy later in one of your script if you like, but you will then have to run the ```nodetool repair -full``` on each node, as described in the [Changing keyspace replication strategy procedure](https://docs.datastax.com/en/cassandra/3.0/cassandra/operations/opsChangeKSStrategy.html).
- If you use the same keyspace for your data and the the metadata table of Evolve, Evolve will create that keyspace prior to running migration scripts if it does not exist (see above); make sure that your script creates the keyspace with the ```if not exists``` parameter in that case.
- The ```use <keyspace>;``` command is not supported. Make sure you prefix all your table names with their respective keyspace in all commands.
- The migration does not use any locking mechanism at the moment, this is to be done.

### TODO

 - Locking mechanism to prevent multiple execution of the transaction (in the log table, using LWT)
 - Allow configuration of the default replication strategy when Evolve creates a keyspace