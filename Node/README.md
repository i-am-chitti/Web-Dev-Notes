---
title: Node JS
created: '2021-05-26T06:53:21.931Z'
modified: '2021-07-16T16:44:03.263Z'
---

Node JS
--------------------------------------
## Introduction

The problem with native Javascript to run only in browser was overcome by NodeJS. Node can be used to write server-side applications with access to OS, file system, and everything else required to build fully-functional applications.

__Node.js is an open-source and cross-platform JavaScript runtime environment__. It is a popular tool for almost any kind of project!

Node.js runs the V8 JavaScript engine, the core of Google Chrome, outside of the browser. This allows Node.js to be very performant.

__A Node.js app runs in a single process__, without creating a new thread for every request. Node.js provides a set of asynchronous I/O primitives in its standard library that prevent JavaScript code from blocking and generally, libraries in Node.js are written using non-blocking paradigms, making blocking behavior the exception rather than the norm.

When Node.js performs an I/O operation, like reading from the network, accessing a database or the filesystem, instead of blocking the thread and wasting CPU cycles waiting, Node.js will resume the operations when the response comes back.

This allows Node.js to handle thousands of concurrent connections with a single server without introducing the burden of managing thread concurrency, which could be a significant source of bugs.

Node.js has a unique advantage because millions of frontend developers that write JavaScript for the browser are now able to write the server-side code in addition to the client-side code without the need to learn a completely different language.

In Node.js the new ECMAScript standards can be used without problems, as you don't have to wait for all your users to update their browsers - you are in charge of deciding which ECMAScript version to use by changing the Node.js version, and you can also enable specific experimental features by running Node.js with flags.


## Why Node?

Node uses 'an event driven, non-blocking I/O model'. Node JS is built well to handle asynchronous Javascript code to perform many asynchronous activities such as reading and writing to file, handling connections to DB servers, or handling requests to web server. It uses a callback-based system to handle asynchronous activities.

```
const fs = require('fs');

fs.readFile('./script.js', function(error, data) {
  // error is null if no error occurred, but an Error object if it did
  if (error) {
   throw error;
  }
  // the file data will be passed into the callback if no error was thrown
  console.log(data);
});
```


### Blocking vs Non-blocking

Blocking is when the execution of additional JavaScript in the Node.js process must wait until a non-JavaScript operation completes. This happens because the event loop is unable to continue running JavaScript while a blocking operation is occurring.

n Node.js, JavaScript that exhibits poor performance due to being CPU intensive rather than waiting on a non-JavaScript operation, such as I/O, isn't typically referred to as blocking. Synchronous methods in the Node.js standard library that use `libuv` are the most commonly used blocking operations. Native modules may also have blocking methods.

All of the I/O methods in the Node.js standard library provide asynchronous versions, which are non-blocking, and accept callback functions. Some methods also have blocking counterparts, which have names that end with `Sync`.

JavaScript execution in Node.js is single threaded, so concurrency refers to the event loop's capacity to execute JavaScript callback functions after completing other work. Any code that is expected to run in a concurrent manner must allow the event loop to continue running as non-JavaScript operations, like I/O, are occurring.

As an example, let's consider a case where each request to a web server takes 50ms to complete and 45ms of that 50ms is database I/O that can be done asynchronously. Choosing non-blocking asynchronous operations frees up that 45ms per request to handle other requests. This is a significant difference in capacity just by choosing to use non-blocking methods instead of blocking methods.

The event loop is different than models in many other languages where additional threads may be created to handle concurrent work.

### What does asynchronicity mean?

Computers are asynchronous by design.

Asynchronous means that things can happen independently of the main program flow.

In the current consumer computers, every program runs for a specific time slot and then it stops its execution to let another program continue their execution. This thing runs in a cycle so fast that it's impossible to notice. We think our computers run many programs simultaneously, but this is an illusion (except on multiprocessor machines).

Programs internally use interrupts, a signal that's emitted to the processor to gain the attention of the system.

Let's not go into the internals of this now, but just keep in mind that it's normal for programs to be asynchronous and halt their execution until they need attention, allowing the computer to execute other things in the meantime. When a program is waiting for a response from the network, it cannot halt the processor until the request finishes.

Normally, programming languages are synchronous and some provide a way to manage asynchronicity in the language or through libraries. C, Java, C#, PHP, Go, Ruby, Swift, and Python are all synchronous by default. Some of them handle async operations by using threads, spawning a new process.

__JavaScript is synchronous by default and is single threaded. This means that code cannot create new threads and run in parallel.__

But JavaScript was born inside the browser, its main job, in the beginning, was to respond to user actions, like `onClick`, `onMouseOver`, `onChange`, `onSubmit` and so on. How could it do this with a synchronous programming model?

The answer was in its environment. The browser provides a way to do it by providing a set of APIs that can handle this kind of functionality.

