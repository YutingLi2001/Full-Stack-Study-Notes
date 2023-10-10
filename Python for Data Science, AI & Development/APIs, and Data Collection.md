# Simple APIs (Part 1)

## Introduction to API

- **API (Application Program Interface)** allows two pieces of software to communicate with each other.
- Just like a function, you only need to know the inputs and outputs.
- **Example**: Pandas is a set of software components, and you use its API to process the data.

### Pandas Example

1. **Creating an instance**: When you create a dictionary and then create a Pandas DataFrame object, this is an "instance."
2. **Communicating with the API**: Using the DataFrame methods like `head` or `mean`, the DataFrame communicates with the API.

## REST API

- **REST (Representational State Transfer) APIs** are used to interact with web services
- They have a set of Rules regarding:
	- Communication
	- Input or Request
	- Output or Response

## API terms

- **Client**: Your program.
- **Resource**: The web service the API communicates with.
- **Endpoint**: The location where the client finds the service.
- **Request**: Client sends this to the resource.
- **Response**: Resource sends this to the client.

1. Client finds the service via an endpoint.
2. The client send requests to the resource and the resource sends a response to the client

## Rest API over HTTP

- We tell the Rest API's what to do by sending a request
- The request is usually communicated via an HTTP message.
- The HTTP message usually contains a JSON file. 

### Example with PyCoinGecko

- **Use Case**: Crypto Currency data is ideal for an API as it's constantly updated.
- **Library**: Py-Coin-Gecko Python Client/Wrapper for the Coin Gecko API.
- **Steps**:
  1. Install and import the library.
  2. Create a client object.
  3. Use a function to request data (e.g., Bitcoin data in USD for the past 30 days).
  4. The response is a JSON expressed as a Python dictionary.
  5. Convert the nested list to a DataFrame and handle time data.

```python
from pycoingecko import CoinGeckoAPI
import pandas as pd

cg = CoinGeckoAPI()

# Requesting data
data = cg.get_coin_market_chart_by_id('bitcoin', 'usd', days=30)

# Selecting price
prices = data['prices']

# Converting to DataFrame
df = pd.DataFrame(prices, columns=['timestamp', 'price'])

# Converting timestamp
df['date'] = pd.to_datetime(df['timestamp'], unit='ms')

# Creating a candlestick plot
# ...
```

### Creating a Candlestick Plot

- **Group by date**: To find the minimum, maximum, first, and last price of each day.
- **Plotting**: Use Plotly to create the candlestick chart and plot it.


# Simple APIs (Part 2)

## Using Watson Language Translator API

- **API Call**: This usually involves sending a request to an API and receiving a response. In this case, the request may include an audio file or a piece of text.
- **POST Request**: Sending data (like an audio file) to an API.
- **GET Request**: Receiving data (like a transcribed text) from an API.
- **API Key**: A unique set of characters that the API uses to identify and authorize you. It is usually included in your first API call.
- **Endpoint**: The location of the API service on the internet.

## Transcribing Audio Files with Watson Text to Speech API

1. Sign up for an API key.
2. Download the audio file you want to transcribe.
3. Import `SpeechToTextV1` from `ibm_watson`.
4. Create a Speech to Text adapter object with your API key and endpoint.
5. Open the audio file in binary format.
6. Use the `recognize` method from the adapter object to send the audio file to the Watson Speech to Text service.
7. The transcribed text can be extracted from the response object.

```python
from ibm_watson import SpeechToTextV1
from ibm_cloud_sdk_core.authenticators import IAMAuthenticator

authenticator = IAMAuthenticator('your-api-key')
speech_to_text = SpeechToTextV1(authenticator=authenticator)

speech_to_text.set_service_url('your-service-endpoint')

with open('audiofile.wav', 'rb') as audio_file:
    response = speech_to_text.recognize(audio=audio_file, content_type='audio/wav')

recognized_text = response.result['results'][0]['alternatives'][0]['transcript']
```

