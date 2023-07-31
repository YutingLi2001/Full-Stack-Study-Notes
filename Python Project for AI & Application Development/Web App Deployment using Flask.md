# Python Libraries and Frameworks for Application Development

## Learning Outcomes

- Describe the Python libraries for app development
- Define a framework for app development
- Identify the benefits of using a framework for app development
- Compare frameworks and libraries

## Python Libraries

Python libraries are like toolkits. Each library has specific tools to simplify and expedite certain programming tasks. 

- Libraries like NumPy facilitate advanced mathematical calculations.
- Pandas offer data manipulation and analysis capabilities.
- Matplotlib simplifies data visualization.

For web application development, some Python libraries are essential. 

- The Requests library simplifies the process of sending HTTP requests.
- BeautifulSoup makes it easy to scrape information from web pages.
- SQLAlchemy is a SQL toolkit and Object-Relational Mapping (ORM) tool.
- PyTest is a testing framework that allows users to create small, simple tests.

## Frameworks for App Development

Frameworks are predefined structures for application development. They provide a set of guidelines for application development. Frameworks facilitate good coding practices and enable the reuse of code libraries. Examples include Django, Flask, and Web2Py.

### Benefits of Using a Framework

- **Eases the development process:** Frameworks offer pre-written code libraries, modules, and developer guidelines.
- **Simplifies debugging:** With pre-built debugging tools, web frameworks simplify the debugging process.
- **More functionality with less code:** Frameworks are equipped with several pre-built libraries and modules, which developers can leverage when creating their code.
- **Improves database management efficiency:** Frameworks come with built-in database integration tools for seamless data transfer.
- **Enforces security:** Developers can leverage the built-in security features and guidelines to enforce security.

## Comparison: Frameworks and Libraries

- A framework contains the basic flow and the architecture of an application, which enables you to build the complete application.
- A Python library is a set of packages that perform only specific functionality.

## Summary

- Python libraries are like toolkits. Each library has specific tools to simplify and expedite certain programming tasks.
- Frameworks are predefined structures for application development.
- Using frameworks provides various benefits, including easing the development process, simplifying the debugging process, enabling more functionality with less code, improving database management efficiency, and enforcing security.
- A framework enables you to build the complete application while libraries aid with specific functionality.

# Introduction to Flask

## Learning Outcomes

- Define the Flask web framework and describe its main features
- Explain how to install Flask on your machines
- Describe main dependencies of Flask
- Explain the main differences between Flask and another Python web framework called Django

## Flask: A Micro Web Framework

Flask is a micro framework used to create web applications. Unlike larger, opinionated frameworks, Flask does not bind the user to a specific set of tools. Flask 2.2.2 requires a minimum Python version of 3.7. 

## History

Flask was created in 2004 by Armin Ronacher as an April Fool's joke. Despite its humorous origins, Flask quickly gained popularity for its ease of use and extensibility.

## Main Features

- **Web Server:** Flask has a web server for running applications in development mode.
- **Debugger:** Flask's debugger helps debug applications with interactive traceback and stack trace in the browser.
- **Logging:** Flask uses standard Python logging for application logs.
- **Testing:** Flask provides a way to test different parts of your application, facilitating a test-driven approach.
- **Request and Response Objects:** Developers can access these objects to pull arguments and customize responses.

## Additional Features

- **Static Assets:** Flask supports static assets like CSS files, JavaScript files, and images.
- **Dynamic Pages:** Using the Jinja templating framework, dynamic pages can be developed.
- **Routing:** Flask provides routing and supports dynamic URLs for RESTful services.
- **Error Handlers:** You can write global error handlers in Flask.
- **Session Management:** Flask supports user session management.

## Community Extensions

- **Flask-SQLAlchemy:** Adds support for SQLAlchemy ORM to Flask.
- **Flask-Mail:** Provides the ability to set up an SMTP mail server.
- **Flask-Admin:** Allows you to add admin interfaces to Flask applications.
- **Flask-Uploads:** Allows you to add customized file uploading to your application.
- **Flask-CORS:** Allows your application to handle Cross-Origin Resource Sharing.
- **Flask-Migrate:** Adds database migrations to SQLAlchemy ORM.
- **Flask-User:** Adds user authentication, authorization, and other user management activities.
- **Marshmallow:** Adds object serialization and deserialization support to your code.
- **Celery:** A powerful task queue for background tasks and complex multi-storage programs.

## Installation

