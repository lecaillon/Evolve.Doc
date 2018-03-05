---
title: "FAQ"
draft: false
chapter: false
pre: "<b>6. </b>"
weight: 6
icon: ""
---

##### Can I modify the content of a migration after it has been applied ?

- Yes during the development phase. Besides the option `Evolve.EraseOnValidationError` is dedicated to this use case. 
- And no in production, because the checksum validation that Evolve executes before each migration would fail with no possibility to erase the database. Isn't it ?

##### Can multiple nodes migrate in parallel ?

Yes! Evolve will use the session level lock of your database to coordinate the migrations on multiple nodes. This prevents two distinct Evolve executions from executing an Evolve command on the same database at the same time.

##### Is it possible to get connection string from connectionStrings section ?

Yes! The option `Evolve.ConnectionString` can also be the name of a key in a connectionStrings section of your config file.

##### Can I provide configuration via environment variables ?

Yes! Use this syntax for your environment variables: `${DB_PWD}`