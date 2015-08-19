## Module: net

IoT.js provides asynchronous networking through Net module.

You can use this module with `require('net')` and create both servers and clients.

### Methods

#### net.createServer([options][, connectionListener])
* `options: Object`
* `connectionListener: Function(connection: net.Socket)`

Creates a TCP server according to `options`.

`connectionListener` is automatically registered as `connection` event listener.


#### net.connect(options[, connectListener])
#### net.connect(port[, host][, connectListener])
#### net.createConnection(options[, connectnListener])
#### net.createConnnection(port[, host][, connectListener])
* `options: Object`
* `port: Number`
* `host: String`, Default: `localhost`
* `connectListner: Function()`

Creates a `net.Socket` and connects to the supplied host.

It is equivalent to `new net.Socket()` followed by `socket.connect()`.

***

## class: net.Server

You can create `net.Server` instance with `net.createServer()`.

### Instance Methods

#### server.listen(port[, host][, backlog][, listenListener])
#### server.listen(options[, listenListener])

* `port: Number`
* `host: String`
* `backlog: Number`
* `listenListener: Function()`

Start listening and accepting connections on specified port and host.


#### server.close([closeListener])

* `closeListener: Function()`

Stop listening new arriving connection.

Server socket will finally close when all existing connections are closed, then emit 'close' event.

`closeListener` is registered as `close` event listener.

### Event

#### `'listening'`
Emittied when server has been started listening.

#### `'connection(socket)'`
* `socket: net.Socket`

Emitted when new connection is established.

#### `'close'`
Emitted when server closed.

#### `'error'`
Emitted when an error occurs.

***

## class: net.Socket

### Constructor

#### new net.Socket([options])

* `options: Object`

Creates a new socket object.

`options` is an object specifying following information:

* `allowHalfOpen: Boolean`

### Instance Methods

#### socket.connect(options[, connectListener])
#### socket.connect(port[, host][, connectListener])
* `options: Object`
* `port: Number`
* 'host: String`, Default: `'localhost'`

Opens the connection with supplied port and host.

`options` is an object specifying following information:
* `port: Number` - port connect to (required)
* `host: String` - host connect to (optional, default: `'127.0.0.1'`)

`connectionListner` is automatically registered as `connect` event listener which will be emitted when the connection is established.

#### socket.write(data[, callback])

* `data: String | Buffer`
* `callback: Funciton()`

Sends `data` on the socket.

`callback` function will be called after given data is flushed through the connection.

#### socket.end([data][, callback])

* `data: String | Buffer`
* `callback: Funciton()`

Half-closes the socket.

If `data` is given it is equivalent to `socket.write(data)` followed by `socket.end()`.

* `data: String | Buffer`
#### socket.destroy()
#### socket.pause()
#### socket.resume()
#### socket.setTimeout(timeout[, callback])
#### socket.setKeepAlive([enable][, initialDelay])

### Events

#### lookup
#### connect
#### data
#### drain
#### end
#### timeout
#### close
#### error

