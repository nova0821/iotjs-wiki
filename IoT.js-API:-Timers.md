## class: Timers

### Methods

#### setTimeout(callback, delay)
* Schedules to call one-time to `callback` function after `delay` milliseconds.
* `callback`: Function
* `delay`: delay in milliseconds to call `callback`
* return: timeoutObject

#### clearTimeout(timeoutObject)
* disables timeout call from `setTimeout` method 
* `timeoutObject': Object returned from `setTimeout`

#### setInterval(callback, delay)
* Schedules to call periodic to `callback` function after every `delay` milliseconds.
* `callback`: function
* `delay`: delay in milliseconds to call `callback`
* return: intervalObject

#### clearInterval(intervalObject)
* disables timeout call from `setInterval` method
* `intervalObject`: Object returned from `setInterval`
