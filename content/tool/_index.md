---
title: "Evolve Tool"
draft: false
chapter: false
pre: "<b>7. </b>"
weight: 7
icon: ""
---

### Introduction

Evolve is also available as a .NET Core tool using the same commands and options than the [CLI](/cli/#command-structure). The only difference between the two is that the dotnet core tool requires the installation of the .NET Core SDK whereas the [CLI](/cli) is an entirely standalone single executable. See the [CLI documentation](/cli/#command-structure) to use it.

#### Installation as a .NET Core Global Tool

```
dotnet tool install --global Evolve.Tool
```

#### Installation as a .NET Core 3 Local Tool

```
dotnet new tool-manifest
dotnet tool install Evolve.Tool
```
