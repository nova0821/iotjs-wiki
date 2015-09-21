### Getting Started with Examples
As **IoT.js** is asynchronous and event-driven, programming style is pretty much different from traditional blocking synchronous programming. This tutorial lets you know how to code with **IoT.js** mainly focused on asynchronous style.

#### Hello World
Firstly, create a javascript file (e.g. `hello.js`) and open it. Then type as following.
```javascript
console.log('Hello, world!');
```

You must be familiar with the code above if you have ever worked with Javascript in web. This is exactly same way as in major web browsers.

You can run it with:
```
$ ./iotjs hello.js
```

Then it gives:
```
Hello, world!
```

Pretty simple. But where did `console` come from? `console` is not defined in Global Object according to ECMAScript spec.

The answer is `console` is a builtin module so it should have been `require`ed. However, `console` is a special case so we can use it directly without `require`. This is about Module System which We will cover later.

#### File Reader
To read a file, we need to import *File System* module.
When importing a module, we use function `require`.
*File System* module is abbreviated as `fs`. You can import it like:
```javascript
var fs = require('fs');
```

Then we can use APIs of `fs`. To open a file, use `open()`.
```javascript
fs.readFile("hello_iotjs.txt",   // path
            readFileCallback);   // callback
```
Let's say we want to read `hello_iotjs.txt`. Just pass it as first argument.
It may be enough for synchronous style but we must specify a callback function as last argument. `fs.readFile` does not wait for I/O to be done, it just goes on to next code. Sometime after file opening is completely done, callback will be called. This means that we must not implement `readFile` handling code on the next line, but in callback function.

Take a look at the callback function for `fs.readFile` below.
```javascript
function readFileCallback(err, data) {
  if (err) throw err;
  console.log(data.toString());
}
```
We can find two arguments in this function. We can think of them as the results of `fs.open`. In this case(`fs.readFile`), `err` and `data` are given. Of course, each API function has their own argument list.

`err` is an `Error` object. We just throw it if an error has occurred. Otherwise we have successfully read the file content and it is stored in `data`. In this example, it only prints the file content but you can do anything you want.

##### full code list
```javascript
var fs = require('fs');

fs.readFile("hello_iotjs.txt",   // path
            readFileCallback);   // callback

function readFileCallback(err, data) {
  if (err) throw err;
  console.log(data.toString());
}
```

#### Echo Server
.

### Module System