A callback is a simple function that's passed as a value to another function, and will only be executed when the event happens. We can do this because JavaScript has first-class functions, which can be assigned to variables and passed around to other functions (called higher-order functions)

Starting with ES6, JavaScript introduced several features that help us with asynchronous code that do not involve using callbacks: Promises (ES6) and Async/Await (ES2017).


### Node JS Architecture

[Reference Video](https://www.youtube.com/watch?v=dT5QizZIDFw&list=PLEfl6gYIDWgYmMGpQYYvc49escwlGvDUa)

It's a runtime environment which is powered by V8 Javascript engine that compiles the Javascript code to machine code and `libuv` library that offers ways to access OS, network calls, file system etc. `libuv` library also has event loop and thread pool. This library is written in C++. V8 engine is written in JS and C++.

Node JS runs as a process (instance of a program under execution) and is single threaded (sequence of instructions). So, whether there are 10 users or millions of users, they are served by this single thread.

Here is how a node program is executed -

- Initialize the program
- Execute the 'top level' code
- require modules
- register event callbacks
- start event loop.

Now, event loop does the work. But works which are blocking in nature or expensive are offloaded to thread pool. Thread Pool is provided by `libuv` library which itself run as a process. This process has at least 4 threads (can be upto 128). These 4 threads takes the offloaded work and do them. Some tasks - file system calls, cryptography, compression, DNS lookups.

Event loop is the heart of NodeJS.

#### V8 Engine

V8 is the JavaScript engine i.e. it parses and executes JavaScript code. The DOM, and the other Web Platform APIs (they all makeup runtime environment) are provided by the browser. The cool thing is that the JavaScript engine is independent of the browser in which it's hosted. This key feature enabled the rise of Node.js.


### Javascript is compiled or interpreted?

JavaScript is generally considered an interpreted language, but modern JavaScript engines no longer just interpret JavaScript, they compile it.

This has been happening since 2009, when the SpiderMonkey JavaScript compiler was added to Firefox 3.5, and everyone followed this idea.

JavaScript is internally compiled by V8 with __just-in-time (JIT) compilation__ to speed up the execution.

Our applications can now run for hours inside a browser, rather than being just a few form validation rules or simple scripts.

In this new world, compiling JavaScript makes perfect sense because while it might take a little bit more to have the JavaScript ready, once done it's going to be much more performant than purely interpreted code.

### Runtime Environments

There are two runtime environments that javascript is executed in and they have their own implementation of various javascript methods.
1. Node runtime: ```process.env.PWD``` prints the current working directory
2. Browser's runtime: ```window.alert()``` executes only in browser.

## The Node REPL

REPL is an abbreviation for read–eval–print loop. It’s a program that loops, or repeatedly cycles, through three different states: a read state where the program reads input from a user, the eval state where the program evaluates the user’s input, and the print state where the program prints out its evaluation to a console. Then it loops through these states again.

## `process` object

Node has a global `process` object with useful methods and information about the current process.

The `process.env` property is an object which stores and controls information about the environment in which the process is currently running. For example, the `process.env` object contains a `PWD` property which holds a string with the directory in which the current process is located. It can be useful to have some `if/else` logic in a program depending on the current environment— a web application in a development phase might perform different tasks than when it’s live to users. We could store this information on the `process.env`. One convention is to add a property to process.env with the key `NODE_ENV` and a value of either `production` or `development`.

```
console.log(process.env);
console.log(process.memoryUsage()); // an object consiting heap meomory used, toal memory etc
console.log(prcess.argv[2]) // node app.js deepak -> prints deepak
```

## Browser vs Node.js

- `document`, `window` and all the other objects that are provided by the browser are not available in Node.js
- All APIs that Node.js provides through its modules like file system acess etc are not available in browser.
- In Node.js you control the environment. You know which version of Node.js will the application run on. But in browser, you don't have luxury to choose which browser visitor will use. This means that you can write all the modern ES2015+ JavaScript that your Node.js version supports. Since JavaScript moves so fast, but browsers can be a bit slow to upgrade, sometimes on the web you are stuck with using older JavaScript / ECMAScript releases. You can use Babel to transform your code to be ES5-compatible before shipping it to the browser, but in Node.js, you won't need that.
- Another difference is that Node.js supports both the CommonJS and ES module systems (since Node.js v12), while in the browser we are starting to see the ES Modules standard being implemented.
- In practice, this means that you can use both require() and import in Node.js, while you are limited to import in the browser.


## Event-Driven Architecture

Node provides an EventEmitter class which we can access by requiring in the events core module:

```
// Require in the 'events' core module
let events = require('events');

// Create an instance of the EventEmitter class
let myEmitter = new events.EventEmitter();

let newUserListener = (data) => {
  console.log(`We have a new user: ${data}.`);
};

// Assign the newUserListener function as the listener callback for 'new user' events
myEmitter.on('new user', newUserListener)

// Emit a 'new user' event
myEmitter.emit('new user', 'Lily Pad') //newUserListener will be invoked with 'Lily Pad'
```

Each event emitter instance has an `.on()` method which assigns a listener callback function to a named event. The `.on()` method takes as its first argument the name of the event as a string and, as its second argument, the listener callback function.

Each event emitter instance also has an `.emit()` method which announces a named event has occurred. The `.emit()` method takes as its first argument the name of the event as a string and, as its second argument, the data that should be passed into the listener callback function.

## User Input/Output

When we use `console.log()` we prompt the computer to output information to the console. In the Node environment, the console is the terminal, and the `console.log()` method is a “thin wrapper” on the `.stdout.write()` method of the process object. stdout stands for standard output.

In Node, we can also receive input from a user through the terminal using the `stdin.on()` method on the process object:

```
process.stdin.on('data', (userInput) => {
  let input = userInput.toString()
  console.log(input)
});
```

Here, we were able to use `.on()` because under the hood `process.stdin` is an instance of `EventEmitter`. When a user enters text into the terminal and hits enter, a `'data'` event will be fired and our anonymous listener callback will be invoked. The `userInput` we receive is an instance of the Node Buffer class, so we convert it to a string before printing.

## Errors

The Node environment has all the standard JavaScript errors such as `EvalError`, `SyntaxError`, `RangeError`, `ReferenceError`, `TypeError`, and `URIError` as well as the JavaScript Error class for creating new error instances. Within our own code, we can generate errors and throw them, and, with synchronous code in Node, we can use error handling techniques such as `try...catch` statements.

Many asynchronous Node APIs use error-first callback functions: callback functions which have an error as the first expected argument and the data as the second argument. If the asynchronous task results in an error, it will be passed in as the first argument to the callback function. If no error was thrown, the first argument will be `undefined`.

```
const errorFirstCallback = (err, data)  => {
  if (err) {
    console.log(`There WAS an error: ${err}`);
  } else {
     // err was falsy
      console.log(`There was NO error. Event data: ${data}`);
  }
}
```

## Modular Programming

Modules are reusable pieces of code in a file that can be exported and then imported for use in another file. A modular program is one whose components can be separated, used individually, and recombined to create a complex system.
![Modules](../images/modules_in_node.PNG)

Benefits of isolating code into separate files called modules are:
1. find, fix and debug easily
2. reuse and recycle logic
3. keep information private and protected
4. prevent naming collisions and assign scopes separately

### Modules in Node runtime

Every JavaScript file that runs in a Node environment is treated as a distinct module. The functions and data defined within each module can be used by any other module, as long as those resources are properly exported and imported.

* Export a module:
```
/* converters.js */
function celsiusToFahrenheit(celsius) {
  return celsius * (9/5) + 32;
}

module.exports.celsiusToFahrenheit = celsiusToFahrenheit;

module.exports.fahrenheitToCelsius = function(fahrenheit) {
  return (fahrenheit - 32) * (5/9);
};
```

* Import a module:
```
/* water-limits.js */
const converters = require('./converters.js');
const { celsiusToFahrenheit, farenheitToCelsius } = require('./converter.js'); // destructuring to be more selective

const freezingPointC = 0;
const boilingPointC = 100;

const freezingPointF = converters.celsiusToFahrenheit(freezingPointC);
const boilingPointF = converters.celsiusToFahrenheit(boilingPointC);

console.log(`The freezing point of water in Fahrenheit is ${freezingPointF}`);
console.log(`The boiling point of water in Fahrenheit is ${boilingPointF}`);
```

### Modules in Browser runtime or using ES 6 syntax:
For applying the module to HTMl, do it like this:
```
<script type="module" src="main.js"></script>
```
* export a module
```
/* dom-functions.js */
export const toggleHiddenElement = (domElement) => {
  // logic omitted...
}

export const changeToFunkyColor = (domElement) => {
  // logic omitted...
}
```
* Import a module:
```
import { toggleHiddenElement, changeToFunkyColor } from '../modules/dom-functions.js';
import { greet as greetInHindi } from 'greeterHindi.js'
```
* Default Export and imports
Every module also has the option to export a single value to represent the entire module called the default export
Exporting
```
const resources = {
  valueA,
  valueB
}
export { resources as default };
export { resA, resB };

OR

export default resources;
```
Importing
```
// This will work...
import resources from 'module.js'
const { valueA, valueB } = resources;

// This will not work...
import { valueA, valueB } from 'module.js'
```

__require__ is used to import modules in Node runtime
__module.exports__ is used to export modules in Node runtime
__export default resA__ is used to export module in ES6 syntax
__import__ is used to import module in ES6 syntax

## Readable Streams

One of the simplest uses of streams is reading and writing to files line-by-line. To read files line-by-line, we can use the `.createInterface()` method from the `readline` core module. `.createInterface()` returns an EventEmitter set up to emit `'line'` events:

```
const readline = require('readline');
const fs = require('fs');

const myInterface = readline.createInterface({
  input: fs.createReadStream('text.txt')  // fs.createReadStream('text.txt') which will create a stream from the text.txt file.
});

myInterface.on('line', (fileLine) => {
  console.log(`The line read: ${fileLine}`);
});
```

## Writeable Stream

We can create a writeable stream to a file using the `fs.createWriteStream()` method:

```
const fs = require('fs')

const fileStream = fs.createWriteStream('output.txt');

fileStream.write('This is the first line!');
fileStream.write('This is the second line!');
fileStream.end();
```

In the code above, we set the output file as output.txt. Then we `.write()` lines to the file. Unlike a readable stream, which ends when it has no more data to read, a writable stream could remain open indefinitely. We can indicate the end of a writable stream with the `.end()` method.

## Creating an HTTP Server

Node was designed with back end development needs as a top priority. One of these needs is the ability to create web servers, computer processes that listen for requests from clients and return responses. A Node core module designed to meet these needs is the http module. This module contains functions which simplify interacting with HTTP and streamline receiving and responding to requests.

The http.createServer() method returns an instance of an http.server. An http.server has a method .listen() which causes the server to “listen” for incoming connections. When we run http.createServer() we pass in a custom callback function (often referred to as the requestListener). This callback function will be triggered once the server is listening and receives a request.

Let’s break down how the requestListener callback function works:

* The function expects two arguments: a request object and a response object.
* Each time a request to the server is made, Node will invoke the provided requestListener callback function, passing in the request and response objects of the incoming request.
* Request and response objects come with a number of properties and methods of their own, and within the requestListener function, we can access information about the request via the request object passed in.
* The requestListener is responsible for setting the response header and body.
* The requestListener must signal that the interaction is complete by calling the response.end() method.

```
const http = require('http');

let requestListener = (request, response) => {
  response.writeHead(200, {'Content-Type': 'text/plain' });
  response.write('Hello World!\n');
  response.end();
};

const server = http.createServer(requestListener);

server.listen(3000);
```

Let’s walk through the above code:

* We required in the http core module.
* We created a server variable assigned to the return value of the http.createServer() method.
* We invoked http.createServer() with our requestListener callback. This is similar to running the .on() of an EventEmitter: the requestListener will execute whenever an HTTP request is sent to the server on the correct port.
* Within the requestListener callback, we make changes to the response object, response, so that it can send the appropriate information to the client sending the request. The status code 200 means that no errors were encountered. The header communicates that the file type is text, rather than something like audio or compressed data.
* The last line starts the server with the port 3000. Every server on a given machine specifies a unique port so that traffic can be correctly routed.

You could run the above code on your local machine, and access it by visiting http://localhost:3000/ from your browser. “localhost” is used to refer to the same computer that’s running the current Node process.

## Comments

- Single Line
- Multi line
- Hashbang - There's a special third comment syntax, the hashbang comment. A hashbang comment behaves exactly like a single line-only `(//)` comment, except that it begins with `#!` and is only valid at the absolute start of a script or module. Note also that no whitespace of any kind is permitted before the `#!`. The comment consists of all the characters after `#!` up to the end of the first line; only one such comment is permitted.

## Review

* Node.js is a JavaScript runtime, an environment that allows us to execute our JavaScript code by converting it into something a computer can understand.
* REPLs are processes that read, evaluate, print, and repeat (loop), and Node.js comes with its own REPL we can access in our terminal with the node command.
* We run JavaScript programs with Node in the terminal by typing node followed by the file name (if we’re in the same directory) or the absolute path of the file.
* Code can be organized into separate files, modules, and combined through requiring them where needed using the `require()` function.
* In addition to core modules, modules included within the environment to efficiently perform common tasks, we can also create our own modules using `module.exports` and the require() function.
* We can access NPM, a registry of hundreds of thousands of packages of re-usable code from other developers, directly through our terminal.
* Node has an event-driven architecture.
* We can make our own instances of the EventEmitter class and we can subscribe to listen for named events with the `.on()` method and emit events with the `.emit()` method.
* Node uses an event loop which enables asynchronous actions to be handled in a non-blocking way by adding callback functions to a queue of tasks to be executed when the callstack is empty.
* In order to handle errors during asynchronous operations, provided callback functions are expected to have an error as their first parameter.
* Node allows for both output, data/feedback to a user provided by a computer, and input data/feedback to the computer provided by the user.
* The Node `fs` core module is an API for interacting with the file system.
Streams allow us to read or write data piece by piece instead of all at once.
* The Node `http` core module allows for easy creation of web servers, computer processes that listen for requests from clients and return responses.
