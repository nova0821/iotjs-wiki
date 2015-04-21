### Overall steps to build for NuttX
1. Get the sources
2. Configure NuttX
3. Build IoT.js-libuv, JerryScript, IoT.js
4. Copy libraries to nuttx/nuttx/lib folder
5. Build NuttX

### Problems working with NuttX
Please acknowledge that we are also not experts on NuttX and may have trouble understanding each problems. For general NuttX issue please read documents at [NuttX Home page](http://nuttx.org/). Visiting and asking to [NuttX forum](https://groups.yahoo.com/neo/groups/nuttx/info) also can be a help.

### Build Host
We assume you work on Ubuntu 14.04.

#### Toolchain 
We recommand gcc-arm-none-eabi version 4.8. Refer to [this](https://pixhawk.org/dev/toolchain_installation_lin) page how to install if you do not have installed yet.

#### Prerequisite 
You may need these packages installed as like;
```
sudo apt-get install autoconf libtool gperf flex bison
sudo apt-get install libusb-1.0-0-dev
sudo apt-get install libsgutils2-dev
sudo apt-get install libsgutils2-dev
```

##### kconfig frontend
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

### Directory structure
Assume harmony as the root folder so it may look like this
* harmony
 * iotjs
 * nuttx

### 1. Get the sources

```
mkdir harmony; cd harmony
git clone https://github.com/Samsung/IoT.js.git iotjs
git clone http://git.code.sf.net/p/nuttx/git nuttx
```

### Apply patch to NuttX for IoT.js
Download [this](???) file to harmony folder and extract it
```
cd harmony
wget ???
cd nuttx
git checkout -b iotjs 2eba8afab5e8bdc32a0f6365de070eaa7f383149
git patch -p1 < ../iotjs-nuttx-20150421.patch
```

#### What is it about the patch?
This patch includes settings for IoT.js on NuttX with STM32F4-discovery with BB.
It's one of our reference target board that we are working on to make development easier. Some to list are;
* added libuv, libjerry, iotjs in configuration
* enabled rcS file in /etc/init.d so that we can use micro SD
* enabled Network, UART6 for serial debug message
* filter too many debug message for network

The patch include some fixes that occurred when working with current version of IoT.js, some to list are;
* fix nxflat that had some problem when reading micro SD card
* fix net accept() error return
* fix syscall CSV file for generating proxy source codes

### 2. Configure NuttX
 
```
(assume you are in nuttx root folder)
cd nuttx/tools
./configure.sh stm32f4discovery/iotjs
```

You may need to change your IP and MAC address. 
```
make menuconfig
```
Select items as follows and change to your address
* Application Configuration > NSH Library > Networking Configuration > IP Address Configuration
* Application Configuration > NSH Library > Networking Configuration > Fixed MAC address 


### 3. Build IoT.js-libuv, JerryScript, IoT.js
### 4. Copy libraries to nuttx/nuttx/lib folder
### 5. Build NuttX


