This page describes how to make IoT.js compile for Raspberry Pi 2, RPi2 for short, latest version of Raspberry Pi at the time of writing.

### Related part in the build script.

In tools folder, look inside build.py. It looks complicated but quite simple if you look carefully. It has four parts. Parsing options, fetching submodules, building sub modules and then building IoT.js.

I'll skip most for now, just describe related parts. When build.py script own page is available, I'll add a link here. Codes and lines may not be exactly same. If you encounter any problem, please leave an issue in Issues menu.

#### Patching for RPi2

Add core type to available list.
 
```
@@ -183,7 +183,7 @@ def parse_args():
         elif opt == 'builddir':
             options[opt] = val
         elif opt == 'target-arch':
-            if val.lower() in ['x86_64', 'i686', 'arm']:
+            if val.lower() in ['x86_64', 'i686', 'arm', 'armv7l']:
                 options[opt] = val.lower()
         elif opt == 'target-os':
             if val.lower() in ['linux', 'darwin', 'nuttx']:
```

libuv needs it's own build environment
```
@@ -250,6 +250,8 @@ def build_libuv():
         # libuv is using gyp. run the system according to build target.
         if opt_target_arch() == 'arm' and opt_target_os() =='nuttx':
             check_run_cmd('./nuttx-configure', [opt_nuttx_home()])
+        elif opt_target_arch() == 'armv7l' and opt_target_os() =='linux':
+            check_run_cmd('./armlinux-configure')
         else:
             check_run_cmd('./gyp_uv.py', ['-f', 'make'])
```

and the new armlinux-configure file for libuv
```
#!/bin/bash

export AR=arm-linux-gnueabihf-ar
export CC=arm-linux-gnueabihf-gcc
export CXX=arm-linux-gnueabihf-g++
export LINK=arm-linux-gnueabihf-g++
export PLATFORM=linux

./gyp_uv.py -Dtarget_arch=arm -DOS=linux
```

need new CMake config for the core, **arm7l-linux.cmake** file in cmake/config folder

```
# Copyright 2015 Samsung Electronics Co., Ltd.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

include(CMakeForceCompiler)

set(CMAKE_SYSTEM_NAME Linux)
set(CMAKE_SYSTEM_PROCESSOR armv7l)

set(EXTERNAL_CMAKE_C_COMPILER arm-linux-gnueabihf-gcc)
set(EXTERNAL_CMAKE_CXX_COMPILER arm-linux-gnueabihf-g++)

CMAKE_FORCE_C_COMPILER(${EXTERNAL_CMAKE_C_COMPILER} GNU)
CMAKE_FORCE_CXX_COMPILER(${EXTERNAL_CMAKE_CXX_COMPILER} GNU)

set(FLAGS_COMMON -mcpu=cortex-a7
                 -mfloat-abi=hard
                 -mfpu=neon-vfpv4
                 -D__LINUX__)

foreach(FLAG ${FLAGS_COMMON})
  set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} ${FLAG}")
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${FLAG}")
endforeach()

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fpermissive")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fno-exceptions")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fno-rtti")

message(${CMAKE_CXX_FLAGS})
```

and what about JerryScript? at the time of this writing, JerryScript supports ARMv7l so no changes are needed.
