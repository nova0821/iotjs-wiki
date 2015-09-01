## class: GPIO

### `pins` and `ports`

* pin number is logical number starts from 1. Thus logical pin number *k* is not necessarily bound to physical pin number *k* in your board.
* port number is logical number starts from 1. Thus logical port number *k* is not necessarily bound to physical port number *k* in your board.
* 8 logical pin will be bound to a logical port. For example, pin number 1~8 will bound to port 1, pin number 9~16 bound to port 2, and so forth.
* If you write a byte value to a port, the result is the same as writing each bit to corresponding pin. For example, let's say you write (10101011)2 to port 1. the operation will write up bit to pin 1, up bit to pin 2, down bit to pin 3, ... , up bit to pin 8.

### Methods

#### initialize(callback)
* `callback: Function(err: Error | null)`

Initializes GPIO device.


Initialises GPIO device driver. 

#### release()

Release GPIO device driver and frees used memory.

#### gpio.setPin(pinNumber, direction[, mode][, callback])
* `pinNumber: Number`: pin number to configure
* `direction: 'in' | 'out' | 'none'`: direction of the pin. `'none'` will unset the Pin.
* `mode: 'pullup' | 'pulldn' | 'float' | 'pushpull' | 'opendrain' | 'none' | '' | undefined` : pin mode. 
* `callback: Function(err: Error | null)`.
  * if callback is not provided and error occurs, throws `Error` object

_TODO_ 
* describe `mode`

#### gpio.writePin(pinNumber, value[, callback])
* `pinNumber: Number` - pin number to wirte
* `value: Boolean`.
* `callback: Function(err: Error | null)`.
  * if callback is not provided and error occurs, throws `Error` object

Write a boolean value to a pin.

#### gpio.readPin(pinNumber, callback)
* `pinNumber: Number` - pin number to read.
* `callback: Function(err: Error | null, value: Boolean)`.

Read value from a pin.

#### gpio.setPort(portNumber, direction[, mode][, callback])
* `portNumber: Number` - port number to configure.
* `direction: 'in' | 'out' | 'none'` - direction of the port.
* `mode: String` - pin mode.
* `callback: Function(err: Error | null)`.
  * if callback is not provided and error occurs, throws `Error` object

Configure single port. All pins bound to this port will have the configuration. 


#### gpio.writePort(portNumber, value[, callback])
* `portNumber: Number` - port number to write
* `value: Number(1 Byte)`.
* `callback: Function(err: Error | null)`.
  * if callback is not provided and error occurs, throws `GpioError` object

Write a byte value to a port.

#### gpio.readPort(portNumber, callback)
* `portNumber: Number` - port number to read.
* `callback: Function(err: Error | null, value: Number(1 byte))`.

Read value from a port.


#### gpio.query(queryOption, callback)
* `queryOption: Object`.
* `callback: Function(err: Error | null, result: Object)`.
* _Need mode discussion for this_

### Error
* _GpioError_ object for Gpio Error may be better.

