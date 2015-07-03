### Overview
IoT.js is built based on JerryScript(lightweight JavaScript engine) and libuv for asynchronous I/O event handling.

#### Source repositories
* IoT.js: https://github.com/Samsung/iotjs.git
* JerryScript: https://github.com/Samsung/jerryscript.git
* libuv: https://github.com/Samsung/libuv.git 

### Supported platforms 
Current supported platforms are **Linux and NuttX**

* [Build for Linux](Build-for-Linux): Ubuntu 14.04 is used as a base platform.
* [Build for NuttX](Build-for-NuttX): NuttX 7.9 (Feb 15, 2015) is used with iotjs specific patches.
* Planning OSX 10.10 

### Porting to other platforms
It depends on the platform you're working on whether it's easy or quite complicated to port to another platform. Below guide will show you an example of the steps.

* [Setting Raspberry Pi 2](https://github.com/Samsung/iotjs/wiki/Setting-Raspberry-Pi-2-for-IoT.js)
* [Porting to Raspberry Pi 2](https://github.com/Samsung/iotjs/wiki/Porting-to-Raspberry-Pi-2)

### Supporting direct H/W control
We may need to control `things` directly from ECMAScript code. How can we make it possible? Let's first describe it at [GPIO-control-ideas](https://github.com/Samsung/iotjs/wiki/GPIO-control-ideas) page.

### IoT.js Package
IoT.js also uses NPM tool, node package manager, as for package development and sharing. Visit [IoT.js Package](https://github.com/Samsung/iotjs/wiki/IoT.js-Package) page for more information.

#### When something goes wrong
Please read [Logging IoT.js execution](Logging-IoT.js-execution) how to display and add log messages while developing.


### [IoT.js API Reference](IoT.js-API-Reference)