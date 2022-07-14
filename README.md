# dotnetcore-github-setup

This repo is an example of creating a .NET 6 project with its setup using GitHub.

All executed commands are collected here:

## Initial Setup

- Create new repository in github.
- Move to the desired parent folder where we are going to clone the repository.
- Clone the repository: git clone https://github.com/fjegear/dotnetcore-github-setup.git
- Create solution file: dotnet new sln --name DotnetCoreExample
- Create folder for source code projects: mkdir src
- Create folder for tests projects: mkdir tests
- Create folder for build files and artifacts: mkdir build
- Create class library project: dotnet new classlib --name MyLibrary --output .\src\MyLibrary
- Add the new project to the solution: dotnet sln add .\src\MyLibrary\MyLibrary.csproj
- Create tests project: dotnet new xunit --name UnitTests --output .\tests\UnitTests
- Add the new tests project to the solution: dotnet sln add .\tests\UnitTests\UnitTests.csproj
- Test building the solution: dotnet build
- Create a global.json file to fix some characteristics across all the projects like dotnet version: dotnet new global.json
- Create a tool manifest to help new contributors to install all necessary tools in the project: dotnet new tool-manifest
- Now if you install dotnet EF CLI, it will be added to the tool manifest: dotnet tool install dotnet-ef
- A new collaborator would run 'dotnet tool restore' to install all needed tools

## Configure projects files to use variables instead of fixed values

- Create Directory.Build.props file in the repo root folder and reference file dependencies.props in the build folder.
- Create file dependencies.props in the build folder and add the netcore app and netstandard versions as variables.
- In the Directory.Build.props file metadata information can be included like Author, Company, LangVersion, ...
- Replace all fixed values in projects with $(variableName).
- Create Directory.Build.targets file and copy item groups from csproj files to this new file, change 'Include' word by 'Update' word.
- In the original csproj file remove version property.

- In the original csproj file you can add additional properties like PackageVersion or Description.

## Configure for SourceLink and deterministics builds

- SourceLink allows to debug the OSS library by using symbols .net technology.
- To check if it is enabled, tool Nuget Package Explorer can be used and check whether SourceLink and Deterministic are enabled.
- To enable it some metadata need to be added to the Directory.Build.props file. (see file).

## Add script files to build the projects locally