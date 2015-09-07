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

## Class: http.ClientRequest
