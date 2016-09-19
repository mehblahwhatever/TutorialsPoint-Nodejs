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

