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
#### net.createConnection(options[, connectnListener])
* `options: Object`
* `connectListner: Function()`

Creates a `net.Socket` and connects to the supplied host.

`connectionListner` is automatically registered as `connect` event listener which will be emitted when the connection is established.


#### net.connect(port[, host][, connectListener])
#### net.createConnnection(port[, host][, connectListener])
* `port: Number`
* `host: String`, Default: `localhost`
* `connectListner: Function()`

Creates a `net.Socket` and connects to the `port` on `host`.

See `net.connect(options[, connectListener])`


## class: net.Server

You can create `net.Server` instance with `net.createServer()`.

### Instance Methods

#### server.listen(port[, host][, backlog][, listenListener])
#### server.listen(options[, listenListener])
#### server.close()

### Event

#### listening
#### connectoin
#### close
#### error

## class: net.Socket

### Constructor

#### new net.Socket([options])

### Instance Methods

#### socket.connect(port[, host][, connectListener])
#### socket.write(data[, callback])
#### socket.end([data])
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