Flask can be installed using the Python package manager called pip. For installing Flask on your machines, it is recommended that you first create a virtual environment using the venv or bin venv module.

## Dependencies

- **Werkzeug:** Implements WSGI (Web Server Gateway Interface), the standard Python interface between applications and servers.
- **Jinja:** A template language that renders the pages in your application.
- **MarkupSafe:** Comes with Jinja and helps avoid injection attacks by escaping untrusted input.
- **ItsDangerous:** Used to sign data securely, protecting Flask's session cookie.
- **Click:** A framework for writing command-line applications, it provides the Flask command and allows adding custom management commands.

## Flask vs Django

- Flask is a very lightweight framework, providing only the basic dependencies needed to create a web application, whereas Django is a full-stack framework.
- Flask is very flexible, allowing developers to add and remove pieces in a plug-and-play manner, while Django is opinionated, making most decisions for the developer.

## Summary

Flask is a micro framework that ships with minimal dependencies. It offers features like debugging servers, routing, templates, and error handling, and can be extended using community extensions. Flask can be installed as a Python package, and it differs from Django, a full-stack framework.

# Basic Application and Routes in Flask

## Objectives
- Create and run a Flask application with basic routes in place.
- Return JSON response from the server to clients.
- Describe various configuration options available in Flask.

## Setting Up Flask

1. Install Flask
2. Create a Python file as your server (e.g., `app.py`).
3. Import Flask class from Flask module.
4. Instantiate an object of the Flask class as your app.

```python
from flask import Flask
app = Flask(__name__)
```

## Adding Routes

- Use `@app.route()` decorator to define a route. 

```python
@app.route('/')
def hello_world():
    return '<b>my first Flask application in action!</b>'
```

## Running the Application

- Set up environment variables:
  - `FLASK_APP`: the name of the main server file.
  - `FLASK_ENV`: define the development or production environment.

```bash
export FLASK_APP=app.py
export FLASK_ENV=development
```

- Run the application using `flask run`.
	- By default on port 5000

## Returning JSON

1. Return a serializable object, like a dictionary or a list.
2. Use the `jsonify()` method provided by Flask.

```python
from flask import jsonify

@app.route('/json')
def json_return():
    return jsonify(message="JSON response", status=True)
```

## Flask Configurations

- Flask provides several configuration options including:
  - `ENV`: Indicates the running environment, production or development.
  - `DEBUG`: Enables the debug mode.
  - `TESTING`: Enables the testing mode.
  - `SECRET_KEY`: Used to sign the session cookie.
  - `SESSION_COOKIE_NAME`: The name of the session cookie.
  - `SERVER_NAME`: Binds the host and port.
  - `JSONIFY`: Defaults to 'application/JSON'.

- Configuration options can be provided to Flask in different ways:
  - Through environment variables.
  - Directly into the `app.config` object.
  - From a separate JSON file using the `from_file` method provided by the config object.

## Application Structure

- Main source code: module directory.
- Configurations: separate configuration file.
- Static assets (images, JavaScript, CSS): static directory.
- Dynamic content: template directory.
- Test files: test directory.
- Virtual environment: for installing the right version of dependencies.

## Key Takeaways

- Create a server by instantiating the Flask class.
- Use the `@app.route()` decorator to create URL handlers.
- Return string messages or use the `jsonify()` method to return JSON objects.
- Set application configuration from Environment variables, Python files, or the `app.config` object directly.


# Request and Response Objects in Flask

## Flask Request Object

- Defined by the path using the `@app.route` decorator.
- Defaults to the GET method.
- Can control HTTP methods the path responds to by passing in a `methods` argument.
- Contains the following information:
  - Server's address (host, port).
  - Headers sent with the request.
  - URL requested by the client.
  - `access_route` lists all IP addresses for requests that are forwarded multiple times.
  - `full_path` includes the complete path of the request, including any query string.
  - `is_secure` is true if the request uses HTTPS or WSS protocol.
  - `is_JSON` is true if the request contains JSON data.
  - Cookies dictionary contains any cookies sent with the request.
  
```python
from flask import Flask, request

@app.route('/health', methods=['GET', 'POST'])
def health_check():
    if request.method == 'GET':
        # process GET request
    elif request.method == 'POST':
        # process POST request
```

## Accessing Data from the Request Object

- `get_data()` accesses data from the POST request as bytes.
- `get_JSON()` gets data parsed as JSON from the post request.
- `args` gives query parameters as a dictionary.
- `JSON` parses the data into a dictionary.
- `files` provides user uploaded files.
- `form` contains all values posted in a form submission.
- `values` combines the args data with the form data.

