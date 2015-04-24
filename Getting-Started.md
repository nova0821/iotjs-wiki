### Overview
IoT.js is built based on JerryScript(lightweight JavaScript engine) and libuv for asynchronous I/O event handling.

#### Source repositories
* IoT.js: https://github.com/Samsung/iotjs.git
* JerryScript: https://github.com/Samsung/jerryscript.git
* libuv: https://github.com/Samsung/libuv-iotjs.git 

### Supported platforms 
Current supported platforms are **Linux and NuttX**

* [Build for Linux](https://github.com/Samsung/iotjs/wiki/Build-for-Linux): Ubuntu 14.04 is used as a base platform.
* [Build for NuttX](https://github.com/Samsung/iotjs/wiki/Build-for-NuttX): NuttX 7.9 2eba8afab5e8bdc32a0f6365de070eaa7f383149 (Feb 15, 2015) is used with iotjs specific patch.
* Planning OSX 10.10 

### Porting to other platforms
Porting to another platform can be easy or quite complicated job depending on the platform you are working. If you have tried both linux and nuttx, you can see that it is quite different. Below link will show you step by step as an example.

* Porting guide to Raspberian for [Raspberry Pi](https://www.raspberrypi.org/downloads/)