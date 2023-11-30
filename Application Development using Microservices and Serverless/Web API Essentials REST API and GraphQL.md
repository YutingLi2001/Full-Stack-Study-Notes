# What is REST?

## Overview
REST, or Representational State Transfer, is an architectural style that outlines how applications should communicate within a network. RESTful APIs have become the predominant method for connecting components in microservices architectures, offering a flexible and lightweight means to integrate applications.

## Characteristics of a REST API
RESTful APIs are characterized by three main features:

1. **HTTP Request Management**: All requests are managed through HTTP.
2. **Stateless Communication**: The communication between client and server is stateless, which means each request from the client contains all the necessary information to process it, without taking advantage of any stored context on the server.
3. **Uniform Interface**: There is a consistent and uniform interface for interaction between components.

## CRUD Operations
REST APIs use HTTP requests to perform CRUD (Create, Read, Update, Delete) operations on resources:

- `POST`: Create a new record.
- `GET`: Retrieve an existing record.
- `PUT`: Update an existing record.
- `DELETE`: Delete a record.

## Stateless Nature and Scalability
According to Roy Fielding:

> "Each request from client to server must contain all of the information necessary to understand the request, and cannot take advantage of any stored context on the server. Session state is therefore kept entirely on the client."

This stateless nature contributes significantly to the scalability of RESTful APIs.

## Uniform Interface
A REST API ensures that the same piece of data, such as a product ID, is accessed using only one URI. Resources should be self-contained and include all the data the client might need, like the name and price of a product.

## Example: CEX.IO API
CEX.IO is a cryptocurrency exchange that offers access to Bitcoin, other crypto prices, and market data through its REST API. The API is well-documented, with detailed information on request and response parameters, and sample code snippets in various programming languages.

### Sample Request
To request the last price of a currency pair through the CEX.IO public API:

```javascript
// Example in JavaScript
// Replace 'currencyPair' with the actual ID of the currency pair.
fetch('https://cex.io/api/last_price/{currencyPair}')
  .then(response => response.json())
  .then(data => console.log(data));
```

# Introduction to API Gateway

## What is an API Gateway?
An API Gateway acts as a management tool that serves as an intermediary between clients and a collection of backend services. It aggregates services, manages requests, and returns the appropriate result to the client.

## Benefits of Using an API Gateway
- **Security**: Protects APIs from overuse and malicious threats, often incorporating an authentication service with rate limiting.
- **Analytics and Monitoring**: Provides insights into API usage.
- **Monetization**: Integrates with billing systems to monetize APIs.
- **Single Point of Contact**: Simplifies client interactions by providing a unified interface to microservices.
- **Flexibility in Backend Management**: Facilitates the addition or removal of backend services without affecting the client interface.

## Drawbacks of Using an API Gateway
- **Maintenance**: Requires additional development and maintenance efforts.
- **Single Point of Failure**: Risks becoming a bottleneck if not designed robustly.
- **Latency**: May increase response time due to the additional network layer.

## Examples of API Gateway Products
- **Managed Products**:
  - IBM DataPower Gateway
  - Google Apigee
  - Google Cloud Endpoints
  - Microsoft Azure API Management
  - Amazon AWS API Gateway
- **Open-Source Options**:
  - Kong
  - Apache APISIX
  - Tyk (also available as managed)
  - Gloo (available in an enterprise version)

## Conclusion
API Gateways provide significant advantages by streamlining client access to microservices, concealing backend complexity, and easing scalability and service management. However, they introduce additional components that require careful design and maintenance. A range of API Gateway products are available, offering solutions for various requirements and preferences.


# Creating REST APIs with Flask in Python

## Introduction
Python is a versatile language that's used across many domains including web development, scientific computing, and artificial intelligence. Flask is a micro web framework for Python that is particularly well-suited for building lightweight and scalable RESTful APIs.

## Prerequisites
- Python 3
- pip (Python package manager)

