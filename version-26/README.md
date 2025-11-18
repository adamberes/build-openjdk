# Build OpenJDK Version 26 from Sources in Windows 11 without WSL

Here a detailed description about building the OpenJDK from sources.

Following prerequisites are have to be installed befor compiling the sources for Windowns Environment.

- 1)Here the [build description from OpenJDK](https://openjdk.org/groups/build/doc/building.html)

- 2)OpenJDK one of the latest versions must be installed locally. If the target version, what will be here compiled is the Version 25 then the installed Version of OpenJDK cant be earlier as 23, but for this existing a clear Error message bei generating the make files.

    - [Download OpenJDK Version 25](https://jdk.java.net/25/)
    - Unzip the jdk in Directory: c:\bin2025\jdk-build\jdk-25


- 3)The C++ Compiler well be needed from Microsoft, is included in the Comunity Edition from Microsoft Visual Studio.
[Visual Studio 2022 Community Edition](https://visualstudio.microsoft.com/de/downloads/)(at 18.11.2025)
Only the "The Desktop development with C++", the "out-of-support components" can be disabled.
Here the [suported Visual Studio Version by OpenJDK](https://wiki.openjdk.org/display/Build/Supported+Build+Platforms)

     - [Here a Screen-Shot about the C++ components that is needed.](../screen-shots/visual-studio.jpg) 
     - [Here a Screen-Shot about the English language (in german Language:"Sprachpackete") pack that is needed.](../screen-shots/visual-studio2.jpg) 


- 4)Cygwin will be also needed with some additional Components. On the [Cygwin Homepage](https://cygwin.com/) download the [Cygwin Installer](https://cygwin.com/setup-x86_64.exe)
  Execute the folowing command to install additional components like: Make,Autoconf,Unzip,Zip and Wget.
  ```
  C:\setup-x86_64.exe -q --packages=make,autoconf,unzip,zip,wget
  ```
- 5)Git is also needed. Download and install from: [Git Download for Windows](https://git-scm.com/downloads/win)


- 6)Install the [English Language Pack for the USA in Windows](../screen-shots/setting-windows2.jpg) this will be needed by the generation of the make file for the process.


- 7)Install JTReg (JTReg is similar to JUnit but is older as JUnit) from the [OpenJDK JTReg builds](https://builds.shipilev.net/jtreg/)
  **Important**: use always the latest version of JTReg.


## Now execute the folowing steps to build the OpenJDK
The Build Process will be done under the Cygwin Environment.

  ```
  open a Cygwin Shell with Cygwin.bat
  # now we are in the home directory from the logged in user
  # download the latest JTReg
  wget https://builds.shipilev.net/jtreg/jtreg-8.1+1.zip
  # unzip 
  unzip jtreg-8.1+1.zip
  # clone OpenJDK from main development (Version 26 is now not released)
  git clone https://github.com/openjdk/jdk.git
  # cd in the directory: jdk 
  # run configure to generate the file: make 
  bash configure --with-boot-jdk=/cygdrive/c/bin2025/jdk-build/jdk-25 --with-jtreg=/home/info/jtreg/ 
  ```
The result is something similar:
  wget https://builds.shipilev.net/jtreg/jtreg-8.1+1.zip
  ### unzip JTReg the latest version
  ```
  $ unzip jtreg-8.1+1.zip
  ```
  ### clone OpenJDK from main development (Version 26 is now not released)
  ```
  $ git clone https://github.com/openjdk/jdk.git
  ```
  ### cd in the directory: jdk 
  ```
  $ cd jdk
  ```
  ### run "configure" to generate the "make" file 
  ```
  $ bash configure --with-boot-jdk=/cygdrive/c/bin2025/jdk-build/jdk-25 --with-jtreg=/home/info/jtreg/ 
  ```
The result is something similar:
  ```
====================================================
A new configuration has been successfully created in
/home/info/jdk/build/windows-x86_64-server-release
using configure arguments '--with-boot-jdk=/cygdrive/c/bin2025/java-bin/jdk-25.0.1 --with-jtreg=/home/info/jtreg/'.

Configuration summary:
* Name:           windows-x86_64-server-release
* Debug level:    release
* HS debug level: product
* JVM variants:   server
* JVM features:   server: 'cds compiler1 compiler2 epsilongc g1gc jfr jni-check jvmci jvmti management parallelgc serialgc services shenandoahgc vm-structs zgc'
* OpenJDK target: OS: windows, CPU architecture: x86, address length: 64
* Version string: 26-internal-adhoc.info.jdk (26-internal)
* Source date:    1762286811 (2025-11-04T20:06:51Z)

Tools summary:
* Environment:    cygwin version 3.6.5-1.x86_64, 2025-10-09 17:21 UTC; windows version 10.0.26200.7019; prefix "/cygdrive"; root "C:\cygwin64"
* Boot JDK:       openjdk version "25.0.1" 2025-10-21 OpenJDK Runtime Environment (build 25.0.1+8-27) OpenJDK 64-Bit Server VM (build 25.0.1+8-27, mixed mode, sharing) (at /cygdrive/c/bin2025/java-bin/jdk-25.0.1)
* Toolchain:      microsoft (Microsoft Visual Studio 2022)
* C Compiler:     Version 19.44.35219 (at /cygdrive/c/progra~1/mib055~1/2022/community/vc/tools/msvc/14.44.35207/bin/hostx64/x64/cl.exe)
* C++ Compiler:   Version 19.44.35219 (at /cygdrive/c/progra~1/mib055~1/2022/community/vc/tools/msvc/14.44.35207/bin/hostx64/x64/cl.exe)

Build performance summary:
* Build jobs:     12
* Memory limit:   65402 MB
* 
  ```
## Build the OpenJDK from the downloaded sources

### Build:
  ```
$ make 
  ```
### Build and run some tests:
  ```
$ make run-test-tier1
  ```
### The generated version will be in the Build directory:
  ```
$ ~/jdk/build/windows-x86_64-server-release/jdk
  ```

Check the newly created OpenJDK as follow:
  ```
$ ./build/windows-x86_64-server-release/jdk/bin/java -version
openjdk version "26-internal" 2026-03-17
OpenJDK Runtime Environment (build 26-internal-adhoc.info.jdk)
OpenJDK 64-Bit Server VM (build 26-internal-adhoc.info.jdk, mixed mode)
  ```

## The binary version of JDK26 is stored in [build](./build/) directory.



