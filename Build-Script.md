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

## Parameters Candidates
**NOTE: some parameters are not supported by current version of build.py**

--
#### `--buildtype`
* `release` | `debug`

Specify whether build output will be for 'debug' or 'release'.

--
#### `--builddir`

Specify a directory where build outputs will be generated.

If given path is not exist, build.py will create it.

--
#### `--clean`
With given this option, build.py will claer all the build directory before start new build.

--
#### `--buildlib`
With given this option, build.py will generate IoT.js output as a library.

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
#### `--compile-flag`
Specify C compiler flags for IoT.js.

If you have multiple cflags, supply it with multiple use of this option;
```
--compile-flag=<cflag1> --compile-flag=<cflag2>
```

--
#### `--link-flag`
Specify linker flags for IoT.js.

If you have multiple ldflags, supply it with multiple use of this option;
```
--link-flag=<ldflag1> --link-flag=<ldflag2>
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
#### `--jerry-compile-flag`
Specify C compiler flags for JerryScript.

If you have multiple cflags, supply it with multiple use of this option;
```
--jerry-compile-flag=<cflag1> --jerry-compile-flag=<cflag2>
```

--
#### `--jerry-link-flag`
Specify linker flags for JerryScript.

If you have multiple ldflags, supply it with multiple use of this option;
```
--jerry-link-flag=<ldflag1> --jerry-link-flag=<ldflag2>
```

--
#### `--jerry-heaplimit`
Specify object heap limit for JerryScript engine.

--
#### `--jerry-lto`
With given this option, JerryScript will be built with LTO.

--
#### `--no-init-submodule`
With given this option, submoduls will not initialized before start build.

--
#### `--no-check-tidy`
With given this option, tidy checking will not performed.

--
#### `--no-check-test`
With given this option, unit test checking will not performed.

--
#### `--config`
Specify build configuration file path.

`build.default.config` file is in the source tree for default setting.

If this option is not specified, `build.config` file will be applied. If the file is not exist, it will be copied from `build.default.config`.

Parameters specified by the config file is applied, and then the parameters given by command line overwrite over the settings.

If you need to apply the same set of parameters for each build, making your own config file and trigger build.py with the config file would be more convenient.