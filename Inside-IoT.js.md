# Inside IoT.js

* [Design](#design)
* [IoT.js Core](#IoT.js Core)
* [Javascript Binding](#javascript-binding)
* [libuv Binding](#libuv-binding)

## Design

IoT.js is built on top of [JerryScript](http://samsung.github.io/jerryscript) and [libuv](http://libuv.org). JerryScript is a lightweight Javascript engine intended to run on small devices for IoT and libuv is a library for supporting asynchronous I/O. 

A big picture of IoT.js is looks like following figure.
 
![Layout of IoT.js](https://github.com/Samsung/iotjs/blob/wikiattach/doc/InsideIoTjs/IoTjs_big_layout.jpg)

The layer related to IoT.js project is green colored box on above figure.

As you can see, it runs upon JerryScript  and libuv. There is a layer that binds JerryScript and libuv to IoT.js. We will discuss about that layer on [Javascript Binding](#javascript-binding) and [libuv Binding](#javascript-binding) section on this document respectively.

## IoT.js Core

## Javascript Binding

## libuv Binding
