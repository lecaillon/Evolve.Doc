---
title: "MSBuild task"
draft: false
weight: 1
---

Evolve.MSBuild NuGet installation adds a new post-build MSBuild task to your project. This task is automatically executed after a successful build and starts the Evolve command (cf. Evolve.Command in the [options](/configuration/#options)) defined in your configuration file, if one is found. If the command fails, the entire MSBuild process is stopped with an error.

Here is the .NET Framework version of the `Evolve.MSBuild.Windows.x64.targets` file:

```xml
<Project ToolsVersion="15.0" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <UsingTask TaskName="Evolve.MSBuild.EvolveBoot" AssemblyFile="$(MSBuildThisFileDirectory)Evolve.MSBuild.dll" />
  <Target Name="SqlMigration" AfterTargets="Build">
    <Message Condition="!Exists('Web.config') AND !Exists('App.config')" Importance="High" Text="Evolve MSBuild mode is off: no configuration file found." />
    <EvolveBoot Condition="Exists('Web.config') OR Exists('App.config')"
                Configuration="$(Configuration)"
                IsDotNetCoreProject="false"
                EvolveCliDir="$([System.IO.Path]::GetFullPath($(MSBuildThisFileDirectory)..\..\tools))" 
                ProjectDir="$([MSBuild]::Unescape($(ProjectDir)))" 
                TargetPath="$([MSBuild]::Unescape($(TargetPath)))" />
  </Target>
</Project>
```

<i class="fa fa-hand-o-right"></i> If the option **Evolve.Command** is null or empty, the MSBuild task does nothing.
