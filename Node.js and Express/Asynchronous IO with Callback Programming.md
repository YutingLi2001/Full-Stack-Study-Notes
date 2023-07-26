# Asynchronous I/O with Callback Programming
---
## Asynchronous I/O
- Network operations run in an asynchronous manner
- When an application blocks for a network operation to complete, that application wastes processing time on the server 
- Node.js makes all network operations in a non-blocking manner 
- To handle the result from a network call, you can write a ==callback function== that Node.js calls when the network operation completes

## Application calls http.request()
1. Application calls `http.request()` in Node.js 
2. Node.js send HTTP request to web service
3. Node.js returns a result for the `http.request()` call
	1. This indicated that the request message was sent successfully
4. Node.js receives HTTP response message from the server 
5. Node.js calls the callback function that you defined during the `http.request()` function call
- Callback function handles two events: 
	- `request.on('data')`
	- `request.on('end')`

## Example: sending an HTTP request
- host: the name of the remote server
- path: the URL
```js
let options = {
	host: 'w1.gov',
	path: '/xml/KSFO.xml'
};

http.request(options, function(response){
	let bugger = '';
	let result = '';
	response.on('data', function(chunk){
	buffer += chunk;
});

response.on('end',function(){
	console.log(buffer);
});
}).end();
```

## http.request options and callback
- `http.request` function calls the callback function parameter when it receives part of the HTTp response message
	- `heep.request(options,[callback function]);`
- when `http.request` calls the callback function, it passes a response object in the first parameter
	- `http.request(options, function(response){...});`

## Handling erro events
- If the request fail, there is an 'error' event followed by the 'close' event 
```js
let request = http.request( options, function(response){...});
request.on('error',function(e){
	resultCallback(e.message);
});
request.end();												
```
- The request method returns an object of type HTTP.ClientRequest
# Creating Callback Functions
---
## Introduction to Callbacks
- Node.js, being an asynchronous framework, extensively uses callback functions.
- Callback functions intercept HTTP method calls and return the result to the calling function.
- Node.js modules pass an error object as the first parameter in a callback function.
- If an error occurs, it is handled by the callback function, which also manages the cleanup of any open network or database connections.
- If there's no error, the callback function examines the result from the call.

## Callback Functions with Error Objects
- Callback functions check the first parameter to see if an error condition occurred.
- An error message is printed if an error is detected.
- The error object is passed back to the main application's callback function.

## Returning Response Message to the Original Calling Application
- The Node.js application can use a return function to have the callback function called after `http.request()` completes.
- This involves multiple stages:
  - The application calls the exported function.
  - The Node.js module makes a web service call using `http.request()`.
  - Control is returned to the Node.js module and then back to the application.
  - When the server sends back an HTTP response, the framework calls the callback handler defined by the Node.js module.
- The main application must provide a callback function to process the HTTP response message.

## Implementing a Callback Chain
- If the main application calls a function that in turn calls `http.request()`, two callback functions are involved:
  - The custom module's callback function handles the HTTP response message.
  - The main application's callback function processes the result captured by the first callback.
- This forms a chain of callbacks where one callback function invokes another, passing the message from the module back to the main application.

## Passing Callbacks to Modules
- The main application passes an anonymous callback function to process the result from the function call.
- The result callback function in the custom Node.js module links to the anonymous callback function of the main application.
- The `response.on('end')` event handler passes a value from one callback handler to another when the server finishes sending back the response message.
- This is how a value from a callback handler is passed to another.

# Expert Viewpoints
# Issues with Callbacks
---
### Understanding Callbacks
- A callback is a function passed as an argument to another function, which executes the callback based on the result.
- Callbacks ensure that a function won’t run before a prerequisite task is completed.
- Asynchronous callbacks are used for tasks such as accessing values from databases, downloading images, reading files, etc.

### Nested Callbacks
- When using callbacks to perform sequential tasks, functions need to be nested one within another.
- Every callback depends on and waits for the previous callback.
- ==Subsequent function becomes the argument passed to the next function==
- The nesting of callback functions often leads to "Callback Hell" or "The Pyramid of Doom", where nested callbacks form a pyramid-like structure. This structure affects the readability and maintainability of the code.

### Inversion of Control (IoC)
- Inversion of Control happens when the flow of control is external to your code.
- Callbacks often hand control over to a third party. This can introduce problems if the third-party code contains errors.
- Issues with third-party code can include: getting called too many or too few times, being called too early or too late, losing context, or passing back incorrect arguments.
- Managing these errors can lead to excessive "defensive" code.

### Mitigating Callback Issues
- There are a number of ways to mitigate callback hell and trust issues:
  - Writing comments to clarify code structure and behavior.
  - Splitting functions into smaller functions to improve manageability and readability.
  - Using Promises to simplify asynchronous operations.
  - Using async/await to write asynchronous code in a more synchronous, linear fashion.

# Promises
