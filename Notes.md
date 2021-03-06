# Node.js Notes

## Node.js Features

* **Asynchronous and Event Driven** All APIs of Node.js library are asynchronous that is, non-blocking. It essentially means a Node.js based server never waits for an API to return data. The server moves to the next API after calling it and a notification mechanism of Events of Node.js helps the server to get a response from the previous API call.
* **Very Fast** Being built on Google Chrome's V8 JavaScript Engine, Node.js library is very fast in code execution.
* **Single Threaded but Highly Scalable** Node.js uses a single threaded model with event looping. Event mechanism helps the server to respond in a non-blocking way and makes the server highly scalable as opposed to traditional servers which create limited threads to handle requests. Node.js uses a single threaded program and the same program can provide service to a much larger number of requests than traditional servers like Apache HTTP Server.
* **No Buffering** Node.js applications never buffer any data. These applications simply output the data in chunks.
* **License** Node.js is released under the MIT license.

## Node.js target applications

* I/O bound Applications
* Data Streaming Applications
* Data Intensive Real Time Applications (DIRT)
* JSON APIs based Applications
* Single Page Applications
* **NOT** CPU intensive Applications

## REPL

**REPL** stands for **Read** **Evaluate** **Print** **Loop** and it represents a computer environment like a window console or a Unix/Linux shell where a command is entered and system responds with an output in interactive mode. Node.js or Node comes bundled with a REPL environment. It performs the following desired tasks:
* **Read** Reads user's input, parse the input into JavaScript data-structure and stores in memory.
* **Evaluate** Takes and evaluates the data structure
* **Print** Prints the result
* **Loop** Loops the above command until user presses **ctrl-c** twice

## Event Driven Programming

Node.js uses events heavily and it is also one of the reasons why Node.js is pretty fast compared to other similar technologies. As soon as Node starts its server, it simply initiates its variables, declares functions and then simply waits for the event to occur.

In an event-driven application, there is generally a main loop that listens for events, and then triggers a call back function when one of those events is detected.

While events seem similar to callbacks, the differenct lies in the fact that callback functions are called when an asynchronous function returns its result, whereas event handling works on the **observer** pattern. The functions which listen listen to events act as observers. Whenever an event gets fired, its listener function starts executing. Node.js has multiple in-built events available through the **events** module and **EventEmitter** class which is used to bind events and event listeners as follows:

```javascript
// Import events module
var events = require('events');

// Create an EventEmitter object
var eventEmitter = new events.EventEmitter();
```

The following is the syntax to bind the event handler with an event;

```javascript
// Bind event and event handler as follows
eventEmitter.on('eventName', eventHandler);
```

Fire and event programmatically as follows:

```javascript
// Fire an event
eventEmitter.emit('eventName');
```

### EventEmitter Class

#### Methods

Method | Description
--- | ---
`addListener(event, listener)` | Adds a listener to the end of the listeners array for the specified event. No checks are made to see if the listener has already been added. Multiple calls passing the same combination of event and listener will result in the listener being added multiple times. Returns emitter, so calls can be chained.
`on(event, listener)` | Adds a listener to the end of the listeners array for the specified event. No checks are made to see if the listener has already been added. Multiple calls passing the same combination of event and listener will result in the listener being added multiple times. Returns emitter, so calls can be chained.
`once(event, listener)` | Adds a one time listener for the event. This listener is invoked only the next time the event is fired, after which it is removed. Returns emitter, so calls can be chained.
`removeListener(event, listener)` | Remove a listener from the listener array for the specified event. Caution: changes array indices in the listener array behind the listener. `removeListener` will remove, at most, one instance of a listener from the listener array. If any single listener has been added multiple times to the listener array for the specified event, then removeListener must be called multiple times to remove each instance. Returns emitter, so calls can be chained.
`removeAllListeners([event])` | Removes all listeners, or those of the specified event. It's not a good idea to remove listeners that were added elsewhere in the code, especially when it's an emitter that you didn't create (e.g. sockets or file streams). Returns emitter, so calls can be chained.
`setMaxListeners(n)` | By default, EventEmitters will print a warning if more than 10 listeners are added for a particular event. This is a useful default which helps finding memory leaks. Obviously not all Emitters should be limited to 10. This function allows for that to be increased. Set to zero for unlimited.
`listeners(event)` | Returns an array of listeners for the specified event.
`emit(event, [arg1], [arg2], [...], [argn])` | Execute each of the listeners in order with the supplied arguments. Returns true if event had listeners, false otherwise.

