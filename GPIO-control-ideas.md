### What is this page ?
RAW idea as is with GPIO control

#### Step 1, primitive GPIO control
Setting the pins
* able to control in unit of PINs
* set mode of pins: digital output, digital input, analog input
* pull up/down: float, pull down, pull up
* [STM32F4 Discovery Tutorials – GPIO](http://armprogramming.com/stm32f4-discovery-tutorials-gpio/)
* [Understanding Microcontroller Pin Input/Output Modes ->](http://coactionos.com/embedded%20design%20tips/2013/10/21/Tips-Understanding-Microcontroller-Pin-Input-Output-Modes/) 

#### Step 2, Support multiple platforms with development boards
Naming GPIO pins for multiple platform
* Make Application code (which runs on top of IoT.js) that can run in different H/W pin configuration
* Configuration code or with data that can translate `Name` to `GPIO#`
* Detect Platform(OS and HW) so that Application don't have to be aware of

#### Step 3, Making standards
Predefine product group
* We can fix the platform without detection if product group can be defined
* Common I/O for products, such as `Generic Air-conditioner` can have ...
   * current temperature and humidity sensor input, 
   * temperature settings control input,
   * Power control output for fan
   * Power control output for compressor
   * and more
* How to extend to real product?

