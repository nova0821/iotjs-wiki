# Inside IoT.js

* [Design](#design)
* [Javascript Binding](#javascript-binding)
* [libuv Binding](#libuv-binding)
* [IoT.js Core](#IoT.js Core)

***

## Design

IoT.js is built on top of [JerryScript](http://samsung.github.io/jerryscript) and [libuv](http://libuv.org). JerryScript is a lightweight Javascript engine intended to run on small devices for IoT and libuv is a library for supporting asynchronous I/O. 

A big picture of IoT.js is looks like following figure.
 
![Layout of IoT.js](https://github.com/Samsung/iotjs/blob/wikiattach/doc/InsideIoTjs/IoTjs_big_layout.jpg)

The layer related to IoT.js project is green colored box on above figure.

As you can see, it runs upon JerryScript  and libuv. There is a layer that binds JerryScript and libuv to IoT.js. We will discuss about that layer in [Javascript Binding](#javascript-binding) and [libuv Binding](#javascript-binding) section on this document respectively.

IoT.js core layer locates above these binding layer. This core layer play a central role in this project that it provides API implementation layer with fundamental functionality for running main event loop, interacting with Javascript engine, managing I/O resources via libuv, managing life cycle of objects, supplies builtin modules, an so forth. We will discuss this topic further in [IoT.js Core](#iotjs-core) section.

IoT.js provides APIs for user applications to help creating IoT friendly services more easily. You can see the list of API from [IoT.js API Reference](https://github.com/Samsung/iotjs/wiki/IoT.js%20API%20Reference).

***

## Javascript Binding

Many modern Javascript Engines are supporting embedding API to provide functionality for compiling and executing Javascript program, accessing Javascript object and its value, handling errors, managing lifecyles of objects and so on. 

Javascript Binding layer of IoT.js is for providing interface between upper layer (IoT.js core) and  underlying Javascript engine. Although IoT.js only supports JerryScript for now, there is a chance that we extend supporting Javascript engine (such as [Duktape](http://duktape.org/) or [V8](https://code.google.com/p/v8/)) in the future. For this reason, we want to keep the interface of Javascript binding layer independent from a specific Javascript engine. You can see the interface of the layer in [iotjs_binding.h](https://github.com/Samsung/iotjs/blob/master/src/iotjs_binding.h).

### `JObject`

`JObject` class stands for a real Javascript object. Upper layer will access Javascript object via this interface. This class provides following functionalities:

* Creating a Javascript object using `Object()` constructor.
* Creating a Javascript object by a value.
* Creating a Javascript function object where its body is implemented in C/C++.
* Creating a Javascript Error object.
* Increasing reference count.
* Decreasing reference count.
* Checking object type.
* Retrieving value.
* Calling a Javascript function.
* Evaluating a Javascript script.


### Native handler

Some operations - such as file I/O, networking, device control, multitasking, and etc - can not be performed by pure Javascript. IoT.js uses a mechanism called "native handler" to perform such operations via Javascript. You can regard native handler as Javascript function implemented in C/C++.

You might think it's a little similar concept to FFI. In a wide sense it's true for native handler is for calling C/C++ function from Javascript but in a narrow sense it's not true.

Usually main purpose of FFI is to call a routine written in one language from a program written in another. After a routine was invoked, it is common that the routine just do what it suppose to do without knowing the context except arguments. Whereas native handler does know that it is being called from Javascript (actually it is a Javascript function although not written in Javascript) and does access surrounding Javascript execution context.

***

## libuv Binding

***

## IoT.js Core