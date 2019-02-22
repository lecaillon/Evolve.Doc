---
title: "Getting Started"
draft: false
chapter: false
pre: "<b>2. </b>"
weight: 2
icon: ""
---

### Introduction

Evolve 2.0 is the first major rewrite version. It will help simplify the overall design by getting rid of the hard to maintain dynamic database driver loading. The benefits: a simpler code base, a simpler test infrastructure, more time to develop new features. Evole is now decoupled from its MSBuild part and fully compatible with .NET Standard 2.0

### Installation

Evolve is available as a single [NuGet package](https://www.nuget.org/packages/Evolve).

```
Install-Package Evolve
```

### Quick Start

<i class="fa fa-hand-o-right"></i> Initialize and [configure](/configuration/#options) Evolve to run when you start your application:

```C#
try
{
    var cnx = new SqliteConnection(Configuration.GetConnectionString("MyDatabase"));
    var evolve = new Evolve.Evolve(cnx, msg => _logger.LogInformation(msg))
    {
        Locations = new[] { "db/migrations" },
        IsEraseDisabled = true,
    };

    evolve.Migrate();
}
catch (Exception ex)
{
    _logger.LogCritical("Database migration failed.", ex);
    throw;
}
```

<i class="fa fa-hand-o-right"></i> Create at least one folder at the root of your project for your migration scripts and named them following the pattern described [here](/configuration/#naming-pattern). For example: `V1_3_1_1__Create_table.sql`

<i class="fa fa-hand-o-right"></i> Make sure to set the property `Copy to output directory` to **Copy always** on each of your migration script, or modify your csproj file to automatically copy all the SQL files to the output build folder:

```xml
<ItemGroup>
  <Content Include="db\migrations\**\*.sql">
    <CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>
  </Content>
</ItemGroup>
```
<i class="fa fa-info-circle"></i> Note that since Evolve 2.1.0, you can embed your migration scripts into assemblies.