It's not that different for ARM-Linux targets, it's almost same as [Build for Linux](https://github.com/Samsung/iotjs/wiki/Build-for-Linux) page.


### Prerequisite

Install arm linux cross compiler

```
sudo apt-get install gcc-arm-linux-gnueabihf g++-arm-linux-gnueabihf
```


### Raspberry Pi 2 build
Giving `target-arch` and `target-os` will do. Rest is up to cross compiler and make system.

```
./tools/build.py --buildtype=release --noinit-submodule \
--target-arch=arm --target-os=linux
```

### Running in Raspberry Pi 2

Output program will be `build/arm-linux/release/iotjs/iotjs` or `build/arm-linux/debug/iotjs/iotjs`.
Copy using your favorite tool or `scp` like below.

```
scp build/arm-linux/release/iotjs/iotjs pi@(your RPi2 IP):/home/pi/.
```

Open a shell and run with your test program.

```
ssh pi@(your RPi2 IP)
./iotjs (your test program)
```

### Building in Raspberry Pi 2 ?

Not yet. Maybe someone out there?