```python
data = request.get_data()
json_data = request.get_JSON()
```

## Extracting Specific Values from Request Data

- Return types are either a `MultiDict`, `ImmutableMultiDict`, or a `CombinedMultiDict`.
- Values can be extracted using indexing or the GET method.

```python
course = request.args['course']
rating = request.args.get('rating')
```

## Flask Response Object

- Status_code indicates the success or failure of the request.
- Headers give more information about the response.
- `content_type` shows the media type of the requested resource.
- `content_length` is the size of the response message body.
- `content_encoding` indicates any encoding applied to the response.
- `mime-type` sets the media type of the response.
- `expires` contains the date or time after which the response is considered expired.

```python
from flask import make_response

response = make_response('Hello World!', 200)
response.mimetype = "text/plain"
```

## Response Object Methods

- `set_cookie` sets a browser cookie on the client.
- `delete_cookie` deletes a cookie on the client.
- `make_response` creates a custom response.
- `redirect` returns a 302 status-code and redirects the client to another URL.
- `abort` returns a response with an error condition.

```python
from flask import redirect

@app.route('/')
def home():
    return redirect('/new-url')
```
# Dynamic Routes in Flask

## Calling an External API in Flask

- The Python requests library can be used for calling an external API.
- The returned JSON from the external API can be directly returned to your client or processed before sending.

```python
from flask import Flask, request
import requests

app = Flask(__name__)

@app.route('/')
def call_api():
    res = requests.get('https://openlibrary.org/api/authors/MichaelCrichton')
    if res.status_code == 200:
        return res.json()
    elif res.status_code == 404:
        return {'message': 'Something went wrong.'}, 404
    else:
        return {'message': 'Server error.'}, 500
```

## Passing Parameters to Routes in Flask

- Flask allows passing some resource-id as part of the request URL (dynamic routing).
- Flask also allows to set the parameter type for validation of incoming requests.

```python
@app.route('/books/<isbn>')
def get_book(isbn):
    res = requests.get(f'https://openlibrary.org/api/books/{isbn}')
    # Handle the response as per the requirement
```

## Parameter Types in Flask

- Flask supports several parameter types in its routing mechanism.
  - `string`: accepts any text without a slash.
  - `int`: accepts positive integers.
  - `float`: accepts positive floating-point values.
  - `path`: similar to `string` but accepts slashes.
  - `uuid`: accepts UUID strings.

```python
@app.route('/network/<uuid:net_id>')
def get_network(net_id):
    # Process the net_id
    return {'message': 'Success'}, 200
```

# Error Handling in Flask

## HTTP Status Codes

HTTP responses contain a three-digit status code indicating different types of outcomes:
- 100-199: Informational
- 200-299: Success
- 300-399: Redirection
- 400-499: Client Errors
- 500-599: Server Errors

Examples:
- 200: OK
- 201: Created
- 202: Accepted (often used for batch operations)
- 204: No Content (successful operation, but nothing to return)
- 400: Bad Request
- 401: Unauthorized
- 403: Forbidden
- 404: Not Found
- 405: Method Not Allowed
- 500: Internal Server Error

## Error Handling in Flask

Flask allows sending status code along with response in a tuple or using `make_response()`. 

```python
from flask import Flask, make_response

app = Flask(__name__)

@app.route('/')
def home():
    return "my first application in action!", 200

@app.route('/make_response')
def home_response():
    res = make_response("my first application in action!")
    res.status_code = 200
    return res
```

## Returning Errors from API Endpoints

Flask automatically returns a 200 OK status when you return from the `@app.route` method. However, you can explicitly return different status codes based on your application logic.

```python
@app.route('/search')
def search_response():
    q = request.args.get('q')
    result = fetch_from_database(q)
    if result:
        return jsonify(result), 200
    else:
        return {'error': 'resource not found'}, 404
```

## Global Error Handlers

Flask allows defining error handlers at the application level to handle specific error codes.

```python
@app.errorhandler(404)
def not_found_error(error):
    return {'error': 'API not found'}, 404

@app.errorhandler(500)
def internal_error(error):
    return {'error': 'Something went wrong on the server.'}, 500
```

Summary:
- HTTP responses require a status code to indicate the outcome of the request.
- Flask implicitly returns a success code of 200 with the response, but you can provide different status codes explicitly.
- Flask allows defining application-level error handlers to manage errors uniformly across your application.