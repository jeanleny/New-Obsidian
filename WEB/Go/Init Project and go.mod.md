[GoDoc](https://go.dev/learn/#guided-learning-journeys)

Create the repo containing the Project.
First create the mod.init :
``` bash 
go mod init <moduleName>
```

This will create the **.mod** file.
This file is the dependency tracking manager of your project.
When we import code and packages from other modules, we manage it our **go.mod** file.
It will tracks the modules and provide those packages.

The `go mod init` takes the module name where the code will be in. Its the path of the module.

In Go the module  path will often be the github repo where all the code is stored.
