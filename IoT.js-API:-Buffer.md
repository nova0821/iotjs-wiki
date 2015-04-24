IoT.js provides Buffer to compensate the lack of pure Javascript's capability of manipulating binary data, Javascript string is only suitable for Unicode string. Buffer allow you handling sequence of binary data in Javascript world.

## Class: Buffer
Buffer class is a global type. you can create a buffer object in several way.
### Constructor
* new Buffer(size)
* new Buffer(buffer)
* new Buffer(str[,encoding])

### Class Methods
* Buffer.byteLength(string[,encoding])
* Buffer.isBuffer(obj)

## Instance of Buffer
Once you get buffer object in some way, you can handle the buffer using the following API:

### Properties
buf.length

### Methods
buf.write(string[,offset[,length]][,encoding])
buf.toString([encoding][,start][,end])
buf.copy(targetBuffer[,targetStart][,sourceStart[,sourceEnd]])