# NuGet .NET Core MultiTarget Error

##Reproduction of NuGet error installing multi-targeted .NET Core class library

## Part A: Multi-Targeted .NET Core Class Library

1. Create a .NET Core class library using Visual Studio 2015 Update 2

2. Add a target framework for **.NETPortable,Version=v4.5,Profile=Profile111**
  - Add framework assemblies

3. Change the netstandard target to 1.3
  - Add a dependency for System.ComponentModel.Annotations

4. Execute `dotnet pack` to compile and build a NuGet package

5. Copy the package to a local NuGet source


## Part B: CsProj-Based Project Compatible with NetStandard 1.3

1. Create both an Android and iOS project

2. Add the multi-targeted version of the .NET Core Class Library

3. The following error will take place and the package install will be rolled back:

  ```
  Failed to add reference to 'System.Collections'. Please make sure that it is in the Global Assembly Cache.
  ``` 

*Commenting out the portable target framework will allow the package install to succeed.*
