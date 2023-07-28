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
---

**Definition:** A Promise is an object returned by an asynchronous method, representing the eventual completion (or failure) of an asynchronous operation and its resulting value.

## States of a Promise:

1. **Pending:** Initial state, neither fulfilled nor rejected.
2. **Fulfilled (Resolved):** Operation completed successfully.
3. **Rejected:** Operation failed.

Promises are especially useful for API requests, I/O operations, and other time-consuming tasks that could block resources.

## Using Promises:

A method can return a Promise object when its execution might take some time and potentially block resources.

```javascript
let methCall = new Promise((resolve, reject) => { 
    // operations 
});
```

## Package Example - Axios:
The `axios` package in Node.js is used to handle HTTP requests and returns a Promise object. The `then` method of a Promise is executed once the Promise is resolved, while `catch` is executed when the Promise is rejected.

```javascript
axios.get('url')
  .then((response) => { console.log(response); })
  .catch((error) => { console.log(error); });
```

## Recap
- A **Promise** is an object representing the eventual completion or failure of an asynchronous operation. - 
- Promises have three states: **Pending**, **Fulfilled (Resolved)**, and **Rejected**.
- Methods that perform time-consuming tasks that might block resources can return a Promise.
- Packages like `axios` in Node.js handle HTTP requests and return Promises. The `then` method handles resolved promises and `catch` deals with rejected ones.
- 

# Working with JSON

## Key Concepts

- **JSON**: Standard format for API data exchange, consisting of attribute-value pairs.
- **Node.js**: Handles JSON effectively.
- **JSON methods**:
  - `JSON.parse()`: Converts a JSON string into a JavaScript object.
  - `JSON.stringify()`: Converts a JavaScript object into a JSON string.

## Example

```javascript
// JSON object example
let obj = {
  "Company" : "IBM",
  "Country" : "USA",
  "Headquarters" : "Armonk, New York"
};

// Using JSON.stringify()
let jsonStr = JSON.stringify(obj);
console.log(jsonStr);

// Using JSON.parse()
let jsonObj = JSON.parse(jsonStr);
console.log(jsonObj);
```

# Expert Viewpoints: Using JSON and JavaScript

## Key Concepts

1. **Importance of JSON and JavaScript:**
   - **JavaScript** is essential for web developers, particularly for front-end development.
   - **JSON** is the de facto standard for data serialization, commonly used in APIs and data specifications. It is extensively used in Node.js projects and deployments for platform as a service offerings or Kubernetes workloads.

2. **JSON and JavaScript Interplay:**
   - **JSON** is a native data type in JavaScript. Serialization and deserialization convert JSON objects into a byte string and vice versa.
   - **JSON** is a common communication format in RESTful web services and Node.js development. Familiarity with JSON is critical for interacting with request and response objects in cloud REST APIs, particularly at the curl or shell script level.
   
3. **Working with JSON Oriented Document Databases:**
   - Knowledge of JavaScript and JSON is beneficial when working with JSON oriented document databases.

4. **JavaScript as the Language of the Internet:**
   - JavaScript is widely used in many applications, making it a valuable skill to add code to existing projects or write JavaScript from scratch.
   - JSON is used by modern languages, including Python and Node.js, and is a popular method for structuring data and interacting with APIs.

```javascript
// Example of a JSON object in JavaScript
let jsonObject = {
    "name": "John Doe",
    "email": "john.doe@example.com",
    "age": 30
};
```

## Conclusion

Both JavaScript and JSON play a crucial role in today's web development landscape, particularly in the development of cloud applications and REST APIs. Becoming proficient in these technologies can greatly enhance a developer's ability to effectively create, contribute to, and interact with modern web applications.

# An Introduction to Async/Await

## Key Concepts

1. **JavaScript's Asynchronous Programming:**
   - JavaScript is a single-threaded language. Processes occur sequentially, not simultaneously.
   - JavaScript overcame this by introducing asynchronous programming through **Promises**.
   - Despite solving synchronous programming issues, nested 'then' statements can complicate code structure and readability.

2. **Introduction of Async/Await (ES 2017):**
   - Async/Await addressed the issue of complicated nested promises, resulting in cleaner, more readable code.
   - By 'awaiting' a promise, we process the result once the promise is fulfilled (or rejected).

## Code Examples

### Promise with callback handling `resolve` and `reject`

```javascript
const axios = require('axios');
const connectToURL = (url) => {
  const req = axios.get(url);
  req.then(resp => {
      let listOfEntries = resp.data.entries;
      listOfEntries.forEach((entry) => console.log(entry.Category));
    })
    .catch(err => console.log(err.toString()));
}
connectToURL('https://api.publicapis.org/entries');
```

