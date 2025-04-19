# Build OpenJDK Version 25 from Sources in Windows 11 without WSL

Here a detailed description about building the OpenJDK from sources.

Following prerequisites are have to be installed befor compiling the sources for Windowns Environment.

- 1)Here the [build description from OpenJDK](https://openjdk.org/groups/build/doc/building.html)

- 2)OpenJDK one of the latest versions must be installed locally. If the target version, what will be here compiled is the Version 25 then the installed Version of OpenJDK cant be earlier as 23, but for this existing a clear Error message bei generating the make files.

    [Download OpenJDK Version 24](https://jdk.java.net/24/)


- 3)The C++ Compiler well be needed from Microsoft, is included in the Comunity Edition from Microsoft Visual Studio.
[Visual Studio 2022 Community Edition](https://visualstudio.microsoft.com/de/downloads/)
Only the "The Desktop development with C++", the "out-of-support components" can be desabled.
[Here a Screen-Shot about the components that is needed.](screen-shots/visual-studio.jpg) 


- 4)Cygwin will be also needed with some additional Components. On the [Cygwin Homepage](https://cygwin.com/) download the [Cygwin Installer](https://cygwin.com/setup-x86_64.exe)
  Execute the folowing command to install additional components like: Make,Autoconf,Unzip and Zip.
  ```
  setup-x86_64.exe -q --packages=make,autoconf,unzip,zip
  ```
- 5)Git is also needed. Download and install from: [Git Download for Windows](https://git-scm.com/downloads/win)


- 6)Install the [English Language Pack for the USA in Windows](screen-shots/setting-windows2.png) this will be needed by the generation of the make file for the process.


- 7)Install JTReg (JTReg is similar to JUnit but is older) from the [OpenJDK JTReg builds](https://builds.shipilev.net/jtreg/)
  **Important**: use always the latest version of JTReg.


## Now it is possible to build the OpenJDK
The Build Process will be done under the Cygwin Environment.

  ```
  open a Cygwin Shell with Cygwin.bat
  # now we are in the home directory from the logged in user
  # download the latest JTReg
  wget https://builds.shipilev.net/jtreg/jtreg-7.5.1+1.zip
  # unzip 
  unzip jtreg-7.5.1+1.zip
  # clone OpenJDK from main development (Version 25 is now not released)
  git clone https://github.com/openjdk/jdk.git
  # cd in the directory: jdk 
  # run configure to generate the file: make 
  bash configure --with-boot-jdk=/cygdrive/c/bin2025/jdk-build/jdk-24 --with-jtreg=/home/info/jtreg/ 
  ```
The result is something similar:
  ```
====================================================
A new configuration has been successfully created in
/home/info/jdk/build/windows-x86_64-server-release
using configure arguments '--with-boot-jdk=/cygdrive/c/bin2025/jdk-build/jdk-24 --with-jtreg=/home/info/jtreg/'.

Configuration summary:
* Name:           windows-x86_64-server-release
* Debug level:    release
* HS debug level: product
* JVM variants:   server
* JVM features:   server: 'cds compiler1 compiler2 epsilongc g1gc jfr jni-check jvmci jvmti management parallelgc serialgc services shenandoahgc vm-structs zgc'
* OpenJDK target: OS: windows, CPU architecture: x86, address length: 64
* Version string: 25-internal-adhoc.info.jdk (25-internal)
* Source date:    1745062716 (2025-04-19T11:38:36Z)

Tools summary:
* Environment:    cygwin version 3.6.0-1.x86_64, 2025-03-18 17:01 UTC; windows version 10.0.26100.3775; prefix "/cygdrive"; root "C:\cygwin64"
* Boot JDK:       openjdk version "24" 2025-03-18 OpenJDK Runtime Environment (build 24+36-3646) OpenJDK 64-Bit Server VM (build 24+36-3646, mixed mode, sharing) (at /cygdrive/c/bin2025/jdk-build/jdk-24)
* Toolchain:      microsoft (Microsoft Visual Studio 2022)
* C Compiler:     Version 19.43.34808 (at /cygdrive/c/progra~1/mib055~1/2022/commun~1/vc/tools/msvc/1443~1.348/bin/hostx64/x64/cl.exe)
* C++ Compiler:   Version 19.43.34808 (at /cygdrive/c/progra~1/mib055~1/2022/commun~1/vc/tools/msvc/1443~1.348/bin/hostx64/x64/cl.exe)

Build performance summary:
* Build jobs:     12
* Memory limit:   65403 MB
  ```
## Build the OpenJDK from the downloaded sources
  ```
# build 
make 
# build and run some tests
make run-test-tier1
  ```
The generated version will be in the Build directory:
~/jdk/build/windows-x86_64-server-release/jdk

Check the newly created OpenJDK as follow:

