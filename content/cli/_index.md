---
title: "Evolve CLI"
draft: false
chapter: false
pre: "<b>6. </b>"
weight: 6
icon: ""
---

### Introduction

The Evolve command-line interface (CLI) is the ideal tool to manage your different database migrations. It is a standalone binary file. No runtime needed in order to use it. 

Currently, we provide Evolve.CLI binaries for the following x64 architecture:

- Windows
- Linux

### Installation

Download the appropriate version for your platform from Evolve [releases](https://github.com/lecaillon/Evolve/releases). 

### Command structure

CLI command structure consists of a [Command](#command-verb), a [Database](#database) and a list of [options](#options).

#### Command ("verb")

The command (or "verb") is simply a command that performs an action:

- `migrate`: applies the migrations
- `erase`: erases the database schema(s) if Evolve has created it or has found it empty
- `repair`: corrects checksums of already applied migrations, with the ones from actual migration scripts

#### Database

The database is the name of the database management system to which the command will be applied:

- `postgresql`
- `sqlite`
- `sqlserver`
- `mysql`
- `mariadb`
- `cassandra`

#### Options

The options you pass on the command line are the options to the command invoked. They are the same that the one available in Evolve at the [configuration](/configuration#options) section, but with more suitable names for a CLI. Below the main options:

```
Options:
  -?|-h|--help                 Show help information
  -c|--connection-string       The connection string to the target database engine. Must have the necessary privileges to execute ddl.
  -l|--location                Paths to scan recursively for migration scripts. Default: Sql_Scripts
  -s|--schema                  A list of schemas managed by Evolve. If empty, the default schema for the datasource connection is used.
  -p|--placeholder             Placeholders are strings to replace in migration scripts. Format for commandline is "key:value".
  --metadata-table             The name of the metadata table. Default: changelog
```

### Example

```
evolve migrate postgresql -c "Server=127.0.0.1;Database=db1;User Id=postgres;Password=postgres;" -l "C:\db\migrations" -s public -s unittest -p schema1:unittest
```