### Same functionality using Async/Await

```javascript
const axios = require('axios');
const connectToURL = async(url) => {
    const outcome = await axios.get(url);
    let listOfEntries = outcome.data.entries;
    listOfEntries.forEach((entry) => console.log(entry.Category));
}
connectToURL('https://api.publicapis.org/entries');
```

### Promises in sequence using Async/Await

```javascript
const axios = require('axios');
async function connectToURL(url) {
    const resp = await axios.get(url);
    let listOfEntries = resp.data.entries;
    let Categories = [...new Set(listOfEntries.map((entry) => entry.Category))];
    Categories.forEach(async (Category) => {
      if (Category.startsWith("A")) {
              try {
                const resp = await axios({
                  method: 'get',
                  url: "https://api.publicapis.org/entries?Category="+Category,
                  responseType: 'json'
                })
                console.log(Category+"   "+resp.data.count);
              } 
              catch(e) {
                console.log(e);
              }
      }
    });
}
connectToURL('https://api.publicapis.org/entries').catch(err => console.log(err.toString()));
```

## Conclusion

Async/Await simplifies JavaScript's asynchronous programming, resulting in cleaner, more readable code. It's important to note that await can only be used inside an async function because await blocks the thread.





# Extending Node.js with Third-Party Packages

## Objectives

1. Extend Node.js with third-party packages.
2. Define package dependencies.

## Introduction

Node.js provides a robust framework to build an HTTP server, but the default framework is limited in certain aspects such as routing, parsing incoming files, authentication, and connecting to a database, among others. Developers often rely on external libraries and packages to extend the core Node.js functionality.

## Parsing XML Data

As an example, consider the need to parse XML data in Node.js. You could use JavaScript string functions, but these are not efficient for parsing a stream of XML data. Instead, developers rely on packages such as xml2js.

Suppose you need to retrieve weather data from an external web server. You can send an HTTP request and parse the received data manually, treating web service messages as a string. However, this approach has several disadvantages:

- String matching ignores the structure of XML data.
- The message body might contain malformed XML data.
- Depending on the complexity of the XML data, string matching might be less efficient than building an XML tree of the data.
- String matching is less tolerant to changes in the XML data structure.

## Introducing xml2js Package

The xml2js Node.js package provides a way to parse a string of XML elements into a JavaScript object. This package is purely written in JavaScript and doesn't require an XML parsing library written in another language.

**Note:** Before installing third-party packages, always verify their licensing terms to ensure they are compatible with your project's requirements.

To install xml2js, you can use the Node Package Manager (npm) with the following command:

```bash
npm install xml2js
```

This command retrieves and installs the xml2js Node.js module and any dependencies that it requires.

## Example

After installing the package, you can import it into your application:

```javascript
const parseString = require('xml2js').parseString;
// Assume buffer contains the XML data
parseString(buffer, function (err, result) {
  console.log(result.current_observation.temp_f[0]);
});
```

Here, the `parseString` function calls the callback function after processing the XML tree. The `result` variable represents the contents of the XML fragment in JavaScript form. The property `current_observation.temp_f[0]` maps to the first child element in the `temp_f` XML element, which is a child of the `current_observation` element.

## Conclusion

- Developers use third-party packages to extend Node.js's features.
- String matching is not an efficient way to parse XML data.
- The xml2js Node.js package converts a string of XML elements into a JavaScript object.
- The npm application manages Node.js packages in your Node.js framework installation.

# Expert Viewpoints: Working with 3rd Party Node.js Extensions

- **Serverless Framework**: Simplifies deploying serverless microservices in the cloud.
- **Lodash**: Utility library for handling collections and arrays.
- **Axios**: Promise-based HTTP client for managing RESTful API interactions.
- **Express Middleware Packages**: Helpful for handling tasks like authentication and JWT management.
- **Database Packages**: Aid in communication with external databases, whether relational or NoSQL.

# Introduction to Web Frameworks

## Key Concepts

1. **Node.js vs Node.js-based web frameworks**:
    - Node.js: Runtime environment that executes JavaScript on a server. It's not a web framework.
    - Node web framework: Works in conjunction with Node.js, providing a skeleton on which an application is built.

