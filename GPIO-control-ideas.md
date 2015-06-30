### What is this page ?
RAW idea as is with GPIO control

#### 1, primitive GPIO control

Setting the pins
* depends on the board which is used by some application 
   * able to control in unit of PINs
   * set mode of pins: digital output, digital input, analog input
   * pull up/down: float, pull down, pull up
* pinmode(pin,callback);
   * pin: number value of pin with port with the mode
   * callback(err): callback function to receive result

Reading
* read the pin and return value
* read(pin,callback);
   * pin: number value of pin with port
   * callback(err,value): callback function to receive value result
      * value may be 0 or 1

Writing
* write the pin with a value
* write(pin, value, callback);
   * pin: number value of pin with port with the mode
   * value: write value, may be 0 or 1
   * callback(err): callback function to receive result

Reference
* [STM32F4 Discovery Tutorials – GPIO](http://armprogramming.com/stm32f4-discovery-tutorials-gpio/)
* [Understanding Microcontroller Pin Input/Output Modes ->](http://coactionos.com/embedded%20design%20tips/2013/10/21/Tips-Understanding-Microcontroller-Pin-Input-Output-Modes/)



#### 2, implementation
* Need to know platform is IoT.js?
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

     
#### 3, testing with push button and LED
* ...


