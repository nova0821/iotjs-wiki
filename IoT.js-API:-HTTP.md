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
After request header is parsed, this event will be fired. 
* `request: http.IncomingMessage` instance. 
* `response: http.ServerResponse` instance.

## Class: http.ClientRequest
### Event
#### 'end'
This event triggered when no more data to be received remains from client request.

## Class: http.ServerResponse
### Event
#### 'end'
This event triggered when no more data to be received remains from server response.

## Class: http.IncomingMessage
### Event
