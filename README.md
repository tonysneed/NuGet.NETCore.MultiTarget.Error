# NuGet .NET Core MultiTarget Error

##Reproduction of NuGet error installing multi-targeted .NET Core class library

## Part A: Multi-Targeted .NET Core Class Library

1. Create a .NET Core class library using Visual Studio 2015 Update 2.

2. Add a target framework for **.NETPortable,Version=v4.5,Profile=Profile111**.
  - Add framework assemblies

3. Change the netstandard target to 1.3
  - Add a dependency for System.ComponentModel.Annotations

4. Execute `dotnet pack` to compile and build a NuGet package.

5. Copy the package to a local NuGet source.


## Part B: CsProj-Based Project Compatible with NetStandard 1.3

1. Create both an Android and iOS project.

2. Add the **multi-targeted** version of the .NET Core Class Library.

3. The following error will take place and the package install will be rolled back:

  ```
  Failed to add reference to 'System.Collections'. Please make sure that it is in the Global Assembly Cache.
  ``` 

4. The same error will occur with the **portable** *only* version of the .NET Core Class Library.

5. The error will **not** occur with the **netcore** *only* version of the .NET Core Class Library.

*If System.Collections is removed from framework assemblies, then the following error takes place:*

  ```
  Failed to add reference to 'System.ComponentModel'. Please make sure that it is in the Global Assembly Cache.
  ``` 


## Part C: Portable Class Library Profile 111

1. Both the **multi-targeted** and **portable** versions of the .NET Core Class Library will install successfully.