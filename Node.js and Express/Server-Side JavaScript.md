# Introduction
--- 
## What are Node.js and Express
- Node.js 
	- Runtime environment
	- Server-side JavaScript applications
- Express
	- Server-side JavaScript web framework
	- Runs on top of Node.js 

# What is Back End Development?
---
## Front end vs. back end
- Front end
	- runs on a client machine
		- client machine runs browser engine, browser engine communicate with the back-end server 
- Back end 
	- runs on a server 
	- codes that communicate with the browser's engine and back-end server
	- backend development refers to the development of the server-side logic:
		- Code that pertains to databases, servers , and applications 

## Back-end technologies:
- Includes: servers, databases, web APIs, programming languages, frameworks, and runtimes
- Servers can refer to hardware, software, or both 
- Servers communicate with and provide functionality to a client
- Servers also communicate with and provide functionality to each other 

## Types of servers:
- Database servers
	- House, retrieve, and deliver data
- Application servers
	- Host and deliver the application through HTTP
	- Sit between a database server and a web server 
	- Transform data into content
	- Run business logic 
		- Data storage rules
		- Data transfer rules 
- Web servers 
	- Ensure client requests are responded to, often using HTTP (hypertext transfer protocol)
	- An HTTP server is part of the software running on a web server 
	- The software part of a web server is what controls how a user accesses files hosted on the server

## Web APIs
- How two pieces of software communicate 
- Web services
	- Types of a web API 
	- Communicate using HTTP

## Frameworks
- Provide structure for code 
- Generate code that cannot be altered
- Back-end frameworks include:
	- Django(Python)
	- Ruby on Rails(Ruby)
	- Express.js(JavaScript)
- Express.js
	- Framework that runs on top of Node.js
	- Handles the HTTP requests made to a web server 

## Runtime environments
- Like a mini operating system that provides the resources necessary for an application to run
- The infrastructure that supports the execution of a codebase
- The environment in which an application gets executed
- Node.js is a back-end runtime environment 

## Node.js
- Run on Google Chrome's V8 engine
- The V8 engine also runs on the client's front-end browser 
- Executes JavaScript
- JavaScript can be used on the front end and on the back end 

## Backend responsibility: scalability
- Load
	- Number of concurrent users
	- Number of concurrent transactions
	- Amount of concurrent data transfer between clients and servers 
- Scalability 
	- Application's ability to handle changes in load without affecting performance
	- Essential for client-server application success 

## Other back-end responsibilities
- Security
- Authentication
- Malware prevention 
- Perfomance 
# Getting Started with Node.js
--- 
## Node.js: Event-driven, Asynchronous, Non-blocking, Single-Threaded
- Single-threaded: only one command is processed at a given point in time.
- Asynchronous & non-blocking: while a process is being executed, the program doesn't have to wait until the process finishes.
- Event-driven: when Node.js performs an IO operation, an event is triggered, instead of blocking the thread and wasting the processor time waiting, Node.js will resume the operations when the response comes back, during the time, the server is not blocked and can do other things, which makes it look like it is multi-threaded. 

## JSON Payload
```json
{
	"name":"John",
	"age":"24",
	"email":"johnparker@gmail.com"
}
```
- JSON stands for JavaScript Object Notation
- Formatted as "key-value pairs"

## Express Framework
- Makes Node.js simple to create APIs and endpoints
- API endpoint is the specific point of entry for a request from client to the server. 
# Introduction to Node.js
---
## Node.js definition
- Open-source language that runs on V8
- Can run on Linux, Windows and Mac OS

## Node.js functionality
- Serverside JS
- Event-driven, and uses asynchronous, non-blocking I/O

## JavaScript with Node.js
1. User interact with UI
2. Action by user triggers JS code that implements the business
3. JS application makes a HTTP request with a JSON data payload
4. The REST web service, which is part of a node.js application receives the HTTP request
5. The REST web service processes the request and returns the result to the client as a JSON payload over HTTP

## Express.js
- Configurable framework for building applications on Node.js 
- Abstracts lower-level APIs in Node.js by using HTTP utility methods and middleware

## Express.js features
- Public: public assets like image, CSS, and JavaScript 
- Template/views: server-rendered HTML that is sent back to the client in response to requests
- Routes: defines endpoints that accept and process client requests
- Server.js: a file which contains the main application code 
- Package.json: contains metadata information about the project including dependencies, scripts, and so on.

# Some features of Node.js
---
- Has an abundance of packages and registries such as NPM
- Can handle high volume of concurrent connections
- Provides faster processing of concurrent requests
	- Popular choice for solutions that require constantly updated date 
		- Such as online gaming, chats, video conferences 
- Works well with microservices
- Single threaded and relies on callbacks
- Can parse JSON amazingly fast since JSON is a native data type in Node.js

# Import and Require
---
## Modules
- Related, encapsulated JS code
- Serves as a single purpose
- Can be a single file or a folder containing files
- Reusable
- Breaks down complex code into manageable chunks

## Purpose of import() and require()
- When an external application needs to use the code in a module
	- It needs to call that module 
	- The module is called using an import() or require()

