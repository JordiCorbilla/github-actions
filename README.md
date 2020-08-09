# Github Actions

## GitHub Actions to publish Artifacts.

In this article you'll find how easy and simple it is to generate your .net core artifacts (binaries) using Github Actions. 

## Adding your action

Github offers a set of predefined actions that you can use to leverage the needs of your deployment machine. Maybe you need to generate artifacts for a Windows machine or Mac, or Linux and you want to generate all of them without having to build thing separately. The easiest way to use continuous integration through Github Actions is via a workflow configuration file. Go to Actions and click new workflow:

![](https://github.com/JordiCorbilla/github-actions/raw/master/githubactions.png)

Select the netcore action to build your .net core application:

![](https://github.com/JordiCorbilla/github-actions/raw/master/netcoreaction.png)

This will open up the following YAML configuration file that we can edit to configure it according to the needs of our project:

![](https://github.com/JordiCorbilla/github-actions/raw/master/workflow.png)

## Configuring your workflow file

The file below specifies building my .net core application using a specific folder and then I publish the binaries that will be available in the action's artifacts section. The package has been configured for Windows x64, .net core 3.1.6 and the package is self-contained (meaning that the .net core libraries will become part of the artifact).

```yaml
name: my Project

on:
  push:
    branches: [ master ]
  pull_request:
    branches: [ master ]

defaults:
  run:
    working-directory: myASPNETCoreApp

jobs:
  build:

    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v2
    - name: Setup .NET Core
      uses: actions/setup-dotnet@v1
      with:
        dotnet-version: 3.1.302
    - name: Install dependencies
      run: dotnet restore
    - name: Build Project
      run: dotnet build --configuration Release --no-restore
    - name: Test Project
      run: dotnet test --no-restore --verbosity normal
    - name: Publish
      run: dotnet publish --configuration Debug --framework netcoreapp3.1 --runtime win-x64 --self-contained true
    - name: Upload a Build Artifact
      uses: actions/upload-artifact@v2.1.1
      with:
        name: myproject-win-64
        path: /home/runner/work/myproject/myproject/myASPNETCoreApp/bin/Debug/netcoreapp3.1/win-x64/publish/
```

