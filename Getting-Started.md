### Overview
IoT.js is built based on JerryScript(lightweight JavaScript engine) and libuv for asynchronous I/O event handling.

#### Source repositories
* IoT.js: https://github.com/Samsung/iotjs.git
* JerryScript: https://github.com/Samsung/jerryscript.git
* libuv: https://github.com/Samsung/libuv.git 

### Build script
There is a script to help you build IoT.js called "build.py" in source repository.

### Supported platforms 
Current supported platforms are **Linux and NuttX**

* [Build for Linux](Build-for-Linux): Ubuntu 14.04 is used as a base platform.
* [Build for NuttX](Build-for-NuttX): NuttX 7.9 (Feb 15, 2015)
* [Build for Nuttx (new)](https://github.com/Samsung/iotjs/wiki/Build-for-Nuttx-(new)): NuttX latest version
* Raspberry Pi 2
    * [Setting Raspberry Pi 2](https://github.com/Samsung/iotjs/wiki/Setting-Raspberry-Pi-2-for-IoT.js)
    * [Build for ARM Linux (RPi2)](https://github.com/Samsung/iotjs/wiki/Build-for-ARM-Linux-(RPi2))

##### Platforms to support
* OSX 10.10 as development host
* [Artik 1 =>](https://www.artik.io/hardware/artik-1) as target board

##### H/W boards
* Current supporting
    * STM32F4-Discovery + BB
    * Raspberry Pi 2
* Plan to support
    * Samsung Artik 1
    * STM32F429-Discovery
    * STM32F411-Nucleo
    * Intel Edison
    * (and your contributions including above plans)


### Supporting direct H/W control
We may need to control `things` directly from ECMAScript code. How can we make it possible? Let's first describe it at [GPIO-API-candidate](https://github.com/Samsung/iotjs/wiki/GPIO-API-candidate) page.

### IoT.js Package
IoT.js also uses NPM tool, node package manager, as for package development and sharing. Visit [IoT.js Package](https://github.com/Samsung/iotjs/wiki/IoT.js-Package) page for more information.

#### When something goes wrong
Please read [Logging IoT.js execution](Logging-IoT.js-execution) how to display and add log messages while developing.


### [IoT.js API Reference](IoT.js-API-Reference)