#### Class Methods

Method | Description
--- | ---
`listenerCount(emitter, event)` | Return the number of listeners for a given event.

#### Events

Event | Description
--- | ---
**newListener** | This event is emitted any time a listener is added. When this event is triggered, the listener may not yet have been added to the array of listeners for the event.
**removeListener** | This event is emmitted any time someone removes a listener. When this event is triggered, the listener may not yet have been removed from the array of listeners for the event.

## Buffers

Pure JavaScript is Unicode friendly but not nice to binary data. When dealing with TCP streams or the file system, it's necessary to handle octet streams. Node provides Buffer class which provides instances to store raw data similar to an array of integers but corresponds to a raw memory allocation outside the V8 heap.

Buffer class is a global class and can be accessed in an application without importing a buffer module.

### Creating Buffers

Node Buffer can be constructed in a variety of way.

#### Method 1

Create an uninitiated Buffer of 10 octets:

```javascript
var buf = new Buffer(10);
```

#### Method 2

Create a Buffer from a given array:

 ```javascript
 var buf = new Buffer([10, 20, 30, 40, 50]);
 ```

#### Method 3

Create Buffer from given string and encoding type:

```javascript
var buf = new Buffer("Simply Easy Learning", "utf-8");
```

### Writing to Buffers

#### Syntax

The syntax of the method to write into a Node Buff:

```javascript
buf.write(string[, offset][, length][, encoding])
```

#### Parameters

* **string** This is the string data to be written to the buffer.
* **offset** This is the index of the buffer to start writing at. Default value is 0.
* **length** This is the number of bytes to write. Defaults to buffer.length.
* **encoding** Encoding to use. 'utff8' is the default encoding.

#### Return value

The method returns the number of octets written. If there is not enough space in the buffer to fit the entire string, it will write a part of the string.

#### Example

```javascript
buf = new Buffer(256);
len = buf.write("Simply Easy Learning");

console.log("Octets written : " + len);
```

When executed, it should output: `Octects written : 20`

### Reading from Buffers

#### Syntax

Syntax of the method to read data from a Node Buffer:

```javascript
buf.toString([encoding][, start][, end])
```

#### Paramters

* **encoding** Encoding to use. 'utf8' is the default encoding.
* **start** Beginning index to start reading. Defaults to 0.
* **end** End index to end reading. Default is the complete buffer.

#### Return value

This method decodes and returns a string from buffer data encoded using the specified character set encoding.

#### Example

```javascript
buf = new Buffer(26);
for (var i = 0; i < 26; i++) {
	buf[i] = i + 97;
}

// outputs: abcdefghijklmnopqrstuvwxyz
console.log(buf.toString('ascii'));

// outputs: abcde
console.log(buf.toString('ascii', 0, 5));

// outputs: abcde
console.log(buf.toString('utf8', 0, 5));

// encoding defaults to 'utf8', outputs: abcde
console.log(buf.toString(undefined, 0, 5));
```

### Convert Buffer to JSON

#### Syntax

Syntax of the method to convert a Node Buffer into a JSON object:

```javascript
buf.toJSON();
```

#### Return Value

This method returns a JSON-representation of teh Buffer instance.

#### Example

```javascript
var buf = new Buffer('Simply Easy Learning');
var json = buf.toJSON();

console.log(json);
```

### Concatenate Buffers

