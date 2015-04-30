## Class: Stream.Readable

Readable stream is abstraction for data for read, so you can read data out from a readable stream.

At any time a readable stream is in one of two state: **flowing** and **paused**. In paused state, readable stream emits `'readable'` event for you that indicates there are data ready for read. and then you can explicitly call `stream.read()` to get the data form the stream. In flowing state, readable stream emits `'data'` event with actual data that you can receive data as fast as possible. All streams start out in paused mode.

### Events

#### 'readable'

Readable stream emits this event when a chunk of data prepared to be read.
This event only emitted when the stream is in paused state.


#### 'data'
* `chunk: Buffer | String`

Readable stream emits this event when a chunk of data prepared to be read.
This event only emitted when the stream is in flowing state.

Attaching a `data` event listener to a stream makes the stream to be switched to flowing mode.
 

#### `end`
This event is only fired when there will be no more data to read.

#### 'close'
Emitted when the underlying resource has been closed.


### Methods

#### readable.read([size])

#### readable.resume()

#### readable.pause()

#### readable.isPaused()
