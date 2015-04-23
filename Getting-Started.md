### Overview
IoT.js is built based on JerryScript(lightweight JavaScript engine) and libuv for asynchronous I/O event handling.

#### Source repositories
* IoT.js: https://github.com/Samsung/iotjs.git
* JerryScript: https://github.com/Samsung/jerryscript.git
* libuv: https://github.com/Samsung/libuv-iotjs.git 

### Supported platforms 
**Linux and NuttX**

* [Build for Linux](https://github.com/Samsung/iotjs/wiki/Build-for-Linux): Ubuntu 14.04 is used as a base platform.
* [Build for NuttX](https://github.com/Samsung/iotjs/wiki/Build-for-NuttX): NuttX 7.9 2eba8afab5e8bdc32a0f6365de070eaa7f383149 (Feb 15, 2015) is used with iotjs specific patch.

### Porting to other platforms
Porting to another platform can be easy to quite complicated job depending on the platform you are working on. If you have tried both linux and nuttx, it is quite different cause nuttx needs extra tasks for it is characteristics.
Below link will show an example not that hard but uses cross compilation.

* Porting guide to another platform