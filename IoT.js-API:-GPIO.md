## class: GPIO

### Methods

#### initialize(callback)
* `callback: Function(err)` 
* Return: undefined if callback is given or `err` value.

Initialises GPIO device driver. Result is `err` value, 0 or positive if success or negative if failed. IOTJS_GPIO_INUSE if initialise more than once. 

#### release()

Release GPIO device driver and frees used memory.

#### pinmode(portpin, callback)
* `portpin`: port or port with pin integer value 
* `callback: Function(err)`
* Return: undefined if callback is given or `err` value.

Sets `portpin` mode. Depends on H/W. Result is `err` value, 0 or positive if success or negative if failed.

#### write(portpin, val, callback) 
* `portpin`: port, pin address, integer value
* `val`: value to write, integer value
* `callback Function(err)`: 
* Return: undefined if callback is given or `err` value.

Write value `val` to portpin. Result is `err`, 0 or positive if success or negative if failed.

#### read(portpin, callback) 
* `portpin`: port pin address, integer value
* `callback Function(err, value)`
* Return: undefined if callback is given or `err`.

Read from `portpin` to `value`. Result is `err`, 0 or positive if success or negative if failed.


### H/W dependency

This primitive GPIO function is common to all hardware that supports GPIO. `portpin` value depend on H/W.