While developing, you want to include Chisel code in a submodule so that it can be shared by different projects. To add a submodule to the Chipyard framework, make sure that your project is organized as follows.

```
yourproject/
    build.sbt
    src/main/scala/
        YourFile.scala
```

Put this in a git repository and make it accessible. Then add it as a submodule to under the following directory hierarchy: `generators/yourproject`.

The `build.sbt` is a minimal file which describes metadata for a Chisel project. For a simple project, the `build.sbt` can even be empty, but below we provide an example build.sbt.

```
organization := "edu.berkeley.cs"

version := "1.0"

name := "yourproject"

scalaVersion := "2.12.4"
```
```
cd generators/
git submodule add https://git-repository.com/yourproject.git
```

Then add `yourproject` to the Chipyard top-level build.sbt file.

```
lazy val yourproject = (project in file("generators/yourproject")).settings(commonSettings).dependsOn(rocketchip)
```

You can then import the classes defined in the submodule in a new project if you add it as a dependency. For instance, if you want to use this code in the `chipyard` project, change the final line in build.sbt to the following.

```
lazy val chipyard = (project in file(".")).settings(commonSettings).dependsOn(testchipip, yourproject)
```





my rocket chip config with hwacha coprocessor