## Translating Text with Watson Language Translator API

1. Import `LanguageTranslatorV3` from `ibm_watson`.
2. Create a Language Translator object with your API key and endpoint.
3. Use the `translate` method to translate the transcribed text.
4. Extract the translated text from the response object.

```python
from ibm_watson import LanguageTranslatorV3

authenticator = IAMAuthenticator('your-api-key')
language_translator = LanguageTranslatorV3(version='date-version', authenticator=authenticator)

language_translator.set_service_url('your-service-endpoint')

translation = language_translator.translate(text=recognized_text, model_id='en-es').get_result()
spanish_translation = translation['translations'][0]['translation']

# Translating back to English
back_translation = language_translator.translate(text=spanish_translation, model_id='es-en').get_result()
english_translation = back_translation['translations'][0]['translation']

# Translating to French
french_translation = language_translator.translate(text=recognized_text, model_id='en-fr').get_result()
french_text = french_translation['translations'][0]['translation']
```

# Understanding the HTTP Protocol: URL, Request, and Response

## HTTP Protocol

- HTTP is a protocol that allows the fetching of resources, such as HTML documents, images, and more from servers on the web. It's the foundation of any data exchange on the web and a protocol used by REST APIs.

- HTTP works as a request-response protocol between a client and a server. When you use a web page, your browser (the client) sends an HTTP request to the server where the page is hosted.

- The server then tries to find the desired resource (by default, "index.html"). If your request is successful, the server sends the object to the client in an HTTP response.

## Uniform Resource Locator (URL)

- A URL is a specific type of Uniform Resource Identifier (URI). It's the most popular way to find resources on the web. We can break the URL into three parts:
  1. **Scheme**: This is the protocol, for this lab it will always be "http://"
  2. **Internet address or Base URL**: This is used to find the location, e.g., "www.ibm.com" and "www.gitlab.com".
  3. **Route**: This is the location on the web server, for example: "/images/IDSNlogo.png".

## Request and Response

- An HTTP message consists of a start-line, headers, and a body. For example, in a GET request:
  - The start-line is "GET /index.html", where "GET" is the HTTP method, and "/index.html" is the requested resource.
  - The headers pass additional information with the HTTP request.
  - In a GET request, the body is usually empty.

- The response from the server contains the protocol version, a status code, and a descriptive phrase, e.g., "HTTP/1.0 200 OK". It also contains headers with additional information and the body which carries the requested resource.

- Status codes are grouped into five classes:
  - 1xx (Informational): The request was received, continuing process.
  - 2xx (Successful): The request was successfully received, understood, and accepted.
  - 3xx (Redirection): Further action needs to be taken in order to complete the request.
  - 4xx (Client Error): The request contains bad syntax or cannot be fulfilled.
  - 5xx (Server Error): The server failed to fulfill an apparently valid request.

## HTTP Methods

- HTTP methods define what action to be performed on the resource identified by the URL. Some of them are:
  - GET: Retrieves data from the server.
  - POST: Sends data to the server.
  - PUT: Updates a current resource with new data.
  - DELETE: Deletes a specified resource.


# Using the HTTP Protocol with Python's Requests Library

## The Requests Library in Python

- Requests is a popular Python library for making HTTP requests. It abstracts the complexities of making requests behind a beautiful, simple API so that you can focus on interacting with services and consuming data in your application.

- To import the Requests library in Python, you can simply use the following line of code:

```python
import requests
```

## Making a GET Request

- You can make a GET request to a website like `www.ibm.com` using the `get()` method in Requests:

```python
r = requests.get('http://www.ibm.com')
```

- You can check the status of the request using the `status_code` attribute:

```python
print(r.status_code)  # prints: 200
```

- You can also view the request headers and body. Since there's no body in a GET request, it will return `None`. 

- The `headers` attribute gives you the response headers which are stored as a Python dictionary. For example, you can get the date of the request or the content type:

