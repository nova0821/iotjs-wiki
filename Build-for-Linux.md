### Overall steps to build for Linux
1. Get the sources
2. Set build options
3. Build all at once


***


#### Build Host
Ubuntu 14.04 is recommended. Any other Unix like platforms can be used. If you are trying other platforms and it doesn't seem to work properly, please look into [Issues](https://github.com/Samsung/iotjs/issues). Someone may have already tried. If you can't find any related one, please leave an issue for help.

#### Directory structure

This document assumes 'harmony' as the root directory. JerryScript and libuv are included as sub-modules in deps folder.

* harmony
    * iotjs
        * deps
            * jerry
            * libuv

※ harmony? It began from our project internal code name. (_Sounds good, isn't it? :)_)

#### Prerequisite

You need to install some packages to build IoT.js, follow as;

```
sudo apt-get install gyp cmake build-essential
```

gcc/g++ compiler at least version 4.8 is required to compile. If you have problem upgrading to 4.8, please google. One of that helped me is [how-to-install-gcc-4-8](http://askubuntu.com/questions/271388/how-to-install-gcc-4-8)


### 1. Get the sources

Clone from our repo to look around and test it. If it attracts you and want to try something interesting, please fork and send us requests.

To get the source for this repo, 
```
cd harmony
git clone https://github.com/Samsung/iotjs.git
cd iotjs
```

Sub modules libuv and jerryscript source will be pulled and matching hash will be checked out for your current IoT.js version when you run the build script.


### 2. Set build options

Some basic options are provided.

Existing build options are listed as follows;
```
buildtype=release|debug (release is default)
builddir=build (build is default)
buildlib (default is false)
target-arch=x86_64|i686|arm (depends on your host platform)
target-os=linux|nuttx (linux is default)
make-flags=-j9 (options to send to make)
nuttx-home= (no default value)
```

options that may need explanations
* builddir: compile intermediate and output files are generated here. 
* buildlib: generating iotjs to a library if true such as for NuttX. It doesn't need value, just --buildlib will do it.
* nuttx-home: it's NuttX platform specific, to tell where the NuttX configuration and header files are.

To give the option, please use two dashes '--' before the option name as described in next section.


### 3. Build all at once

IoT.js and required submodules are generated all at once with build.py in tools folder.

```
cd iotjs
./tools/build.py
```

#### Options example

It's a good practice to build in separate folder, like 'build'. IoT.js generates all outputs into separate **'build'** folder. You can change this by --builddir option. Usually you won't need to use this option. Target and architecture name is used as a name for a folder inside 'build' folder.

To build debug version and results to 'output' folder
```
./tools/build.py --buildtype=debug --builddir=output
```

If you want to build 32bit version in x86_64 and debug ony a library,
```
./tools/build.py --target-arch=i686 --buildtype=debug --buildlib
```

#### Build only iotjs with given build option

If you had some modification and build only IoT.js this explains how. IoT.js uses [CMake](http://www.cmake.org/) for makefile generation. You can go inside the build folder and just build with 'make' command. Go inside where your target platform name, for example x86_64 linux,
```
cd build/x86_64-linux/iotjs
make
```

#### How to execute?

Executable name is **'iotjs'** and resides in (target-arch)-(target-os)/iotjs. To run greetings JavaScript in test folder for example,

```
./build/x86_64-linux/iotjs/iotjs ./test/hello_iot.js
```

#### What build script does

1. It will clone submodules jerryscript and libuv, this is done only once when version hash has not changed.
2. Checkout matching version for each submodules.
3. Build submodules, you can see the outputs at build/(target-arch)-(target-os)/libs folder.
4. Build iotjs


#### How to clean

Just remove the folder like
```
rm -rf build
```
or it you want to clean for rebuild one submodule, for example libuv
```
rm -rf build/x86_64-linux/deps/libuv
```

