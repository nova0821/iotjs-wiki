### Overall steps to build for NuttX
1. Get the sources
2. Configure NuttX
3. Build libuv, jerryscript and iotjs
4. Copy libraries to nuttx/nuttx/lib folder
5. Build NuttX

### Problems working with NuttX
Please acknowledge that we are also not experts on NuttX and may have trouble understanding each problems. For general NuttX issue please read documents at [NuttX Home page](http://nuttx.org/). Visiting and asking to [NuttX forum](https://groups.yahoo.com/neo/groups/nuttx/info) also can be a help.

### Build Host
We recommend Ubuntu 14.04. Other platforms can be used but not verified by us.

#### Toolchain 
We recommend gcc-arm-none-eabi version 4.8. Refer to [this](https://pixhawk.org/dev/toolchain_installation_lin) page how to install if you do not have installed yet.

#### Packages 
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
git clone https://github.com/Samsung/iotjs.git iotjs
git clone http://git.code.sf.net/p/nuttx/git nuttx
```

#### Apply patch to NuttX for IoT.js
Download [this](???) file to harmony folder and extract it
```
cd harmony
wget ???
cd nuttx
git checkout -b iotjs 2eba8afab5e8bdc32a0f6365de070eaa7f383149
git patch -p1 < ../iotjs-nuttx-20150421.patch
```

##### What is it about the patch?
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

##### STM32F4-discovery with BB ?
Please refer [this](http://www.st.com/web/en/catalog/tools/FM116/SC959/SS1532/LN1199/PF255417) page.

##### Relation with STM board?
We do not have any business relation with STM board. It is selected cause it has enough RAM and Flash ROM and have lots of pins to play with. (Our company is big so others in our company may have, but IoT.js related developers have no relation)

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
> just google "free mac address for development" and you may know what to do.

### 3. Build libuv, jerryscript and iotjs
### 4. Copy libraries to nuttx/nuttx/lib folder
### 5. Build NuttX

Enter nuttx and configure with _make menuconfig_ with your taste
```
make menuconfig
```
If all things are ready to go, build.
```
make
```

With successful compilation, you'll get nuttx and nuttx.bin files.

#### Prepare flashing to target board

Flashing to STM32F4 board needs another tool called _stlink_. You can download it from [here](https://github.com/texane/stlink)

```
cd harmony
git clone https://github.com/texane/stlink.git
cd stlink

./autogen.sh
./configure
make
```

#### Flash

Assume you are in nuttx/nuttx folder where nuttx.bin file exist.
```
../../stlink/st-flash write nuttx.bin 0x8000000
```
With successful flashing you'll get something like
```
INFO src/stlink-common.c: Starting verification of write complete
INFO src/stlink-common.c: Flash written and verified! jolly good!
```




