### Overview
IoT.js is built based on JerryScript(lightweight JavaScript engine) and libuv for asynchronous I/O event handling.

#### Source repositories
* IoT.js: https://github.com/Samsung/iotjs.git
* JerryScript: https://github.com/Samsung/jerryscript.git
* libuv: https://github.com/Samsung/libuv-iotjs.git 

### Supported platforms 
Current supported platforms are **Linux and NuttX**

* [Build for Linux](https://github.com/Samsung/iotjs/wiki/Build-for-Linux): Ubuntu 14.04 is used as a base platform.
* [Build for NuttX](https://github.com/Samsung/iotjs/wiki/Build-for-NuttX): NuttX 7.9 2eba8afab5e8bdc32a0f6365de070eaa7f383149 (Feb 15, 2015) is used with iotjs specific patches.
* Planning OSX 10.10 

### Porting to other platforms
It depends on the platform you're working on whether it's easy or quite complicated to port to another platform. Below guide will show you an example of the steps.

* Porting guide to Raspberian for [Raspberry Pi](https://www.raspberrypi.org/downloads/)

#### When something goes wrong
Please read [Logging IoT.js execution](https://github.com/Samsung/iotjs/wiki/Logging-IoT.js-execution) how to display and add log messages while developing.


### [IoT.js API Reference](https://github.com/Samsung/iotjs/wiki/IoT.js-API-Reference)