## Packages and specifications
- A directory with one or more modules bundled together is called a package
- Module specifications:
	- Conventions and standards used to create packages
	- Commonly used Node.js specifications:
		- CommonJS
		- ES

## Enable ES modules
- By default, Node.js treats JS code as a CommonJS module
- Library authors can easily enable ES modules in a Node.js package by simply changing the package file extension from `.js` to `.mjs`

## Importing and exporting modules
- CommonJS
	- import: `require()`
	- export: `module.exports`
- ES
	- import: `import()`
	- export: `export`

## Differences calling `require()` and `import()`
- `require()`
	- Can be called anywhere in the code
	- Can be called within conditionals and functions
	- Dynamic
		- Binding errors not identified until run-time
- `import()`
	- Can only be called at the beginning of the file
	- Cannot be called within conditionals or functions
	- Static
		- Binding errors identified at compile-time

## Synchronous vs. asynchronous
- `require()`
	- Synchronous
		- Linear load of modules, one at a time
- `import()`
	- Asynchronous
		- Modules can be processed simultaneously 
		- Runs faster in large-scale applications

## Example 
```js
//require()
//export from a file named 'message.js'
module.exports = 'Hello Programmers';

//import from the 'message.js' 
let msg = require('./message.js');
console.log(msg);

//import()
//export from a file named 'message.mjs'
const a = 1;
export { a as "myvalue" };

//import from 'message.mjs'
import { myvalue } from "module.mjs";
```
# Creating a Web Server with Node.js
---
## Node.js 
- Heavy emphasis on concurrent programming with a lightweight language
- Single-threaded application that handles I/O operations through events
- Callback functions that handle results when they complete

## Node.js modules
- Every JS file is a module in Node.js
- Multiple modules can be grouped into a package

## Simple HTTL web server
```js
let server = http.createServer(function(request, response)){
	let body = "Hello world!";
	response.writeHdea(200,{
		'Content-Length': body.length,
		'Content-Type':'text/plain'
	});
	response.end(body);
});
server.lesten(8080);
```
# Working with Node.js Modules
---
## Package.json: the module manifest
- A package consists of one or more modules
- Every package has a package.json file that describes details about a Node.js module
	- If a module does not have a package.json file, Node.js assumes that the main class is named `index.js`
- To specify a different main script for your module, specify a relative path to the Node.js script from the module directory
	- The name and version form a unique identifier
	- The main field list a path to the main node.js script
```json
{
	"name": "mod_today",
	"version": "1.0.0",
	"main": "./lib/today",
	"license": "Apache-2.0"
}
```

## Importing Node.js modules
- Use the `require` function to import a Node.js module 
	- `let today = require('./today');`
		- The require statement assumes that scripts have a file extension of .js 
- The require function creates an object that represents the imported Node.js module 

## Export functions and properties
- Each Node.js module has an implicit exports object
- To make a function or a value available to Node.js applications that import your module, add a property to exports
	- 
```js
exports.dayOfWeek = function(){
	return days[ date.getDay() - 1];
};
```

## Accessing exported properties
- When you import a Node.js module, the require function returns a JS object that represents an instance of the module 
	- `let today = require('./mod_today');`
- To access the properties of the module, retrieve the property from the variable 
	- `console.log("Heppy %s!", today.dayOfWeek());`

# Advanced Node.js Modules
---
## Three types of Node.js modules
- Core
	- Contains the minimal functionality needed to develop Node.js applications
- Local 
	- Modules written by you and the development team as part of creating your Node.js application
- Third-party
	- Available online and have been created by the back-end Node.js community.
# Overview of Node Package Manager
--- 
## Package managers
- Set of tools to deal with modules and packages containing dependencies

## Dependencies
- Code in the form of a library or a package reused in a program 
- Libraries and packages contain many dependencies
- A library does not depend on code outside of it to function 

## Package manager responsibilities
- Automate the process of ==finding, installing, upgrading, configuring, maintaining and removing packages== for a computer program
- Package managers:
	- Maintain a database of dependencies and versioning
	- Ensures software has correct dependencies

## Node package manage (NPM)
- Default package manager for Node.js 
- Two functions 
	- Provides a CLI to publish and download packages
	- Behaves as an online repository of JS packages
- The repository is a database of packages that tracks package versions

## package.json file
- File located in a project's root directory
- NPM uses package.json to determine dependencies
- Contains key-value pairs that identify the project 
- ==MUST== contain
	- Project name 
	- Project version

## Local install
- NPM packages can be installed locally or globally
- Use local install for use with packages within your application
- Run the local install command from the directory you want the package installed in 
- Local install is NPM's default behaviour

## Local install command
- Use the NPM CLI to enter:
	- `npm install <package_name>`
- This command creates a directory named node_modules with the package and its dependencies in your current working directory 

## Global install
- Packages can also be installed globally
- A globally installed package will be used by all applications on the machine 
- If you have different versions, they will all use the globally installed packages
	- Might break compatibility with other dependencies 

## GLobal install command
- `npm install -g <package_name>`
