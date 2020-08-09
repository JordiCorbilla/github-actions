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

