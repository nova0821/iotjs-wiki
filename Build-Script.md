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

--
#### `--buildtype`
* `release` | `debug`

Specify whether build output will be for 'debug' or 'release'.

--
#### `--builddir`
Specify a directory where build outputs will be generated.

--
#### `--buildlib`
#### `--no-buildlib`
Specify whether build output will be a library or not (executable).

--
#### `--target-arch`
* `arm` | `x86` | `i686` | `x86_64` | `x64`

Specify target architecture.

--
#### `--target-os`
* `linux` | `darwin` | `osx` | `nuttx`

Specify target OS.

--
#### `--target-board`
Specify target board.

--
#### `--cmake-param`
Specify CMake parameters for IoT.js.

"cmake" command for IoT.js will be executed with the given parameter applied.

If you have multiple parameters, supply it with multiple use of this option;
```
--cmake-param=<param1> --cmake-param=<param2>
```

--
#### `--cflag`
Specify C compiler flags for IoT.js.

If you have multiple cflags, supply it with multiple use of this option;
```
--cflag=<cflag1> --cflag=<cflag2>
```

--
#### `--ldflag`
Specify linker flags for IoT.js.

If you have multiple ldflags, supply it with multiple use of this option;
```
--ldflag=<ldflag1> --ldflag=<ldflag2>
```

--
#### `--external-include-dir`
Specify external include directory for IoT.js.

If you have multiple external include directoies, supply it with multiple use of this option;
```
--external-include-dir=<dir1> --external-include-dir=<dir2>
```

--
#### `--external-static-lib`
Specify external static library that will be liked with IoT.js statically.

If you have multiple such libraries, supply it with multiple use of this option;
```
--external-static-lib=<lib1> --external-static-lib=<lib2>
```

--
#### `--external-shared-lib`
Specify external shared library that will be liked with IoT.js dynamically.

If you have multiple such libraries, supply it with multiple use of this option;
```
--external-shared-lib=<lib1> --external-shared-lib=<lib2>
```

--
#### `--jerry-cmake-param`
Specify CMake parameters for JerryScript.

"cmake" command for JerryScript will be executed with the given parameter applied.

If you have multiple parameters, supply it with multiple use of this option;
```
--jerry-cmake-param=<param1> --jerry-cmake-param=<param2>
```

--
#### `--jerry-cflag`
Specify C compiler flags for JerryScript.

If you have multiple cflags, supply it with multiple use of this option;
```
--jerry-cflag=<cflag1> --jerry-cflag=<cflag2>
```

--
#### `--jerry-ldflag`
Specify linker flags for JerryScript.

If you have multiple ldflags, supply it with multiple use of this option;
```
--jerry-ldflag=<ldflag1> --jerry-ldflag=<ldflag2>
```

--
#### `--jerry-lto`
#### `--no-jerry-lto`
Specify whether JerryScript will be built with LTO or not.

--
#### `--check-tidy`
#### `--no-check-tidy`
Specify whether tidy checking will be carried out after build finished or not.

--
#### `--check-test`
#### `--no-check-test`
Specify whether unit test checking will be carried out after build finished or not.
