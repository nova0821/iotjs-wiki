### Getting Started with Examples
As **iot.js** is asynchronous and event-driven, programming style is pretty much different from traditional blocking synchronous programming. This tutorial lets you know how to code with **iot.js** mainly focused on asynchronous style.

#### hello world
Firstly, create a javascript file (e.g. `hello.js`) and open it. Then type as following.
```
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

#### read/write files
.

#### a echo server
.

### Module System