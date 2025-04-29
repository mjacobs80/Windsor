# Castle Windsor

<img align="right" src="docs/images/windsor-logo.png">

Castle Windsor is a best of breed, mature Inversion of Control container available for .NET.

See the [documentation](docs/README.md).

## Considerations

Castle.Windsor.Extensions.DependencyInjection try to make Microsoft Dependency Injection works with Castle.Windsor. We have some
really different rules in the two world, one is the order of resolution exposed by the test Resolve_order_in_castle that shows
how the two have two different strategies.

1. Microsof DI want to resolve the last registered service
2. Castle.Windsor want to resolve the first registered service.

This is one of the point where the integration become painful, because it can happen that the very same service got resolved
in two distinct way, depending on who is resolving the service.

	The preferred solution is to understand who is registering the service and resolve everything accordingly.

## I want to try everything locally.

If you want to easily try a local compiled version on your project you can use the following trick.

1. Add the GenerateAssemblyInfo to false on the project file
1. Add an assemblyinfo.cs in Properties folder and add the [assembly: AssemblyVersion("6.0.0")] attribute to force the correct version
1. Compile the project
1. Copy into the local nuget cache, from the output folder of this project run

```
copy * %Uer Profile%\.nuget\packages\castle.windsor.extensions.dependencyinjection\6.0.x\lib\net8.0
```

This usually works.

## Releases

See the [releases](https://github.com/castleproject/Windsor/releases).

## License

Castle Windsor is &copy; 2004-2023 Castle Project. It is free software, and may be redistributed under the terms of the [Apache 2.0](http://opensource.org/licenses/Apache-2.0) license.

## NuGet Preview Feed

If you would like to use preview NuGet's from our CI builds on AppVeyor, you can add the following NuGet source to your project:

```
https://ci.appveyor.com/nuget/windsor-qkry8n2r6yak
```

## Building

### Conditional Compilation Symbols

The following conditional compilation symbols are currently defined for Windsor:

Symbol                              | .NET 4.6.2         | .NET Standard / 6
----------------------------------- | ------------------ | ------------------
`FEATURE_APPDOMAIN`                 | :white_check_mark: | :no_entry_sign:
`FEATURE_ASSEMBLIES`                | :white_check_mark: | :no_entry_sign:
`FEATURE_PERFCOUNTERS`              | :white_check_mark: | :no_entry_sign:
`FEATURE_REMOTING`                  | :white_check_mark: | :no_entry_sign:
`FEATURE_SECURITY_PERMISSIONS`      | :white_check_mark: | :no_entry_sign:
`FEATURE_SERIALIZATION`             | :white_check_mark: | :no_entry_sign:
`FEATURE_SYSTEM_CONFIGURATION`      | :white_check_mark: | :no_entry_sign:

* `FEATURE_APPDOMAIN` - enables support for features that make use of an AppDomain in the host.
* `FEATURE_ASSEMBLIES` - uses `AssemblyName.GetAssemblyName()` and `Assembly.LoadFile()`.
* `FEATURE_PERFCOUNTERS` - enables code that uses Windows Performance Counters.
* `FEATURE_REMOTING` - supports remoting on various types including inheriting from `MarshalByRefObject`.
* `FEATURE_SECURITY_PERMISSIONS` - enables the use of CAS and `Security[Critical|SafeCritical|Transparent]`.
* `FEATURE_SERIALIZATION` - enables support for serialization of dynamic proxies and other types.
* `FEATURE_SYSTEM_CONFIGURATION` - enables features that use `System.Configuration` and the `ConfigurationManager`.

The following conditional compilation symbols are defined for tests only under .NET 4.6.2:
* `FEATURE_CODEDOM` - enables code that uses `System.CodeDom`.
* `FEATURE_CONSOLETRACELISTENER` - enables code that requires `System.Diagnostics.ConsoleTraceListener`.
* `FEATURE_THREADABORT` - enables code that uses `Thread.Abort()`.
* `FEATURE_WPF` - enables code that uses `PresentationCore.dll`.
