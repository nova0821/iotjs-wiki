### Overall steps to build for Linux
1. Get the sources
2. Build options
3. Build all at once

#### Build Host
Ubuntu 14.04 is recommended. Any other Unix like platforms can be used. If you are trying other platforms and don't seem to work properly, please look in side or add an issue in [Issues](https://github.com/Samsung/iotjs/issues), someone may have already tried. It you can't find any, please leave an issue so anyone can be a help.

#### Directory structure

This document assumes 'harmony' as the root directory. JerryScript and libuv are included in submodules in deps folder.

* harmony
    * iotjs
        * deps
            * jerry
            * libuv

##### harmony ?

It began from our project internal code name. Sounds good isn't it :)


#### Prerequisite

You need to install some packages to build IoT.js, follow as;

```
sudo apt-get install gyp cmake build-essential
```

gcc/g++ compiler version 4.8 is required to compile. If you have problem upgrading to 4.8, please google. One of  that helped me is [how-to-install-gcc-4-8](http://askubuntu.com/questions/271388/how-to-install-gcc-4-8)


### 1. Get the sources

Clone from our repo to look around and test it. If you get interested and want to try something interesting, please fork and lets work together.

To get the source for this repo, 
```
cd harmony
git clone https://github.com/Samsung/iotjs.git
cd iotjs
```

Sub modules libuv and jerryscript source will be pulled and matching hash will be checked out for your current IoT.js version when you run the build script.


### 2. Build options

Some basic options are provided.

Existing build options are listed as follows;
```
buildtype=release|debug (release is default)
builddir=build|(used provided folder name) (build is default)
buildlib (default is false)
target-arch=x86_64|i686|arm (x86_64 is default)
target-os=linux|nuttx (linux is default)
make-flags=-j9 (options to send to make)
nuttx-home= (this is for nuttx platform, no need for linux)
```

options that may need explanations
* buildlib: generating iotjs to a library if true such as for NuttX.
* nuttx-home: it's NuttX platform specific to tell where the configuration and header files are.

To give the option, please use two dashes '--' as in next section.

### 3. Build all at once

It's a good practice to build in separate folder, like 'build'. IoT.js generates all outputs into separate **'build'** folder. You can change this by --builddir option.

```
cd iotjs
./tools/build.py
```

To build debug version to output folder
```
./tools/build.py --buildtype=debug --builddir=output
```

If you want to build 32bit version and debug
```
./tools/build.py --target-arch=i686 --buildtype=debug --buildlib
```

If you want to modify iotjs source and just want to build with **'make'**,
```
cd build/x86-linux/iotjs
make
```
You may as well get inside jerry or libuv if you 


#### How to execute?

Executable name is **'iotjs'** and resides in (target-arch)-(target-os)/iotjs. To run greetings JavaScript in test folder for example,

```
./build/x86_64-linux/iotjs/iotjs ./test/hello_iot.js
```

#### What build script does

1. It will clone submodules jerryscript and libuv, this is done only once
2. Checkout matching version
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