1. **Architectural Styles**:
    - **Model-View-Controller (MVC)**: 
        - Divides an application into three components: model, view, and controller.
        - Model: Manages the data of the application, interacting with the database and handling data logic.
        - View: Renders the presentation of the data passed to it by the model.
        - Controller: Regulates the flow of the data, processing user supplied data and sending it to the model for manipulation or storage.
    - **Representational State Transfer Application Programming Interfaces (REST APIs)**:
        - Allows multiple web services to communicate with each other.
        - RESTful APIs are independent, stateless 
        - Communicate from client to Server via operations on resources using ==HTTP methods== (GET, POST, PATCH, DELETE). 
        - The data transferred back to client can be in various formats like JSON, HTML, XLT, Python, PHP, or plain text.

1. **Node web frameworks**:
    - **Express.js**: Used for routing and middleware. It delivers high performance, handles multiple operation requests concurrently, provides debugging mechanisms and HTTP helpers. 
    - **Koa**: A new web framework designed by the same team behind Express. It uses async functions to eliminate the need for callbacks and enhances error handling capabilities.
    - **Socket.io**: Ideal for apps requiring real-time bidirectional data exchange between clients and servers. Suitable for applications such as chat rooms, texting applications, video conferencing, and multiplayer games.
    - **Hapi.js**: An open-source framework known for its reliability and built-in security. It's used for developing proxy and API servers, HTTP-proxy applications, REST APIs, and other desktop applications.
    - **NestJS**: Designed for building dynamic, scalable enterprise applications. It uses an MVC architecture and is compatible with TypeScript. It's built on top of Express and works in conjunction with the Angular front-end framework.

# Express Web Application Framework

## Key Concepts

1. **Express framework**:
    - A web application framework based on the Node.js runtime environment.
    - Express abstracts low-level details, aiding in application organization and faster development.
    - Provides robust mechanisms for integrating middleware packages and handling different HTTP request methods.

1. **Primary Uses of Express**:
    - **API Development**: 
        - Express is used to set up an HTTP interface to interact with the data layer. 
        - Data is sent back to the client in JSON format using a response object (`res`), with `res.json` method notifying the client of the content type and stringifying data.
    - **Server-Side Rendering (SSR)**:
        -  Express is used to set up templates, dynamically writing HTML, CSS, and JavaScript using the data sent from the client supplied by an HTTP request. This is achieved using the `res.render` method.

1. **Working with Express**: Express application development follows five steps:
    - Declare Express as a dependency in the package manifest of a Node.js project.
        - Create a `package.json`
            - Name, Version, Description, Main & Dependencies
                - Main: Identifies the Node.js script as the entry point into the module 
    - Run the npm command to download any missing modules.
    - Import the Express module and create an Express application.
    - Create a new route handler.
    - Start an HTTP server on a given port number.

## Summary

- Express is a third-party module that provides a framework for building web applications.
- Express serves two purposes: to set up APIs and to implement SSR.
- To install Express, there are five steps: Declare Express as a dependency in the package manifest of a Node.js project, run the npm command to download any missing modules, import the Express module and create an Express application, create a new route handler, and finally, start an HTTP server on a given port number.

# Your First Express Web Application

## Key Concepts

1. **Steps to work with Express**:
    - Declare Express as a dependency in the package manifest of your Node.js project.
    - Run the npm command to download any missing modules.
    - Import the Express module and create an Express application.
    - Create a new route handler.
    - Start an HTTP server on a given port number.

2. **Creating an Express application**: After declaring Express as a dependency and downloading any missing modules, a Node.js file (for example, `mynodeserver.js`) can be created in the project folder. This marks the beginning of Express programming.

3. **Creating an instance of the app**: After importing the Express web application framework, create an instance of the app JavaScript object from the framework.

4. **Creating a new route handler**: The application should handle web application requests by mapping an HTTP method and a web resource path to the JavaScript function. For instance, listening to incoming HTTP GET requests to the 'temperature' resource path.

5. **Starting an HTTP server**: To create an instance of the server from the app, call `app.listen` to create a web server object that listens to incoming requests on the specified port. For example, on port 8080.

## Summary
- Creating an Express application involves declaring Express as a dependency in a Node.js project, downloading any missing modules, importing the Express module, creating an Express application, creating a new route handler, and starting an HTTP server on a given port number.
- The Express framework makes it possible to handle web application requests by mapping an HTTP method and a web resource path to a JavaScript function.
- An HTTP server can be started by creating an instance of the server from the app, which listens to incoming requests on the specified port.

# Expert Viewpoints: Working with Backend JavaScript frameworks and Express

## Key Concepts

1. **Express.js for backend web apps**: Express.js is a widely-used framework for building backend web applications. It allows high-level, expressive declaration of REST API endpoints, enhancing both productivity and code readability.

2. **Middleware usage**: Express.js has a strong community that has developed a range of middleware for various purposes, such as parsing body content, authentication, handling user sessions, and request logging.

