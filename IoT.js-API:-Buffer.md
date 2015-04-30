IoT.js provides Buffer to compensate the lack of pure Javascript's capability of manipulating binary data, Javascript string is only suitable for Unicode string. Buffer allow you handling sequence of binary data in Javascript world.

## Class: Buffer
Buffer class is a global type. you can create a buffer object in several way.

### Constructor

#### new Buffer(size)
* `size: Number`

Allocate a new buffer of `size` bytes.

#### new Buffer(buffer)
* `buffer: Buffer`

Allocate a new buffer copied from given `buffer`.

#### new Buffer(str[,encoding])
* `str: String`
* `encoding: String`, Default: `utf8`

Allocate a new buffer containing given `str`.

### Class Methods

#### Buffer.byteLength(string[,encoding])
* `string: String`
* `encoding: String`, Default: `utf8`
* Return: `Number`

Returns actual byte length of `string` when it is encoded in `encoding`.
Note that it may different from `String.prototype.length` since that returns number of characters in a string.

#### Buffer.concat(list[, length])
* `list: Array of Buffer`
* `length: Number`
* Return: `Buffer`

Returns a `Buffer` concatenating all the Buffers in the `list`.

#### Buffer.isBuffer(obj)
* `obj`: Object

Test if `obj` is a `Buffer`.

## Instance of Buffer
Once you get buffer object in some way, you can handle the buffer using the following API:

### Properties

#### buf.length
* `Number`

The capacity of buffer in bytes.
Note that the value of `length` is not necessarily the same to the size of contents.

### Methods

#### buf.write(string[,offset[,length]][,encoding])
* `string: String` - data to be written to buffer
* `offset: Number`, Default: `0` - start position of buffer for writing.
* `length: Number`, Default: `buffer.length - offset` - total length to be written.
* `encoding: String`, Default: `utf8`
* Return: `Number` - total number of bytes written.

Writes `string` to buffer using `encoding` starts at `offset`. Returns total number of bytes written to the buffer.

#### buf.toString([encoding][,start][,end])
* `encoding: String`, Default: `utf8`
* `start: Number`, Default: `0`
* `end: Number`, Default: `buffer.length`
* Return: `String`

Decodes and returns a string from buffer.

#### buf.copy(targetBuffer[,targetStart][,sourceStart[,sourceEnd]])
* `targetBuffer: Buffer`
* `targetStart: Number`, Default: `0`
* `sourceStart: Number`, Default: `0`
* `sourceEnd: Number`, Default: `buf.length`

Copies data from `buf[sourceStart..sourceEnd-1]` to `targetBuffer[targetStart..]`.