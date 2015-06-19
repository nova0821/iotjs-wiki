### Overall steps to build for NuttX
1. Get the sources
2. Configure NuttX
3. Build libuv, JerryScript and IoT.js
4. Copy libraries to nuttx/nuttx/lib folder
5. Build NuttX

#### Problems working with NuttX
Please acknowledge that we are not experts on NuttX and may have trouble to resolve each problem you may be faced. For general NuttX issues, please read documents at [NuttX Home page](http://nuttx.org/). [NuttX forum](https://groups.yahoo.com/neo/groups/nuttx/info) also would be helpful.

#### Build Host
We recommend Ubuntu 14.04. Other platforms can be used but not verified by us.

#### Target board
Our work and this document describes [STM32F4-discovery with BB](http://www.st.com/web/en/catalog/tools/FM116/SC959/SS1532/LN1199/PF255417) as reference target. 

##### Relation with STM board?
We do not have any business relation with STM board. It is selected because it has enough RAM and Flash ROM so that development can be more comfortable. And it have lots of pins to play with. 

When IoT.js is built up and optimized, it may work in devices having smaller resource.


#### Toolchain 

As for STM32F4-discovery uses ARM, we recommend gcc-arm-none-eabi version 4.8. Refer [this](https://pixhawk.org/dev/toolchain_installation_lin) page how to install if you do not have installed yet.

#### Packages 

You may need to install below packages as follows;
```
sudo apt-get install autoconf libtool gperf flex bison
sudo apt-get install libusb-1.0-0-dev
sudo apt-get install libsgutils2-dev
```

#### kconfig frontend

To use menuconfig in NuttX, you may need to install kconfig frontend.

```
git clone https://github.com/jameswalmsley/kconfig-frontends.git
cd kconfig-frontends
./bootstrap
./configure
make
sudo make install
sudo ldconfig
```


### 1. Get the sources

If you haven't read [Build for Linux](https://github.com/Samsung/iotjs/wiki/Build-for-Linux) page, it would be better to read it. Some explanations may be skipped in this document.


#### Directory structure

Assume _harmony_ as a root folder so it may look like this;
* harmony
 * iotjs
 * nuttx

```
mkdir harmony; cd harmony
git clone https://github.com/Samsung/iotjs.git
git clone http://git.code.sf.net/p/nuttx/git nuttx
```

#### Apply patch to NuttX for IoT.js

Download [iotjs-nuttx-20150526.tar.gz](https://github.com/Samsung/iotjs/blob/wikiattach/iotjs-nuttx-20150526.tar.gz?raw=true) file to harmony folder.

```
cd harmony
# assume you already copied to this folder
tar xvf iotjs-nuttx-20150526.tar.gz
cd nuttx
git checkout -b iotjs 2eba8afab5e8bdc32a0f6365de070eaa7f383149
patch -p1 < ../iotjs-nuttx-20150526.diff
```


##### What is it about the _patch_ in above?

This _patch_ includes settings for IoT.js on NuttX with STM32F4-discovery and BB. It's one of our reference target board that we are working on to make development easier. 
Some of the settings are;
* added libuv, libjerry, iotjs in configuration
* enabled rcS file in /etc/init.d so that we can use micro SD
* enabled Network, UART6 for serial debug message
* filter too many debug message for network

The patch include some fixes that occurred when working with current version of IoT.js, some of the fixes are;
* fix nxflat that had some problem when reading micro SD card
* fix net accept() error return
* fix syscall CSV file for generating proxy source codes


### 2. Configure NuttX
 
```
# assume you are in nuttx root folder
cd nuttx/tools
./configure.sh stm32f4discovery/iotjs
cd ..
```

You may need to change your IP and MAC address.

```
# assume you are in nuttx folder where .config resides
make menuconfig
```

Select items as follows and change to your address
* Application Configuration > NSH Library > Networking Configuration > IP Address Configuration
* Application Configuration > NSH Library > Networking Configuration > Fixed MAC address 

> How to set MAC address for development?
> There are _locally administered addresses_ in MAC address.
> By googling "free mac address for development", you may find what to do.


### 3. Build IoT.js with libuv and JerryScript

As noted in [Build for Linux](https://github.com/Samsung/iotjs/wiki/Build-for-Linux) page, you need to give additional options for NuttX.

```
--target-arch=arm 
--target-os=nuttx 
--nuttx-home=(full path of nuttx home where .config file exist)
--buildlib
```

To build IoT.js for nuttx, first, you need to build NuttX to create configuration file 'config.h'.

```
cd harmony/nuttx/nuttx
make
```

It will show errors that _libuv.a cannot be found_. It is ok for now. If you just want to try nuttx only before proceeding, please turn off three options in ".config" file.

```
CONFIG_SYSTEM_IOTJS=n
CONFIG_LIBUV=n
CONFIG_LIBJERRY=n
```

And back to building IoT.js.
If you have harmony in /home/maxwell/harmony, for example;

```
cd harmony/iotjs
./tools/build.py --buildtype=release --target-arch=arm --target-os=nuttx \
--nuttx-home=/home/maxwell/harmony/nuttx/nuttx --buildlib
```

### 4. Copy libraries to nuttx/nuttx/lib folder

For the moment, lib files need to be copied manually.

```
cp build/arm-nuttx/release/libs/libjerrycore.a ../nuttx/nuttx/lib/libjerry.a
cp build/arm-nuttx/release/libs/libuv.a ../nuttx/nuttx/lib
cp build/arm-nuttx/release/iotjs/liblibiotjs.a ../nuttx/nuttx/lib/libiotjs.a
```


### 5. Build NuttX

Enter nuttx and configure with _make menuconfig_ with your taste
```
make menuconfig
```
If all things are ready to go, build.
```
make
```

With successful compilation, you'll get _nuttx_ and _nuttx.bin_ files.

#### Prepare flashing to target board

Flashing to STM32F4-discovery board needs another tool called _stlink_. You can download it at [here](https://github.com/texane/stlink), follow below steps;

```
cd harmony
git clone https://github.com/texane/stlink.git
cd stlink

./autogen.sh
./configure
make
```

Relative path is used when executing _stlink_ tools. You may have to change them when they are not cloned in harmony folder.


#### Flash

```
# Assume you are in nuttx/nuttx folder where nuttx.bin file exists.
../../stlink/st-flash write nuttx.bin 0x8000000
```
With successful flashing you'll get something at the bottom like;
```
INFO src/stlink-common.c: Starting verification of write complete
INFO src/stlink-common.c: Flash written and verified! jolly good!
```


### Running IoT.js

You can connect STM32F4-discovery board by 1) USB as ttyACM0, or 2) telnet if telnet daemon is running. We use [minicom](https://help.ubuntu.com/community/Minicom) for USB ttyACM0.

```
minicom --device=/dev/ttyACM0
```
You may need to enable _Add Carriage Return_ option. Press Ctrl-A + Z + U for short in minicom screen.

Press _Enter_ key several times to trigger NuttShell to start.

If micro SD is enable, you can copy any script file to it and run with _nsh_, for example;
```
NuttShell (NSH)
nsh> iotjs /mnt/sdcard/test.js
```

If you see
```
+-----------------------------+                  
|                             |                  
|  Cannot open /dev/ttyACM0!  |                  
|                             |                  
+-----------------------------+ 
```
and it stays on the screen, something is wrong. Blue LED may blink if NuttX is in abnormal state. Press black(reset) button on the board and try again. If you still see this warning message, begin with original NuttX code and check your board, USB line and other softwares.


### 6. Latest status

Current IoT.jsm, as of June 2015, requires more memory than STM32F4-disco provides. We need memory optimisation. Until some result with this, I'll start with 256K [FRDM-K64F](https://developer.mbed.org/platforms/FRDM-K64F/) board.
