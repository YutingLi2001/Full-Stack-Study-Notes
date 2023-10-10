# Django's Model View Template (MVT) Pattern

## Learning Objectives
- Understand the Model-View-Controller (MVC) pattern.
- Familiarize yourself with Django's Model View Template (MVT) pattern.

## Key Points

### MVC Design Pattern
- **Model**: Responsible for data access and manipulation. It interfaces with databases using SQL, ORM, or business logic.
- **View**: Handles data presentation in various formats, like visual webpage elements, mobile app UI, or JSON/XML.
- **Controller**: Acts as a coordinator between Model and View. It routes requests, processes inputs, handles data CRUD operations from Model, and updates the View.

### Django's MVT Pattern
- In Django, there isn't a distinct Controller component. Instead, the Django server itself takes on this role.
- **Django Model**: Manages both data modeling and business logic. It maps classes to database tables and enables CRUD operations on objects.
- **Django View**: Determines the data to be presented but not how it is displayed. Usually, the View delegates presentation details to a Template.
- **Django Template**: Describes how data is presented, blending static HTML elements with Python code to generate dynamic web pages.

### Workflow of Django MVT
1. A client sends a request to the Django server.
2. The server routes the request to the appropriate view based on Django's URL configuration.
3. The View, often a Python function, processes the request, interacts with the Model if necessary, and generates a web response.
4. The response could be HTML content, a redirect, error messages, or any other web response type.
5. If dynamic web pages are needed, Django utilizes a template to generate them, which are then rendered on the user's browser.

## Conclusion
In this lesson:
- You learned how the MVC design pattern segregates application logic into Model, View, and Controller.
- Django implements a variation of MVC, known as the MVT pattern, where the framework itself acts as the Controller.
- The Django Model handles data and business logic, the View determines which data to present, and the Template specifies how the data should be displayed.

# Create a Django App

## Learning Objectives
- Understand Django web app structure.
- Create and run a basic Django web application.

## Django Development Process
1. **Create a Django Project**: Acts as a container for Django apps and settings.
2. **Create and Add Django Apps**: To the project.
3. **Core Development**:
   - Create Django models for data modeling.
   - Create views to present data to UI.
   - Map request URLs to views.
4. **UI Design and Build**.
5. **Testing**: Conduct unit or system tests.
6. **Add-ons Integration**: Integrate admin sites or third-party libraries for production.
7. **Deployment & Monitoring**: Deploy on a web server and monitor status.

## Key Project Files
- `manage.py`: Command-line interface for interacting with the Django project.
- `settings.py`: Holds settings and configurations for the project.
- `urls.py`: Contains URL and routing definitions for the app.

## Creating Your First App
1. From the project directory, run `python manage.py startapp onlinecourse` to create a new app named "onlinecourse".
2. This generates the app structure with key files:
   - `admin.py`: For creating and customizing admin sites.
   - `models.py`: Contains data models and ORM.
   - `views.py`: Holds view functions and classes for creating views.
   - `urls.py`: Contains URL declarations and routing for the app.
   - `app.py`: Contains the application configuration class.

## Linking App to Project
- Add 'onlinecourse.apps.OnlinecourseConfig' to the `INSTALLED_APPS` list in the `settings.py` file of the project.

## Database Setup
- Configure databases in the `DATABASES` dictionary in `mysite/settings.py`.

## Defining and Migrating Models
- Define models in `models.py`.
- Run migrations with `python manage.py makemigrations onlinecourse` and `python manage.py migrate`.

## Creating a Simple View
1. Open `onlinecourse/views.py` and add a `course_list` view function.
2. Create an HTML template and insert dynamic content.
3. Return completed HTML as `HttpResponse`.

## URL Configuration
- Create `urls.py` under `onlinecourse/` folder.
- Add `path` objects pointing to created views.
- Reference the app’s URLConf in the project’s `urls.py` file.

## Running the App
- Start the server using `python manage.py runserver`.
- Access the app through your web browser.

## Summary
- You learned about the structure and key files of a Django project and app.
- You've seen the process of creating and running a simple Django app, from defining models to creating views and configuring URLs.

# Django Admin

## Learning Objectives
- Build and manage a Django Admin site for an online course application.
- Customize the Admin site interface.

## Overview
- **Models in Online Course App**: The application consists of various entities like Course, Lessons, Questions, Choices, User, Learner, Instructor, Course Enrollment, and Question Submission.
- **Django Admin for Content Management**: Django offers a built-in Admin site facilitating content management without requiring extensive coding.

## Building Django Admin Site
1. **Create an Admin User**: Run `python manage.py createsuperuser` and follow prompts to set credentials.
2. **Start Django Server and Access Admin Site**: Login using created credentials.
3. **Register Models for Management**: In `onlinecourse/admin.py`, add `admin.site.register(Course)` and `admin.site.register(Instructor)` to make Courses and Instructors manageable.
   - Django generates UI elements based on model fields.
   - Customize which fields to display and manage on the Admin site.

