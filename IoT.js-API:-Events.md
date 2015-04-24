The application programming model of IoT.js is based on event-driven programming. Thus many objects in IoT.js emit events. `events.EventEmitter` plays a role as base class for such objects.

## Class: EventEmitter
You cannot directly create a instance of `EventEmitter` since `EventEmitter` is an abstract trait which defines and grants its behavior to classes that inherit `EventEmitter`. 

## Instance of EventEmitter
* emitter.on(event, listener)
* emitter.addListener(event, listener)
* emitter.once(event, listener)
* emitter.removeListener(event, listener)
* emiiter.removeAllListener([event])
* emitter.emit(event[, arg1[, arg2[...]]])