```python
print(r.headers['Date'])  # prints the date of the request
print(r.headers['Content-Type'])  # prints the content type
```

- Since the content type is `text/html`, you can use the `text` attribute to display the HTML in the body. 

## Making a GET Request with Query Parameters

- You can also make a GET request with query parameters. This is especially useful when interacting with APIs. 

- To do this, you can include a dictionary of your query parameters and pass them into the `get()` method. This dictionary will then be incorporated into the URL.

```python
payload = {"name": "Joseph", "ID": "123"}
r = requests.get('http://httpbin.org/get', params=payload)
```

- This request will return a JSON response that you can format into a Python dictionary using the `json()` method:

```python
print(r.json())  # prints the JSON response as a Python dict
```

## Making a POST Request

- A POST request is used to send data to a server in the request body, unlike a GET request which includes data in the URL.

- You can send a POST request using the `post()` function. Just like in the GET request, you include a dictionary of your data and pass it into the `post()` method.

```python
payload = {"name": "Joseph", "ID": "123"}
r = requests.post('http://httpbin.org/post', data=payload)
```

- You'll notice that the URL does not contain the name-value pairs like in a GET request. Instead, the data is included in the body of the request.

- When you print the response of a POST request, you'll see that the data you sent is included in the response:

```python
print(r.json())  # prints the JSON response as a Python dict
```

# Introduction to Web Scraping with Python

## What is Web Scraping

- Web scraping is the process of automatically extracting information from a website, saving hours that would otherwise be spent manually copying and pasting information.

- We'll use Python and two modules: Requests and Beautiful Soup.

## BeautifulSoup Objects

- Beautiful Soup parses HTML and XML documents, representing them as a nested data structure which we can then navigate and search.

```python
from bs4 import BeautifulSoup

# Store the webpage HTML as a string in the variable HTML
html = "<html><head><title>Page Title</title></head><body><h3>Player Name</h3><p>Player Salary</p></body></html>"

# Parse the document
soup = BeautifulSoup(html, 'html.parser')
```

- The `tag` object corresponds to an HTML tag in the original document. If there's more than one tag with the same name, Beautiful Soup will select the first.

## Navigating the BeautifulSoup Object

- HTML tree representation
- You can access children of the tag or navigate up the tree using the `parent` attribute, or find siblings using the `next_sibling` attribute.
- Tags' attributes can be accessed like a dictionary, and their contents can be returned as a navigable string.

## The `find_all` Method

- This method scans through a tag's descendants and retrieves all that match your filters. 

```python
# Create a BeautifulSoup object
table = BeautifulSoup(html, 'html.parser')

# Apply find_all to the table with the tag <tr>
table_rows = table.find_all('tr')
```

- The result is a Python iterable (like a list), with each element being a `tag` object for `<tr>`. This corresponds to each row in the table, including headers.

- By iterating through the rows and finding all the table cells, we can extract data from each cell.

## Scraping a Webpage

- To scrape a webpage, we also need the Requests library. The `get` method from the requests library is used to download the webpage.

```python
import requests
from bs4 import BeautifulSoup

# Download the webpage
page = requests.get('https://example.com').text

# Create a BeautifulSoup object
soup = BeautifulSoup(page, 'html.parser')
```

- After creating the BeautifulSoup object, you can parse through the HTML page and scrape the required data.




# Working with Different File Formats in Python

## File Formats

- Files have extensions at the end of their names, like `example.csv`, `example.json`, or `example.xml`. These extensions inform us about the file's format.
- Different Python libraries can help us interact with these different formats.

## Pandas for CSV Files

- The first Python library to become familiar with is `pandas`. By importing it, we can easily read different file types.
```python
import pandas as pd

# Assign the file to a variable
filename = 'example.csv'

# Use pandas to read the CSV file
data = pd.read_csv(filename)
print(data)
```
- If the file doesn't contain headers, the first line of data will be used as headers. We can avoid this by specifying column names using a dataframe.

