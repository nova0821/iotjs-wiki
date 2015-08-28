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

As you can see above, IoT.js runs upon JerryScript  and libuv.
There is a layer that binds JerryScript and libuv to IoT.js.
We will deals with the layer in [Javascript Binding](#javascript-binding) and [libuv Binding](#javascript-binding) section on this document respectively.

IoT.js core layer locates above these binding layer.
This core layer plays a central role in this project providing upper layer with fundamental functionality of running main event loop, interacting with Javascript engine, managing I/O resources via libuv, managing life cycle of objects, providing builtin modules, and so forth.
[IoT.js Core](#iotjs-core) section deals with the layer in detail.

IoT.js provides APIs for user applications to help creating IoT friendly services.
You can see the list of API from [IoT.js API Reference](https://github.com/Samsung/iotjs/wiki/IoT.js%20API%20Reference).

***

## Javascript Binding

Many modern Javascript Engines come with embedding API to provide functionality for compiling and executing Javascript program, accessing Javascript object and its value, handling errors, managing lifecyles of objects and so on. 

You can think of Javascript binding layer as an interface between upper layer (IoT.js core) and  underlying Javascript engine.
Although IoT.js only supports JerryScript for now, there will be a chance that we extend supporting Javascript engine (such as [Duktape](http://duktape.org/) or [V8](https://code.google.com/p/v8/)) in the future.
For this reason, we want to keep the layer independent from a specific Javascript engine.
You can see interface of the layer in [iotjs_binding.h](https://github.com/Samsung/iotjs/blob/master/src/iotjs_binding.h).

### JObject

`JObject` class stands for a real Javascript object. Upper layers will access Javascript object via this class.
This class provides following functionalities:

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
* Set and Get corresponding native data to the Javascript object.

### JObjectWrap

`JObjectWrap` is used for wrapping a Javascript object to a C++ instance.
The main purpose is to hand managing object's life cycle over to Javascript engine while linking the object with other data structures.
To create a instance of `JObjectWrap`, you need to supply a Javascript object and free handler.

To make sure that the Javascript object could be reclaimed by GC when there are no more references to that object, this wrapper will not increase reference count for the Javascript object.
Free handler will be invoked just before the Javascript object actually being reclaimed by GC and it will free the wrapper instance.

Make sure that wrapper should not be a created in stack space, it could lead double free(when it goes out scope and when corresponding object is being collected by GC). If you really want to use local wrapper, just using `JObject` would be enough. This wrapper must be create with C++ 'new' keyword.

And do not hold pointer to the wrapper in native code side globally because even if you are holding a wrapper by pointer, Javascript engine probably releases the corresponding Javascript object resulting  deallocation of wrapper. Consequentially your pointer turned into dangling.

The only safe way to get wrapper is to get it from Javascript object. When a wrapper is being created, it links itself with corresponding Javascript object with `SetNative()` method of [`JObject`](#jobject). And you can get the wrapper from the object with `GetNative()` method of [`JObject`](#jobject) later when you need it.

### Native handler

Some operations - such as file I/O, networking, device control, multitasking, and etc - can not be performed by pure Javascript.
IoT.js uses a mechanism called "native handler" to enable such operations performed from Javascript.
You can regard native handler as Javascript function object with its body implemented in C/C++.

You might think it is somewhat similar to [FFI](https://en.wikipedia.org/wiki/Foreign_function_interface).
In a wide sense, it's true for native handler is for calling C/C++ function from Javascript.
But in a narrow sense, it's not true.

Usually main purpose of [FFI](https://en.wikipedia.org/wiki/Foreign_function_interface) is to call a routine written in one language from a program written in another.
After a routine was invoked, it is common that the routine just do what it is supposed to do without knowing the surrounding context except arguments.
Whereas native handler does know that it is being called from Javascript (actually it is a Javascript function although not written in Javascript) and does access surrounding Javascript execution context using [embedding API](#embedding-api).

### Embedding API

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

Normally `ReqWrap` is created when there is a request and freed after the request is treated.

Note that `ReqWrap` does not inherits [`HandleWrap`](#handlewrap) to wrapping the callback function object.
This is because it need to prevent the callback function from being reclaimed by GC until finish handling the result.
As `HandleWrap` just hand over the managing lifecycle to Javascript engine without increasing reference count, we could not guarantee liveness of the callback function object if we use `HandleWrap`.

On the other hand, `ReqWrap` manages the reference count for callback function by itself - increasing reference count for the callback function when it is being created and decreasing when it is being freed
guaranteeing the liveness of callback function during processing request.
Also the function could be collected by GC when it need to be after request finished.

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

Javascript object fully implemented in C/C++ using [embedding API](#embedding-api) are called "builtin".
You can find list of builtin object at `MAP_MODULE_LIST` macro in ['iotjs_module.h'](https://github.com/Samsung/iotjs/blob/master/src/iotjs_module.h).

Builtin modules are very useful since it can accesss underlying system using libuv, C/C++ library, and system call by implementing its method as [native handler](#native-handler). And it may be used for optimizing performance of CPU bound routine and reduce binary size.

Builtin modules are initialized during [intializing step of IoT.js](#life-cycle-of-iotjs) and released just before the process terminates.

### Native module

The [basic modules and extended modules](https://github.com/Samsung/iotjs/wiki/IoT.js-API-Reference) provides by IoT.js are called 'native module' because that modules will be included IoT.js native binary. 
There is a [tool](https://github.com/Samsung/iotjs/blob/master/tools/js2c.pl) that transfer Javascript script source file into C++ header file.

Usually native modules need help from [builtin](#builtin) modules which are implemented in C/C++ thus able to access underlying system.

Some native modules are bound to global object while others are on demand.
On demand modules will be created at the moment when it is first required and will not released until the program terminates.

### Event loop

_Note:_
_It would be helpful to read [libuv design overview](http://docs.libuv.org/en/v1.x/design.html) to understand asynchronous I/O programming model if you are not familiar with it._

_Note:_
_In this section we will see simple file open example and relevant code segment. You can find the source files at ['iotjs.cpp'](https://github.com/Samsung/iotjs/blob/master/src/iotjs.cpp), ['iotjs_module_fs.cpp'](https://github.com/Samsung/iotjs/blob/master/src/iotjs_module_fs.cpp) and ['fs.js'](https://github.com/Samsung/iotjs/blob/master/src/js/fs.js)_


IoT.js follows asynchronous I/O programming model proposed by libuv to perform non-blocking, single-threaded, asynchronous I/O.

You can find main loop of the program at the file ['iotjs.cpp'](https://github.com/Samsung/iotjs/blob/master/src/iotjs.cpp) in the source tree. It looks like this:

```
  // Run event loop.
  bool more;
  do {
    more = uv_run(env.loop(), UV_RUN_ONCE);
    more |= ProcessNextTick();
    if (more == false) {
      more = uv_loop_alive(env.loop());
    }
  } while (more);
```

While running a IoT.js application, it could make requests for I/O operations using [IoT.js API](https://github.com/Samsung/iotjs/wiki/IoT.js-API-Reference).
For example, You can write a code for opening 'hello.txt' file and printing file descriptor out like this:
```
fs.open('hello.txt', 'r', function(err, fd) {
  console.log('fd:' + fd);
});
conosle.log('requested');
```

To handle the request, IoT.js will wrapping the request and callback function using [`ReqWrap`](#reqwrap). 
```
  FsReqWrap* req_wrap = new FsReqWrap(jcallback); 
```

libuv will take charge of actual I/O processing taking the request.
```
  uv_fs_t* fs_req = req_wrap->req(); \
  int err = uv_fs_open(env->loop(), \
                       fs_req, \
                       path, flags, mode, \
                       After);
```

Since all I/O are treated as non-blocking, calling for async I/O API returns immediately right after request was sent to libuv.
And then next line of javascript program will be executed continuously.
Thus in the above example 'requested' will be printed out right after file open request was made.

If there were I/O requests, `uv_run()` in the main loop waits by polling the requests until at least one of the request processing were finished.
When a result for a request was produced, internal part of libuv calls corresponding handler function(let it be after function) back. 

Usually, the after function retrieves I/O result and `ReqWrap` object from request data.
And calling the javascript callback function with the result.

```
  FsReqWrap* req_wrap = static_cast<FsReqWrap*>(req->data); // get request wrapper
  JObject cb = req_wrap->jcallback(); // javascript callback function

  JArgList jarg(2);
  jarg.Add(JObject::Null()); // in case of success.
  JObject arg1(static_cast<int>(req->result));
  jarg.Add(arg1); // result - file descriptor for open syscall

  // callback
  MakeCallback(cb, JObject::Null(), jarg);
```

For above file open example, calling javascript callback function would result execution of the handler.
```
function(err, fd) {
  console.log('fd:' + fd);
}
```

One iteration of event loop is finished and 'uv_run()' finally returns after all results were handled.
Next, it calls next tick handler.
```
    more |= ProcessNextTick();
```
And for next step, main event loop checks if there were no more request to be treated.
```
    if (more == false) {
      more = uv_loop_alive(env.loop());
    }
```
If there are another iteration of the loop executed. Otherwise, main event loop ends.