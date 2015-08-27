# Inside IoT.js

* [Design](#design)
* [Javascript Binding](#javascript-binding)
* [libuv Binding](#libuv-binding)
* [IoT.js Core](#iotjscoe)

***

## Design

IoT.js is built on top of [JerryScript](http://samsung.github.io/jerryscript) and [libuv](http://libuv.org). JerryScript is a lightweight Javascript engine intended to run on small devices for IoT and libuv is a library for supporting asynchronous I/O. 

A big picture of IoT.js is looks like following figure.
 
![Layout of IoT.js](https://github.com/Samsung/iotjs/blob/wikiattach/doc/InsideIoTjs/IoTjs_big_layout.jpg)

The layer related to IoT.js project is green colored box on above figure.

As you can see, it runs upon JerryScript  and libuv.
There is a layer that binds JerryScript and libuv to IoT.js.
We will discuss about that layer in [Javascript Binding](#javascript-binding) and [libuv Binding](#javascript-binding) section on this document respectively.

IoT.js core layer locates above these binding layer.
This core layer play a central role in this project that it provides API implementation layer with fundamental functionality for running main event loop, interacting with Javascript engine, managing I/O resources via libuv, managing life cycle of objects, supplies builtin modules, an so forth.
We will discuss this topic further in [IoT.js Core](#iotjs-core) section.

IoT.js provides APIs for user applications to help creating IoT friendly services more easily.
You can see the list of API from [IoT.js API Reference](https://github.com/Samsung/iotjs/wiki/IoT.js%20API%20Reference).

***

## Javascript Binding

Many modern Javascript Engines are supporting embedding API to provide functionality for compiling and executing Javascript program, accessing Javascript object and its value, handling errors, managing lifecyles of objects and so on. 

Javascript Binding layer of IoT.js is for providing interface between upper layer (IoT.js core) and  underlying Javascript engine.
Although IoT.js only supports JerryScript for now, there is a chance that we extend supporting Javascript engine (such as [Duktape](http://duktape.org/) or [V8](https://code.google.com/p/v8/)) in the future.
For this reason, we want to keep the interface of Javascript binding layer independent from a specific Javascript engine.
You can see the interface of the layer in [iotjs_binding.h](https://github.com/Samsung/iotjs/blob/master/src/iotjs_binding.h).

### JObject

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

### JObjectWrap

`JObjectWrap` is used for wrapping a Javascript object to a C++ instance.
The main purpose of this wrapper is to hand object's life cycle managing over to Javascript engine while linking the object with other data structure.
To create a instance of `JObjectWrap`, you need to supply a Javascript object and free handler.

To make sure the Javascript object could be reclaimed by GC when there are no more references to that object, this wrapper will not increase reference count for the Javascript object.
Free handler will be invoked just before the Javascript object actually being reclaimed by GC and it will free the wrapper instance.

Make sure that wrapper should not be a local variable for it could lead double free of wrapper instance. If you really want to use local wrapper just using `JObject` would be enough.

### Native handler

Some operations - such as file I/O, networking, device control, multitasking, and etc - can not be performed by pure Javascript.
IoT.js uses a mechanism called "native handler" to perform such operations via Javascript.
You can regard native handler as Javascript function implemented in C/C++.

You might think it's a little similar concept to [FFI](https://en.wikipedia.org/wiki/Foreign_function_interface).
In a wide sense it's true for native handler is for calling C/C++ function from Javascript but in a narrow sense it's not true.

Usually main purpose of [FFI](https://en.wikipedia.org/wiki/Foreign_function_interface) is to call a routine written in one language from a program written in another.
After a routine was invoked, it is common that the routine just do what it is supposed to do without knowing the context except arguments.
Whereas native handler does know that it is being called from Javascript (actually it is a Javascript function although not written in Javascript) and does access surrounding Javascript execution context.

### Embedding API supporting from Javascript engine

Many Javascript engines these days provide embedding API for this purpose. IoT.js uses the API to create [builtin module](#builtin) and [native handler](#native-handler). See following link if you want further information about the API:
 * [JerryScript API](https://samsung.github.io/jerryscript/API/)
 * [Duktape API](http://duktape.org/api.html)
 * [V8 embedder's guide](https://developers.google.com/v8/embed)
 * [SpiderMonkey API](https://developer.mozilla.org/en-US/docs/Mozilla/Projects/SpiderMonkey/JSAPI_reference)

***

## libuv Binding

IoT.js is using libuv to perform various asynchronous I/O and threading.
Because IoT.js adopt asynchronous programming model, libuv plays very important role in this project. Actually the [main loop](#event-loop) of IoT.js is libuv event loop that waits until an event occurs, picks the event, and dispatches the event through corresponding callback function.
You may read [libuv design document](http://docs.libuv.org/en/v1.x/design.html) to get detailed information about asynchronous programming model based on libuv.

### HandleWrap

IoT.js is wrapping libuv handle (e.g. file descriptor) using `HandleWrap` class. Here "handle" stands for "libuv request handle".
Because every libuv I/O handle (e.g. file descriptor) in IoT.js links to a Javascript object that correspond with the handle, `HandleWrap` inherits [`JObjectWrap`](#jobjectwrap).

### ReqWrap

`ReqWrap` if for wrapping libuv request (e.g. read file).
Because every libuv I/O request in IoT.js links to a Javascript function that treats result of the request, `ReqWrap` manages the lifecycle of the callback function object and has member function called `jcallback()` to retrieve the function object.

Note that `ReqWrap` does not inherits [`HandleWrap`](#handlewrap) to wrapping the callback function object.
This is because it need to prevent the callback function from being reclaimed by GC until finish handling the result.
As `HandleWrap` just hand over the managing lifecycle to Javascript engine without increasing reference count, we could not guarantee liveness of the callback function object if we use `HandleWrap`.

On the other hand, `ReqWrap` manages the reference count for callback function by itself - increasing reference count for the callback function when it is being created and decreasing when it is being freed
guaranteeing the liveness of callback function during request processing.
Also the function will be collected by GC when it need to be.

***

## IoT.js Core

### Life cycle of IoT.js

_Note:_
_We are currently focusing on implementing IoT.js upon JerryScript engine._
_The manner of implementing initialization is depends on JerryScript API._
_This could be changed when we adopt other Javascript engines._
_This chapter will explain initialization process based on current implementation._

The process of IoT.js can be summarized as follow:

1. Initialize JerryScript engine.
2. Execute empty script
 * This will create initial Javascript context.
3. Initialize builtin modules. 
 * This will create builin modules including ['process'](https://github.com/Samsung/iotjs/wiki/IoT.js-API:-Process).
4. Evaluate ['iotjs.js'](https://github.com/Samsung/iotjs/blob/master/src/js/iotjs.js).
 * This will generate entry function.
5. Run the entry function passing 'process'.
 1. Initialize 'process' module.
 2. Load user application script.
 3. Run the user application.
6. Run [event loop](#event-loop) until there are no more events to be handled.
7. Clean up.

### Builtin

Javascript object fully implemented in C/C++ using [embedding API](#embedding-api-supporting-from-javascript-engine) are called "builtin".
You can find list of builtin object at `MAP_MODULE_LIST` macro in ['iotjs_module.h'](https://github.com/Samsung/iotjs/blob/master/src/iotjs_module.h).

Builtin modules are very useful since it can accesss underlying system using libuv, C/C++ library, and system call. And it may be used for optimizing performance of CPU bound routine and reduce binary size.

Builtin modules are initialized during [intializing step of IoT.js](#life-cycle-of-iotjs) and released just before the process terminates.

### Native module

The [basic modules and extended modules](https://github.com/Samsung/iotjs/wiki/IoT.js-API-Reference) provides by IoT.js are called 'native module' because that modules will be included IoT.js native binary. 
There is a [tool](https://github.com/Samsung/iotjs/blob/master/tools/js2c.pl) that transfer Javascript script source file into C++ header file.

Usually native modules need help from [builtin](#builtin) modules which are implemented in C/C++ thus able to access underlying system.

Some native modules are bound to global object while others are on demand.
On demand modules will be created at the moment when it is first required and will not released until the program terminates.

### Event loop