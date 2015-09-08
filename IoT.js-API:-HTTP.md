# Module: http

IoT.js provides HTTP to support HTTP server and client enabling users to receive/send HTTP request easily.

## Methods
### http.createServer(requestListener)
* `requestListener: Function`
* Return: `http.Server` instance


### http.request(options[, callback])
* `options: Object`
* `callback: Function`
* Return: `http.ClientRequest` instance

### http.get(options[, callback])
* `options: Object`
* `callback: Function`
* Return: `http.ClientRequest` instance

Same as http.request except that `http.get` automatically call `req.end()` at the end.


## Class: http.Server

### Event

#### 'request'
* `request: http.IncomingMessage` instance.
* `response: http.ServerResponse` instance.
After request header is parsed, this event will be fired.

### Method
#### setTimeout(ms, cb)

* `ms: Number`
* `cb: Function`

Register cb for 'timeout' event and set socket's timeout value to ms. This event will be triggered by the underlying socket's 'timeout' event.

If cb is not provided, the socket will be destroyed automatically after timeout.
If you provides cb, you should handle the socket's timeout.

Default timeout for server is 2 minites.

## Class: http.ClientRequest
### Event

#### 'response'
* `response: http.IncomingMessage` instance

After response header is parsed, this event will be fired.

### Method
#### setTimeout(ms, cb)

* `ms: Number`
* `cb: Function`

Register cb for 'timeout' event and set socket's timeout value to ms. This event will be triggered by the underlying socket's 'timeout' event.

If cb is not provided, the socket will be destroyed automatically after timeout.
If you provides cb, you should handle the socket's timeout.


## Class: http.ServerResponse
### Event
#### 'end'
Thit event is fired when no more data to be sent.

#### 'close'
When underlying connection is closed, 'close' event is emitted.

### Method
#### setTimeout(ms, cb)

* `ms: Number`
* `cb: Function`

Register cb for 'timeout' event and set socket's timeout value to ms. This event will be triggered by the underlying socket's 'timeout' event.



## Class: http.IncomingMessage
### Event
#### 'end'
Thit event is fired when no more data to be received.

#### 'close'
When underlying connection is closed, 'close' event is emitted.

### Method
#### setTimeout(ms, cb)

* `ms: Number`
* `cb: Function`

Register cb for 'timeout' event set socket's timeout value to ms. This event will be triggered by the underlying socket's 'timeout' event.