```python
# Add column headers
data.columns = ['column1', 'column2', ...]
print(data)
```

## JSON Files

- JSON files contain data in a language-independent format, similar to a Python dictionary. We use the `json` library to interact with these files.
```python
import json

# Open and load the JSON file
with open('example.json', 'r') as file:
    data = json.load(file)
print(data)
```

## XML Files

- To parse XML files, we import the `xml` library and use its `etree` module. `pandas` doesn't directly support XML files, but we can collect the necessary data and append it to a dataframe.
```python
import xml.etree.ElementTree as ET
import pandas as pd

# Parse the XML file
tree = ET.parse('example.xml')
root = tree.getroot()

# Add column headers and assign them to the dataframe
data = pd.DataFrame(columns=['column1', 'column2', ...])

# Loop through the document to collect data
for elem in root:
    column1 = elem.find('column1').text
    column2 = elem.find('column2').text
    ...

    # Append data to the dataframe
    data = data.append(pd.Series([column1, column2, ...], index=data.columns), ignore_index=True)

print(data)
```


### Flask Overview
- **Definition**: Flask is a micro framework for creating web applications quickly with Python.
- **Features**: Enables CRUD (Create, Read, Update, Delete) operations through Post, Put, Get, Update, and Delete requests.
- **CRUD Details**:
  - **Create**: Use Post and Put. Post creates data every request, while Put creates on first request then updates.
  - **Read**: Use Get request to read data from the server.
  - **Update**: Update requests to modify existing data.
  - **Delete**: Delete requests to remove data.
- **Installation**: Install Flask using `pip install Flask`.

### Basic Structure of a Flask App
1. **Install Flask**: `pip install Flask`.
2. **Import Flask**: 
   ```python
   from flask import Flask
   ```
3. **Create Flask Object**:
   ```python
   app = Flask("My first Application")
   ```
4. **Define Route and Method**:
   ```python
   @app.route('/')
   ```
   Default request type is Get.
5. **Define Method for Route**:
   ```python
   def hello():
       return 'Hello World!'
   ```
6. **Run Application**:
   ```python
   if __name__ == '__main__':
       app.run(debug=True)
   ```
7. **Access Application**: Open browser and connect to 127.0.0.1 at port 5000.

### Templates in Flask
- **Static**: Served as-is from `static` directory.
- **Dynamic**: Pages filled dynamically for each request.
- **Importing Flask, render_template, and request**:
  ```python
  from flask import Flask, render_template, request
  ```

### Example Flask App
- **Static HTML Page**:
  ```python
  @app.route('/sample')
  def getSampleHtml():
      return render_template('sample.html')
  ```
- **Dynamic URL Parameter**:
  ```python
  @app.route('/user/<username>', methods=['GET'])
  ```
  Renders page with username from URL.
- **Request Parameter**:
  Renders page with username passed as a request.

### Conclusion
- Flask enables quick web application creation, supporting CRUD operations.
- You can render both static and dynamic templates with Flask.
- The application is accessible through IP and port, often 127.0.0.1:5000.


### Decorators in Flask

#### Objectives
- Understand what are decorators
- Understand the two kinds of decorators in a Python application
- When and how to use decorators

#### What are Decorators
- Decorators help in annotating the methods and defining what a particular method is meant for. They're different from comments and are used by the interpreter while running the code.

#### Method Decorators
- Help reduce redundant code, for example, when output needs to be in a specific format like JSON for all methods.

```python
def jsonify_decorator(function):
    def modifyOutput():
        return {"output":function()}
    return modifyOutput

@jsonify_decorator
def hello():
    return 'hello world'

@jsonify_decorator
def add():
    num1 = input("Enter a number - ")
    num2 = input("Enter another number - ")
    return int(num1)+int(num2)

print(hello())
print(add())
```
- This decorator (`jsonify_decorator`) modifies the output of the `hello()` and `add()` functions to return JSON formatted output.

