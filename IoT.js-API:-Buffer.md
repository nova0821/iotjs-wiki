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

## Properties of Buffer instance
* buf.length

## Methods of Buffer instance
* buf.write(string[,offset[,length]][,encoding])
* buf.toString([encoding][,start][,end])
* buf.copy(targetBuffer[,targetStart][,sourceStart[,sourceEnd]]) 