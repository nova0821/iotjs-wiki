## Class: fs


### Methods

#### fs.open(path, flags[, mode], callback)

* `path: String` - file path to be opened.
* `flags: String` - open flags.
* `mode: Number`, Default: `0666` - permission mode.
* `callback: Function(err, fd)`
 * `err: Error` - `Error` object if there was something wrong, otherwise `null`.
 * `fd: Number` - file descriptor.

#### fs.read(fd, buffer, offset, length, position, callback)

* `fd: Int` - file descriptor.
* `buffer: Buffer` - buffer that the data will be written to.
* `offset: Number` - offset of the buffer where to start writing.
* `length: Number` - number of bytes to read.
* `position: Number` - specifying where to start read data from the file, if `null`, read from current position.
* `callback: Function(err, bytesRead, buffer) `

#### fs.readFile(path[, options], callback)

* `path: String` - file path to be opened.
* `options: Object` - options for the operation.
 * `encoding: String`, Default: `null` - encoding of the file.
 * `flag: String`, Default: `r` - file open flag.
* `callback: Function(err, data)` - callback function.
