# Setting up SFML.NET using .NET Core

# Tools
* Visual Studio Code
  * C# Extension
* .NET Core 2+ 
* Windows 10
* Powershell

# Learning Outcomes
* Learn how to set up an exteremly basic SFML.Net Project that will run locally on .NET Core

# Method
1. Download and install Tools
2. Download CSFML dlls from the offical distribution source.
   1. Ensure you get the ones corresponding to your architecture.
3. Create a new .NET Core project
   1. Create project folder and navigate into it
   2. At the console, run `dotnet new console`
      1. If you're using the .NET Core 3 preview:
         1. In the generated .csproj file, change `<TargetFramework>netcoreapp3.0</TargetFramework>` to `<TargetFramework>netcoreapp2.2</TargetFramework>`. The minor version shouldn't be terribly important.
         2. Run `dotnet restore` to get the build system to pull the correct framework packages
         3. In `.vscode/launch.json`, change the `cwd` member to `"${workspaceFolder}/bin/Debug/netcoreapp2.2` 
4. Install required nuget packages. At the console, run `dotnet add package SFML.System.NetCore,SFML.Window.NetCore,SFML.Graphics.NetCore`. This will pull the SFML binding packages into your project. Note that as of the creation of this tutorial they do not contian the required binaries. Also note that additional packages `SFML.Audio.NetCore` and `SFML.Network.NetCore` are also available.
5. In the root project directory, create the folder tree `res/bin` and copy the CSFML dlls into this folder.
   1. They don't have to be in this folder, but this tutotiral will assume they are for simplicity.
6. In the .csproj file, add the following target after the PropertyGroup element. This will copy the dlls to the output directory after the build completes. `<Target Name="CopySFMLBinaries" AfterTargets="AfterBuild">
    <Copy SourceFiles="./res/bin/csfml-system-2.dll" DestinationFolder="$(OutDir)"/>
    <Copy SourceFiles="./res/bin/csfml-graphics-2.dll" DestinationFolder="$(OutDir)"/>
    <Copy SourceFiles="./res/bin/csfml-window-2.dll" DestinationFolder="$(OutDir)"/>
  </Target>`
7. Create a window and event loop.
    ![Alt text](tutorial/res/EventLoop.png?raw=true "Event Loop")
8. Create a shape and use the window to draw it.
    ![Alt text](tutorial/res/DrawingCommands.png?raw=true "Drawing A Shape")
  
