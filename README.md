# *-bootclasspath* sbt error
This file contains information about **sbt error** **`-bootclasspath`**.

We are facing this issue when we try to upgrade the environment in the project. 

> Note: - Since due to confidentiality we cannot disclose the code base
> of any related file for example sbt, therefore we attach a sample
> project with a simple `build.sbt`.

## Error
The error is as follows: -

    [error] missing argument for -bootclasspath
    [error] bad option: '-bootclasspath'
    [error] (Compile / compileIncremental) Compilation failed

This error occurs when we try to run the following command in order.

>  1. sbt
>  2. clean
>  3. compile

## Environment
The environment in which we were trying to run this: -

|  |  |
|--|--|
| Java | **AdoptOpenJDK Java 14.0.1** |
| SBT | **1.3.13** |
| Scala | **2.13.3** |
|  |  |

The previous successful build runs with the following environment: - 
|  |  |
|--|--|
| Java | **AdoptOpenJDK Java 8** |
| SBT | **1.3.3** |
| Scala | **2.12.8** |
|  |  |

## Build Result
If we revert to the original environment and then try to run these commands in order.

>  1. sbt --debug
>  2. clean
>  3. compile

We get the log as: -

> [debug] -bootclasspath   [debug]
> /usr/lib/jvm/adoptopenjdk-8-hotspot-amd64/jre/lib/resources.jar:/usr/lib/jvm/adoptopenjdk-8-hotspot-amd64/jre/lib/rt.jar:/usr/lib/jvm/adoptopenjdk-8-hotspot-amd64/jre/lib/sunrsasign.jar:/usr/lib/jvm/adoptopenjdk-8-hotspot-amd64/jre/lib/jsse.jar:/usr/lib/jvm/adoptopenjdk-8-hotspot-amd64/jre/lib/jce.jar:/usr/lib/jvm/adoptopenjdk-8-hotspot-amd64/jre/lib/charsets.jar:/usr/lib/jvm/adoptopenjdk-8-hotspot-amd64/jre/lib/jfr.jar:/usr/lib/jvm/adoptopenjdk-8-hotspot-amd64/jre/classes:/home/user/.cache/coursier/v1/https/path-to-scala/org/scala-lang/scala-library/2.12.8/scala-library-2.12.8.jar

but if we run it with an upgraded environment, we get the error as: -
 
    [error] missing argument for -bootclasspath
    [error] bad option: '-bootclasspath'
    [error] (Compile / compileIncremental) Compilation failed

## Sample-Code-Result

To debug this error, we first create a fresh virtual machine with `windows 10` operating system and installed the configuration at which we are facing the issue i.e. `Java 14`, `Scala 2.13`, `SBT 1.3.13`.

Then we run the following commands in order-

> 1. sbt --debug
> 2. clean
> 3. compile

And we get the successful compilation result having logs as:-

> [debug] The Scala compiler is invoked with:
> [debug] -bootclasspath
>[debug] C:\Users\User\AppData\Local\Coursier\cache\v1\https\repo1.maven.org\maven2\org\scala-lang\scala-library\2.13.3\scala-library-2.13.3.jar
>[debug] -classpath
>[debug] D:\bootclasspath-error\target\scala-2.13\classes
>[debug] Scala compilation took 3.2177838 s
>[debug] Done compiling.

It's a strange thing, that now on fresh machine it gets compiled successfully without any error but when trying to upgrade the environment we get an error for -bootclasspath.