#### Route Decorators
- Define endpoints for a Flask web application.
- Assign URLs to functions in the application.

```python
@app.route("/")
def home():
    return "Hello World!"
```
- This decorator (`@app.route("/")`) assigns the `home()` function to the root URL ("/") of the application.

- Multiple routes can be handled with a single function:

```python
@app.route("/")
@app.route("/home")
@app.route("/index")
def home():
    return "Hello World!"
```
- These decorators assign the `home()` function to three different URLs ("/", "/home", "/index").

- Route decorators can also accept HTTP method types as a second parameter.
- Route decorators can be more specific to handle cases like user details:

```python
@app.route("/userdetails/<userid>")
def getUserDetails(userid):
    return "User Details for  "+userid
```
- This decorator (`@app.route("/userdetails/<userid>")`) dynamically creates routes for each user's details based on the user id.

### Conclusion
- Decorators in Python, especially with Flask, can greatly help with code organization and efficiency. They are useful for both method and route handling.



# CRUD Operations using Additional Features in Flask

## Overview
CRUD stands for Create, Read, Update, and Delete. They are fundamental operations in any application with a database. In this context, Flask is used to manage these operations using different HTTP methods like GET and POST.

## Objectives
- Use `flask.request.form` to access form data in POST requests
- Redirect users using Flask's `redirect` function
- Generate dynamic URLs with `url_for`
- Handle various HTTP request types
- Implement CRUD operations in a Flask app

## Key Concepts

### Accessing Form Data with `flask.request.form`

This is how to access form data submitted via a POST request:

```python
from flask import request

@app.route('/login', methods=['POST'])
def login():
    username = request.form['username']
    password = request.form['password']
    # process login here
```

### Redirecting to a URL with `flask.redirect`

Redirect users to different pages using the `redirect` function:

```python
from flask import redirect

@app.route('/admin')
def admin():
    return redirect('/login')
```

### Generating Dynamic URLs with `flask.url_for`

Dynamically generate URLs for a given endpoint with `url_for`:

```python
from flask import url_for

@app.route('/admin')
def admin():
    return redirect(url_for('login'))

@app.route('/login')
def login():
    return "<Login Page>"
```

### Handling Different HTTP Request Types

Define routes that handle different types of HTTP requests:

```python
@app.route('/data', methods=['GET', 'POST'])
def data():
    if request.method == 'POST':
        # process POST request
    if request.method == 'GET':
        # process GET request
```

### CRUD Operations in Flask

- **Create Operation**: Data creation involves presenting a form to the user. In Flask, this data is accessed using `flask.request.form`.

- **Read Operation**: Reading data involves accessing the data and presenting it to the user. You can pass specific IDs as an argument to the function to access specific entries.

- **Update Operation**: Updating data involves accessing specific entries (like the Read operation) and giving new data (like the Create operation). 

- **Delete Operation**: Deleting data involves removing a record based on its ID. The operation requires the ID to be passed as an argument to the function. 

These operations are implemented in the following way:

```python
# Create
@app.route('/create', methods=['GET', 'POST'])
def create():
    if request.method == 'POST':
        # Access form data
        name = request.form['name']
        # Create a new record with the name
        record = create_new_record(name)
        return redirect(url_for('read', id=record.id))
    return render_template('create.html')

# Read
@app.route('/read/<int:id>', methods=['GET'])
def read(id):
    record = get_record(id)
    return render_template('read.html', record=record)

# Update
@app.route('/update/<int:id>', methods=['GET', 'POST'])
def update(id):
    if request.method == 'POST':
        name = request.form['name']
        update_record(id, name)
        return redirect(url_for('read', id=id))
    record = get_record(id)
    return render_template('update.html', record=record)

# Delete
@app.route('/delete/<int:id>', methods=['POST'])
def delete(id):
    delete_record(id)
    return redirect(url_for('home'))
```