3. **Ease of use and productivity**: Express.js facilitates a shorter development lifecycle due to its ease of use and flexibility. It can be used to quickly develop web applications.

4. **Express.js abstracts low-level code**: Express.js handles a lot of the low-level code that developers would otherwise have to write themselves, making them more effective and efficient.

5. **Best practices and community-driven framework**: Express.js is built on certain best practices and is an open-source, community-driven framework. This ensures reliability and adherence to the most efficient approaches in web development.

6. **Scalability and performance**: Express.js supports rapid scaling of applications and delivers high performance, supported by the Google V8 engine.

7. **Caching feature and third-party integration**: Express.js supports caching, enabling faster loading of web pages and reducing the need for re-execution of codes. It also allows integration of several third-party applications and services.

8. **Use of managed services in the cloud**: Some developers may prefer using fully managed services in the cloud, which handle API requests and other backend functionalities, reducing the need for Express.js.

# Routing, Middleware, and Templating

## Key Concepts

1. **Routing in Express**: 
	1. Routing is a critical feature of server-side scripting. 
	2. It allows the server to handle requests (GET, POST, PUT, DELETE) directed at various routes or return appropriate error messages. 
	3. Routing can be managed at either the application level or the router level. 
	4. Express allows for both simple routing when there are fewer endpoints or routes and more complex routing when dealing with many endpoints using routers.

2. **Middleware in Express**: 
	1. Middleware consists of functions that have access to the request and response objects, as well as a 'next' function, which defines what happens after the function executes. 
	2. Middleware types include application-level, router-level, error handling, built-in, and third-party.
	3. Middleware is useful for various tasks like parsing requests, adding authentication, and handling errors.

3. **Template Rendering in Express**: 
	1. Template rendering enables the server to fill in dynamic content in HTML templates.
	2. This feature can be used with various view engines, like express-react-views for rendering React components from the server.
	3. The view engine is responsible for creating HTML from your views, which are usually written in JSX code.

# Authentication and Authorization in Node.js

## Key Concepts

- **Authentication**: The process of confirming a user's identity using credentials by validating who they claim to be.
- **Authorization**: The process of providing the user access to specific resources in the system.
- **Session-based, Token-based, and Passwordless**: The three popular authentication methods in Node.js.

## Session-Based Authentication

- Oldest form of authentication technology.
- User logs in using credentials which are verified against a database.
- The server creates a session with a unique, encrypted session ID, stored in the database and the user's browser.
- The session ID is destroyed once the user logs out or after a specified amount of time.

## Token-Based Authentication

- It consists of two parts: authentication and authorization.
- User provides credentials to obtain a token (authentication).
- The token (usually a JSON Web Token or JWT) contains:
  - **Header**: Information about the type of token and the algorithm used.
  - **Payload**: User attributes, such as permissions, groups, and expirations.
  - **Signature**: Verifies the integrity of the token.
- An ID token is passed to the web server as proof of authentication.
- Access tokens (separate from ID tokens) are used to authorize resource access.

```javascript
// Example of using JWT for token-based authentication
const jwt = require('jsonwebtoken');

// generate a token
let token = jwt.sign({data: 'userData'}, 'secret', { expiresIn: '1h' });

// verify a token
jwt.verify(token, 'secret', function(err, decoded) {
  console.log(decoded) // userData
});
```

## Passwordless Authentication

- User authenticates by proving possession of a specific factor (e.g., a fingerprint, a magic link sent via email, or a one-time passcode sent to a mobile device).
- Utilizes Public Key and Private Key Encryption:
  - **Public Key**: Used to encrypt messages, stored with the application and registered with a registration service.
  - **Private Key**: Used to decrypt messages, stored on the user's device.
- Upon login, the application generates a challenge (e.g., request for biometrics, sending a magic link), encrypts it with the public key, and the private key is used to decrypt the message.

```javascript
// Example of passwordless authentication using public/private keys
// Simplified example - in reality, keys should be securely stored and managed

const crypto = require('crypto');
const { publicKey, privateKey } = crypto.generateKeyPairSync('rsa', {
  modulusLength: 2048,
});

const text = 'Hello, world!';
const encrypted = crypto.publicEncrypt(publicKey, Buffer.from(text));
const decrypted = crypto.privateDecrypt(privateKey, encrypted);

console.log('Decrypted text: ', decrypted.toString());
```

# Authentication in Node.js

## Key Learning Objectives

1. Understand the advantages of token-based authentication in Node.js.
2. Implement token-based authentication and authorization in Node.js.