## Setting up Flask
To get started with Flask, install it using pip:
```bash
pip install Flask
```

## Creating a Basic Flask Application
1. Create a file named `hello.py`.
2. Add the following content to `hello.py`:

```python
from flask import Flask
app = Flask(__name__)

@app.route('/')
def hello_world():
    return 'Hello, World!'
```

3. Run the Flask server:
```bash
export FLASK_APP=hello.py
flask run
```

4. Access the application in a web browser at `127.0.0.1:5000` to see the "Hello World" response.

## Building a Products Microservice
1. Create a new Python file named `products.py`.
2. Define the imports and set up a list of default products:

```python
from flask import Flask, jsonify

app = Flask(__name__)

# Example product list
products = [
    {"id": 1, "name": "Laptop", "price": 800},
    {"id": 2, "name": "Mouse", "price": 20},
    {"id": 3, "name": "Monitor", "price": 150}
]

@app.route('/products', methods=['GET'])
def get_products():
    return jsonify(products)
```

3. Run the Flask server as before and access the `/products` endpoint to retrieve the list of products.

## HTTP Status Codes
When the `GET` method is defined, it implicitly returns HTTP status `200 OK` if the request is successful.

## Conclusion
With Flask, you can quickly create a RESTful API microservice in Python. This microservice can handle HTTP requests and return responses in JSON format, making it suitable for a wide range of applications.

To start your Flask REST API, ensure you have the correct environment variable set and then run the Flask application:

```bash
export FLASK_APP=products.py
flask run
```

Your API will be accessible at `127.0.0.1:5000/products`, returning the list of products in JSON format.


# Making API Requests using cURL and Postman

## Overview
- **Goal**: Learn to make HTTP requests using cURL and Postman.
- **cURL**: A command-line tool for transferring data using various protocols.
- **Postman**: An API platform for building and using APIs with a user-friendly interface.

## cURL
- **Short for**: Client URL.
- **Use Cases**:
  - Downloading files from the internet.
  - Endpoint testing, debugging, and error logging.
- **Supported Protocols**: HTTP, HTTPS, FTP, IMAP.

### Basic cURL Command Example

```bash
curl -X GET "http://example.com/api/products" -H "Content-Type: application/json"
```

### Components of cURL Command
- `-X`: Specifies the HTTP method (e.g., GET, POST).
- `-H`: Defines headers (e.g., Content-Type: application/json).

### cURL Options
- Options start with one (`-`) or two (`--`) dashes.
- Single-dash options that don't require additional values can be combined (e.g., `-X GET`).

## Postman
- **Description**: A suite of tools for API development.
- **Features**:
  - Orchestrate multiple requests.
  - Streamline collaboration.
  - Convert API requests to code for languages like JavaScript, Python.
- **Use Cases**: Testing APIs, automating testing with pre-filled data.
- **Accessibility**: Available as a desktop application and an online version.

### Using Postman for API Requests
1. Open a new tab in Postman.
2. Set the request type to GET.
3. Enter the URL of the microservice.
4. Click on the `Send` button to make the request and analyze the output.
5. Save the request in the workspace for future use.

## Summary
- cURL is a versatile tool for data transfer with URLs, suitable for command line or scripting.
- Postman provides an intuitive platform for API development and testing, with features that speed up the process and facilitate collaboration.



# Module 2 Summary

- REST APIs provide flexible but uniform interfaces between components
- REST APIs are stateless and scalable
- REST APIs communicate using HTTP methods POST, GET, PUT and DELETE
- REST is an architectural style defining how applications communicate
- API Gateway is the door to your backend services while also enabling you to plug additional services while providing unified access
- API Gateway makes it easier to scale or replace your backend services
- Flask is a micro web framework to host Python web applications
- cURL is used for transferring data with URLs and can be used at a command line or in scripts
- Postman is a simple and popular tool for building, testing, and using APIs
- Swagger helps you document and test your API
- OpenAPI specification is a standard way of representing your APIs