## Overview

build.py help you build IoT.js.

It locates in "./tools" directory of source tree.

It automatically creates a directory where build object and outputs will be generated, 
checks configurations, tidiness of source code, licenses, and more.
Also it downloads, updates and builds submodules.
And finally generate IoT.js binary.


## How to use

You can build IoT.js with default setting for your host machine with;
```
./tools/build.py
```
The command will generate runnable IoT.js binary in "./build/<arch-os>/debug/iotjs/iotjs".

You can also build release binary with;
```
./tools/build.py --buildtype=release
```

## Parameters
**NOTE: some parameters are not supported by current version of build.py**

* buildtype
* builddir
* buildlib
* target-arch
* target-os
* target-board
* cmake-options
* cflags
* ldflags
* jerry-cflags
* check-tidy
* check-test
* external-static-lib
* external-shared-lib
* external-include-dir