## Customizing Admin Site Interface
- **Field Selection and Order**: Create a model admin class and specify a list of fields to be included in the Admin site. This controls the order and selection of fields displayed.
   - Example: For `Course` model, create `CourseAdmin` class and define fields to be displayed.
- **Adding Multiple Related Models**: Admin.StackedInline or Admin.TabularInline allows adding related models within the same form. This facilitates adding multiple related items efficiently.
   - Example: Define `LessonInline` object and include it within `CourseAdmin` to enable adding lessons within the course creation form.
- **Customizing List Displays**: Define which fields are displayed when listing multiple items by using `list_display`.
   - Example: For a course list, display only course name and publication date.
- **Enabling Search and Filter Functions**: Implement search and filter functionalities by defining `search_fields` and `list_filter` for ease of navigation and management.

## Summary
- The Django Admin site is a powerful tool for content management, significantly easing the process of handling various entities and their relationships within an application.
- With customization options available, the Admin interface can be tailored to suit the needs of content managers and administrators for efficient and user-friendly content management.

# Django Views

## Learning Objectives
- Understand the concept of a Django view.
- Create a basic function-based Django view.

## Introduction
- A view is crucial in handling Web requests (HTTP GET, POST, DELETE, UPDATE) and returning appropriate Web responses.
- Responses can be various data formats: string, JSON/XML file, HTML page, or an error status.

## Creating Function-Based View
- **Function Basics**: A view is a function that accepts arguments and returns a value.
- **Request Object**: 
  - The primary argument is an HTTP request object, which is read-only.
  - This object contains metadata: method, header, parameters, or payload.
- **Processing Logic**: 
  - The view processes the request using business logic (e.g., querying a database and populating an HTML template).
  - For instance, a view might retrieve a course record and insert its name into an HTML template.
- **HttpResponse Object**: After processing, the view returns an HttpResponse object to the UI.
  - You can pass content like HTML pages, strings, or bytestrings to the HttpResponse constructor.

## Mapping URL to View
- After creating a view, associate it with a URL pattern.
- Open the URL configuration file (`urls.py` in the app’s root folder).
- Add a `path` object with:
  - `route` (the URL pattern).
  - The view function as the second argument.
  - An optional name for reference and an app_name for namespacing.
- Example: For an app named “onlinecourse” with a view named ‘course’, refer to its URL pattern using `onlinecourse:course`.

## Response Status Codes
- Every HttpResponse is accompanied by a status code.
  - `200 OK`: The request was successful.
  - Error codes (e.g., `404 Not Found`): Indicate issues with the request or on the server.
- To send an error, include the error status and content in the HttpResponse constructor.
- Customize the content sent with both successful and error status codes (e.g., success/error messages or pages).

## Summary
- Django views are essential for processing HTTP requests and returning responses.
- You've learned the basics of creating a function-based view, from processing the request to sending an appropriate response.
- Ensure to map your views to URLs and handle status codes appropriately for successful and error scenarios.

# Django Template

## Learning Objectives
- Understand the role and structure of Django templates.
- Combine Django views with templates to display dynamic HTML pages.

## Introduction
- Django templates are the bridge between static HTML and dynamic data.
- They combine static HTML with Django template tags and variables.
- The end goal is to generate HTML pages dynamically, which browsers can render.

## Creating Templates in Django
- A Django template is an HTML file infused with Django-specific tags and variables.
- To create a template for the `onlinecourse` app:
  - Make a directory named `templates` in the app's root folder.
  - Inside `templates`, create another directory with the app's name (`onlinecourse`) for namespacing.
  - Inside this namespaced directory, you can create your template file (e.g., `course_list.html`).

## Rendering Templates
- Templates need data to render dynamically, this data comes from views.
- Views fetch data, generate a context (a dictionary-like object), and push it to the template.
- The template renders by replacing variables from the context and executing tags.
- For example: 
  - Use the `if-else` tag to conditionally display content.
  - Use the `for` tag to iterate over lists or querysets from the context.
- To use variables in the template, just enclose them in `{{ }}`.
- You can access attributes of objects using dot notation (`course.name`).

## Using the `render` Method
- Instead of returning `HttpResponse` directly, views use the `render` method.
- `render` combines the template with the context and returns an `HttpResponse` with the rendered text.
- `render` takes three arguments: 
  - The HTTP request.
  - The path to the template file.
  - The context containing the data.

## Beautifying with CSS
- To enhance and style our web pages, integrate static resources like CSS.
- Load static resources using the `load static` tag.
- Use the `static` tag to generate absolute URLs for static files.
- Apply the CSS classes in your template tags to style the content.
- Example: The background can be set to light gray, course descriptions to green, separated by horizontal lines.

## Summary
- Django templates are powerful tools for presenting dynamic data in a structured and styled manner.
- Templates and views work hand-in-hand: views provide data, templates define presentation.
- Enhance the user experience further with static resources like CSS.

