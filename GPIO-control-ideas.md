### What is this page ?
RAW idea as is with GPIO control

#### 1, primitive GPIO control
Setting the pins
* able to control in unit of PINs
* set mode of pins: digital output, digital input, analog input
* pull up/down: float, pull down, pull up
* [STM32F4 Discovery Tutorials – GPIO](http://armprogramming.com/stm32f4-discovery-tutorials-gpio/)
* [Understanding Microcontroller Pin Input/Output Modes ->](http://coactionos.com/embedded%20design%20tips/2013/10/21/Tips-Understanding-Microcontroller-Pin-Input-Output-Modes/)
* Multiple OS and H/W Board


#### 2, implementation
* Supporting real devices
   * as an example, visit [johnny-five](https://github.com/rwaldron/johnny-five) and see how it looks like
* Structure Components
   * Device: Sensors and Actuators attached to the Board
   * Board: Where SoC exist
   * Board dependent codes: C++ codes that depend on the board
   * IoT.js platform codes: C++/JS core codes of IoT.js
   * Board dependent application codes: code that depend on board and device
   * Application codes: 
* How should the API look like?
   * Class: to manage APIs in classes, in functional and usage: GPIO -> I2C -> ZWave
   * Methods
      * Initialize(): initialise the device
      * Read, Write, ...

     