#### Syntax

Syntax of the method to concatenate Node buffers to a single Node Buffer:

```javascript
Buffer.concat(list[, totalLength]);
```

#### Parameters

* **list** Array List of Buffer objects to be concatenated.
* **totalLength** This is the total length of the buffers when concatenated.

#### Return Value

This method returns a Buffer instance.

#### Example

```javascript
var buffer1 = new Buffer('TutorialsPoint ');
var buffer2 = new Buffer('Simply Easy Learning');
var buffer3 = Buffer.concat([buffer1, buffer2]);
console.log("buffer3 content: " + buffer3.toString());
```

### Compare Buffers

#### Syntax

Syntax of the method to compare two Node buffers:

```javascript
buf.compare(otherBuffer);
```

#### Parameters

* **otherBuffer** This is the other buffer which will be compared with **buf**.

#### Return Value

Returns a number indicating whether this comes before or after or is the same as the other Buffer in sort order.

#### Example

```javascript
var buffer1 = new Buffer('ABC');
var buffer2 = new Buffer('ABCD');
var result = buffer1.compare(buffer2);

if(result < 0) {
	console.log(buffer1 + " comes before " buffer2);
} else if(result == 0) {
	console.log(buffer1 + " is same as " + buffer2);
} else {
	console.log(buffer1 + " comes after " + buffer2);
}
```

In this example, the expected result is: `ABC comes before ABCD`

### Copy Buffer

#### Syntax

Syntax of the method to copy a node buffer:

```javascript
buf.copy(targetBuffer[, targetStart][, sourceStart][, sourceEnd]);
```

#### Parameters

* **targetBuffer** Buffer object where buffer will be copied.
* **targetStart** Number, Optional, Default: 0
* **sourceStart** Number, Optional, Default: 0
* **sourceEnd** Number, Opitonal, Default: buffer.length

#### Return Value

No return value. Copies data from a region of this buffer to a region in the target buffer even if the target memory overlaps with the source. If undefined, the targetStart and sourceStart parameters default to 0 while the sourceEnd defaults to buffer.length.

#### Example

```javascript
var buffer1 = new Buffer('ABC');
var buffer2 = new BUffer(3);

buffer1.copy(buffer2);
console.log("buffer2 content: " + buffer2.toString());
```

When executed, it produces: `buffer2 content: ABC`

### Slice Buffer

#### Syntax

Syntax of the method to get a sub-buffer of a node buffer:

```javascript
buf.slice([start][, end]);
```

#### Parameters

* **start** Number, Optional, Default: 0
* **end** Number, Optional, Default: buf.length

#### Return Value

Returns a new buffer which references the same memory as the old, but offset and cropped by the start (defaults to 0) and end (defaults to buf.length) indices. Negative indices start from the end of the buffer.

#### Example

```javascript
var buffer1 = new Buffer('TutorialsPoint');
var buffer2 = buffer1.slice(0, 9);
console.log("buffer2 content: " + buffer2.toString());
```

When executed, this produces: `buffer2 content: Tutorials`

### Buffer Length

#### Syntax

Syntax of the method to get a size of the node buffer in bytes:

```javascript
buf.length;
```

#### Return Value

Returns a size of buffer in bytes.

#### Example

```javascript
var buffer = new Buffer('TutorialsPoint');
console.log("buffer length: " + buffer.length);
```

When executed, outputs: `buffer length: 14`

## Streams

### What Are Streams?

Four types of streams:

* **Readable** Stream which is used for read operation
* **Writable** Stream which is used for write operation
* **Duplex** Stream which can be used for both read and write operation
* **Transform** Duplex where the output is computed based on input

Streams are **EventEmitter** instances and throw several evants and different times.  Commonly used events are:

* **data** This event is fired when there is data available to read
* **end** This event is fired when there is no more data to read
* **error** This event is fired when there is any error receiving or writing data
* **finish** This event is fired when all data has been flushed to underlying system

