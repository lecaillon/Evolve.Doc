---
title: "FAQ"
draft: false
chapter: false
pre: "<b>6. </b>"
weight: 6
icon: ""
---

##### Can I modify the content of a migration after it has been applied ?

- Yes, in development. The `MustEraseOnValidationError` option is provided specifically for this use case. 
- No, in production. The checksum validation performed by Evolve will fail. Since we're in production, erasing the data and starting over will likely not be an option.

##### Can multiple nodes migrate in parallel ?

Yes! Evolve will use the session level lock of your database to coordinate the migrations on multiple nodes. This prevents two distinct Evolve executions from running an Evolve command on the same database at the same time.

