#### About

This page describes short version to use with latest version of NuttX for STM32F4-Discovery with BB.

Please read [Build for NuttX](https://github.com/Samsung/iotjs/wiki/Build-for-NuttX) page and understand full procedure.

#### Get NuttX for IoT.js

Follow [Building nuttx for iotjs](https://bitbucket.org/seanshpark/nuttx/wiki/Home) page

#### Build IoT.js for NuttX

Giving these options are needed
```
--target-arch=arm
--target-os=nuttx
--nuttx-home=(where .config file exist)
--target-board=stm32f4disco
--tuv
```

for example,
```
./tools/build.py \
--target-arch=arm --target-os=nuttx --nuttx-home=/home/user/harmony/nuttx/nuttx \
--target-board=stm32f4disco --jerry-heaplimit=78 \
--tuv
--buildtype=release
```

#### NuttX build and flashing

in nuttx
```
make
sudo ../../stlink/st-flash write nuttx.bin 0x8000000
```

#### ETC
##### Testing network on NuttX

* ping to subnet gateway
* ping to other subnet gateway
* tuvtester (local loopback send/receive)
* nettest with client mode
* nettest with server mode 