## Token-Based Authentication

Token-based authentication is a popular method for implementing authentication in Node.js due to several key advantages:

- **Scalability**: Tokens are stored client-side, making the system more scalable.
- **Flexibility**: Tokens can be used across multiple servers, allowing authentication across various websites and applications simultaneously.
- **Security**: Tokens (e.g., JWTs) can be signed and encrypted to prevent tampering and unauthorized reading.

## Implementing Token-Based Authentication and Authorization

Consider a scenario where we're developing an Express.js API server that provides access to employee data. The application will have two APIs:

1. **POST API for Login**: Returns a token after verifying the user's credentials.
2. **GET API for Employee Data**: Provides employee information that only authenticated users can access.

```javascript
const express = require('express');
const jwt = require('jsonwebtoken');

const myapp = express();
const JWT_SECRET = 'JWT_SECRET';

myapp.use(express.json());

myapp.post('/login', (req, res) => {
  const { username, password } = req.body;
  if (username === 'user' && password === 'password') {
    const token = jwt.sign({ user: username }, JWT_SECRET);
    return res.json({ token });
  } else {
    return res.status(401).json({ message: 'Invalid username and/or password' });
  }
});

myapp.get('/employees', (req, res) => {
  const authHeader = req.headers.authorization;
  if (!authHeader) {
    return res.status(401).json({ message: 'No Token' });
  }

  const token = authHeader.split(' ')[1];
  try {
    const payload = jwt.verify(token, JWT_SECRET);
    if (payload.user === 'user') {
      return res.json({ message: 'Access Successful to Employee Endpoint' });
    }
  } catch (e) {
    return res.status(401).json({ message: 'Please login to access this resource' });
  }
});

myapp.listen(5000, () => console.log('API Server is localhost:5000'));
```

To execute the server, save the file as `api-server.js` and run `node api-server.js`.

In this code:

- We set up an Express.js server.
- The `/login` endpoint receives a `POST` request with the user's credentials and returns a token if the credentials match the stored values.
- The `/employees` endpoint receives a `GET` request, checks the Authorization header for a token, verifies the token, and returns employee data if the user is authenticated.

To verify the secure endpoint cannot be accessed unless the user is authorized, run this curl command:

```bash
curl -X GET 'http://localhost:5000/employees'
```

You should see the message: "Please login to access this resource".

## Recap

In this session, you learned:

- The advantages of token-based authentication include scalability, flexibility, and security.
- The `POST` API is used during authentication to log a user into an application.
- The `GET` API is used in authorization to determine which resources a user can access.
- A JSON web token (JWT) is used to authenticate a user and authorize their resource access.
---
# Express Best Practices

- **Directory Structure:**
  - `bin`: Contains the script for starting your app.
  - `config`: Includes all configuration related files like database configuration.
  - `models`: Holds all the data models for your application.
  - `routes`: Contains all route definitions for your Express application.
  - `views`: Stores all template files which are used to render data.
  - `public`: Holds all static files like styles, scripts, and images.
  - `app.js`: The entry point to your app.
  - `package.json`: Keeps track of all your npm dependencies.
- **Designing API Routes:**
  - Use nouns to represent resources (e.g., `/users`, `/orders`).
  - Use HTTP methods (GET, POST, PUT, DELETE) to perform CRUD operations on these resources.

```javascript
app.get('/users', function(req, res){
  // code to fetch users
});

app.post('/orders', function(req, res){
  // code to create an order
});
```

- **Error Handling:**
  - 2XX codes for successful operations.
  - 4XX codes for client errors.
  - 5XX codes for server errors.

```javascript
app.get('/users', function(req, res){
  if(error){
    res.status(500).send(error);
  } else {
    res.status(200).send(users);
  }
});
```

- **Testing:**
  - Use libraries like Mocha and Chai for unit and integration tests.

```javascript
describe('GET /users', function() {
  it('responds with json', function(done) {
    request(app)
      .get('/users')
      .expect('Content-Type', /json/)
      .expect(200, done);
  });
});
```

- **Stateless Authentication:**
  - Consider using JWT (JSON Web Tokens) for stateless authentication.

```javascript
const jwt = require('jsonwebtoken');
const token = jwt.sign({ foo: 'bar' }, 'secret');
```

- **Documentation:**
  - Always create comprehensive API documentation.
  - Tools like Swagger can help.

```yaml
swagger: "2.0"
info:
  version: "1.0.0"
  title: "Simple API"
paths:
  /users:
    get:
      summary: "Returns a list of users"
      responses:
        200:
          description: "A JSON array of user objects"
```

---

