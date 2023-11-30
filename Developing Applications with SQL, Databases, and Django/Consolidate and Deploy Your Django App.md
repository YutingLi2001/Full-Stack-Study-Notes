# Class-based and Generic Class Views

## Learning Objectives
- Understand how to create class-based and generic class-based views.
- Distinguish between function-based views and class-based views, weighing their pros and cons.

## Introduction to Class-Based Views
- Class-Based Views (CBVs) were introduced to improve extensibility and reusability in Django views.
- While function-based views solve specific problems with request parameters and response generation, CBVs offer more structure and flexibility.
- Both function-based and class-based views are essentially callables or functions.

## Creating a Class-Based View
1. **Define a Class:** Subclass from Django’s `View` base class.
2. **Implement Methods:** Use predefined methods (like `get` or `post`) to handle respective HTTP requests, and add your logic.
3. **Map URL:** Similar to function-based views but use the `as_view()` method for the view argument in URL mapping.

## Workflow of Class-Based View
- `as_view()` is a class method of Django’s `View` class that returns a function.
- When this function is called, it passes the request to the `dispatch` method.
- `dispatch` then routes to the appropriate HTTP method handler (GET, POST, etc.).

## Generic Class-Based Views
- Django offers built-in generic views to facilitate common tasks.
- With minimal code, developers can leverage these to perform routine operations:
  - `ListView`: Displays a list of objects.
  - `DetailView`: Shows details of a specific object.
  - `FormView`: Handles forms.
  - A set of Date views for date-based data.

## Example of Using Generic Class-Based View
- For displaying details of a course:
  - Define `CourseView` extending `DetailView`.
  - Specify the model (Course) and provide the path to the HTML template.
  - Generic views automate tasks like object retrieval and HTML page population.

## Pros and Cons: Function-Based Views
- **Pros:**
  - Simple and straightforward to write and understand.
  - Explicit logic without the need for extra structures or designs.
  - Ideal for specific, non-reusable functions.
- **Cons:**
  - Difficult to extend or reuse.
  - Relies on conditional statements to handle HTTP requests, potentially complicating the code.

## Pros and Cons: Class-Based Views
- **Pros:**
  - Highly reusable and extendable.
  - Request handling using class methods.
  - Allows use of generic views for common tasks.
- **Cons:**
  - Code may be harder to read due to the inheritance of the View base class.
  - Implicit code is hidden, necessitating source code review to understand view implementation.

## Summary
- Class-based views offer a structured, extendable, and reusable approach to building views in Django.
- Generic class-based views further simplify common tasks with minimal code.
- Choose between function-based and class-based views based on your project's needs, considering their respective advantages and limitations.

# Django Authentication System

## Learning Objectives
* Understand the concepts of authentication and authorization.
* Use Django User objects for authentication and authorization.

## Authentication and Authorization
* **Authentication**: The process of verifying user identities, typically through credentials like username and password. Advanced methods include one-time passcodes, single sign-on (SSO), biometrics (face recognition, fingerprints).
* **Authorization**: After authentication, it checks users' access permissions for resources, e.g., viewing content. System admins define roles/groups with specific permissions and assign users to these groups.

## The User Model
* Provides basic user information (username, password, email).
* Used for authentication and works in tandem with groups and permissions for authorization.
* Can be extended for application-specific users, like instructors or learners.

## Authenticating a User
1. **Webpage Template**: Create a webpage template to receive user credentials.
2. **Login Form**: Implement inputs for username and password, submitted via a POST request to the `onlinecourse` login view.
3. **Login View**: 
    * Retrieve username and password from the request object.
    * Use Django's `authenticate` method to verify credentials against the database.
    * If credentials are valid, use the `login` method to log in the user and redirect to the index view.

## User Sessions
* After login, Django creates a session with a unique ID and associates user information with it.
* Session stores data for users, allowing continuous interaction without needing to log in multiple times.
* Session ID is stored as a COOKIE in the browser.

## Logging Out
* To log out a user, simply call the `logout` method with the HTTP request object.

## User Registration
* Similar process to login but directs to a registration view.
* Registration view retrieves credentials, creates a new user using the `create_user` method, logs in the user, and redirects to the index page.

## Authorization Models
* Django’s authorization is managed mainly by three models: User, Permission, and Group.
    * **User**: Used for authentication.
    * **Permission**: Defines access types to various objects.
    * **Group**: Manages users with similar permissions.
* Permissions can be assigned at the model level, with defaults being View, Add, Change, and Delete.
* Groups allow for easy management of users with similar permissions, e.g., Instructors can add, change, delete, and view courses, while Learners can only view.

## Summary
* Authentication validates user identities, while authorization checks access permissions post-authentication.
* Django’s User model is pivotal for both processes, working alongside Permission and Group models for efficient authorization management.
* This tutorial covered user registration, login, session management, and permission and group management, providing a foundation for implementing robust authentication and authorization in Django apps.

# Bootstrap

## Introduction to Bootstrap
- Bootstrap is a free and open-source front-end framework.
- It provides well-designed HTML and CSS templates for faster web development.
- With Bootstrap, developers can easily create stylized and interactive web pages.

## Integrating Bootstrap into Django
1. **Simple Integration**: Add a link to the latest Bootstrap version (hosted by CDN networks like MaxCDN) in the head element of your HTML template. This allows you to use Bootstrap's CSS classes without needing to download anything.

## Designing Layouts with Bootstrap
- **Navigation Bar (Navbar)**
  - The navbar is a responsive header that includes navigational links, forms, buttons, or text.
  - Use the `navbar` class, with additional classes to customize its appearance and behavior.
  - Add items like links or buttons using the `ul` element with the `navbar-nav` class, and `li` items with the `nav-item` class.
  
- **Authentication Form in Navbar**
  - Create an inline form where all elements are in line and left-aligned.
  - Add input elements for receiving username and password, styled using the `form-control` class.
  - Include a submission button styled with `btn` and `btn-primary` classes, and a sign-up link styled with `btn` and `btn-link` classes.

- **Main Content: Course Cards**
  - Enclose the page main content in a `div` element with the `container` class.
  - Create a `div` styled with `card-deck` class to arrange course cards.
  - Each course card includes an image, card body with card title for course name, and `card-text` for course description.

- **Data Tables with Bootstrap**
  - Bootstrap also supports styling for tables.
  - Use the `table` class for basic styling. Define table headers with `thead` and table data with `tbody`.

## Conclusion
In this tutorial, you learned how to integrate Bootstrap into your Django templates. This allows you to leverage Bootstrap's navigation bars, forms, containers, cards, card decks, and tables for a responsive and well-designed web application. These components significantly speed up the process of developing and styling your Django web pages.


# Django Static Files

## Learning Objectives
After this video, viewers will understand:
- How Django manages static files, including CSS and media files.
- Combining Django views, templates, and static files to craft dynamic HTML pages.

## Managing Static Files in Django
- Static files are essential components, such as HTML templates, images, CSS files, etc.
- Create specific folders for each type of static file, and further organize them with subfolders named after the app (e.g., `onlinecourse`).
- The subfolder mechanism ensures namespace uniqueness for static files across multiple apps in a Django project.

### App-Specific and External Static Files
- Each app within a Django project can have its set of static files stored in a `static` folder at the app's root level.
- For external static files not tied to a specific app, define directories in `STATICFILES_DIRS` within the `settings.py` file.

### Static File Finders
- Django uses `STATICFILES_FINDERS` (e.g., `AppDirectoriesFinder` and `FileSystemFinder`) to locate and serve static files efficiently.

### Deployment Considerations
- For ease of deployment, you might want to consolidate all static files into a single directory.
- Django’s `staticfiles` app (installed by default) helps collect all static files into a specified directory.
  
## Preparing for Deployment
1. **Set `STATIC_ROOT`**: An absolute path serving as the root location for static files.
2. **Define `STATIC_URL`**: A URL prefix for static files.
3. **Use `collectstatic` Command**: This command collects all static files into the `STATIC_ROOT` directory, organizing them for deployment.
   - `findstatic` can help locate paths containing static files.

## Example File Structure
- After running `collectstatic`, you'll have an organized file structure under `STATIC_ROOT`, with first-level folders named after apps and subfolders for different static file types.
- During deployment, having all files under `STATIC_ROOT` simplifies the task for the web server to locate and serve these files.

## Serving Static Files
- Files under `STATIC_ROOT` are served either locally (by the Django development server) or remotely (by a dedicated web server).
- Access these files via URLs composed of the host and domain name, `STATIC_URL` (a defined prefix like `/static/`), and the file path in `STATIC_ROOT` (e.g., `/onlinecourse/course.css`).

## Conclusion
In this session, you've learned how Django handles static files both in development and production environments, providing a systematic approach to organizing, serving, and deploying these essential web components.

# Deploy Your Django Apps

## Learning Objectives
After watching this video, you will be able to:
- Deploy Django apps on web servers and the cloud.
- Understand best practices for making Django apps production-ready for the cloud.

## Deployment Overview
- **Development Server**: Django’s `runserver` command starts a minimal server for development and testing.
- **Web Servers**: For production, deploy Django apps on web servers like Apache, HTTP, or Nginx.

### Web Server Gateway Interface (WSGI)
- **Role**: Primary standard for communication between web servers and Python applications.
- **Supports**: Synchronous code only.
- **Configuration**: `wsgi.py` file in Django projects contains an application callable used by WSGI servers.
- **Popular WSGI Servers**: Gunicorn, uWSGI, Apache with mod_wsgi.

### Asynchronous Server Gateway Interface (ASGI)
- **Difference from WSGI**: Supports asynchronous code.
- **Configuration**: `asgi.py` file contains an application callable for ASGI servers.
- **Popular ASGI Servers**: Daphne, Hypercorn, Uvicorn.

## Cloud Deployment Options
1. **Virtual Machine (VM) Deployment**: 
   - Use a VM from a cloud provider and install necessary OS and software manually.
   - Requires manual configuration and deployment.
2. **Platform-as-a-Service (PaaS) Deployment**:
   - Platforms like Heroku streamline the deployment process.
   - Push code to a Git repository and let the platform handle deployment.
3. **Containerization Deployment**:
   - Package Django apps and dependencies in Docker containers.
   - Deploy using container orchestration tools like Kubernetes.

## Cloud Database Options
- Django supports PostgreSQL, MariaDB, MySQL, Oracle, and SQLite.
- Databases can be self-managed or use Database-as-a-Service from cloud providers.

## Best Practices for Cloud-Ready Django Apps
1. **Use Production Database**: Opt for robust and scalable databases like PostgreSQL or MySQL, avoiding SQLite in production.
2. **Secure Database Credentials**: Store sensitive information in environment variables, not in code.
3. **Implement HTTPS**: Secure communication between the server and clients.
4. **Serve Static and Media Files Efficiently**: Utilize cloud storage or CDNs for efficient delivery.
5. **Implement Load Balancing**: Distribute traffic across multiple app instances for performance and high availability.
6. **Design for Horizontal Scaling**: Add more instances or containers as traffic increases.
7. **Set Up Monitoring and Logging**: Implement services to track and diagnose issues efficiently.

## Conclusion
In this video, you’ve learned about deploying Django apps using various methods, choosing the right databases, and following best practices to ensure your applications are secure, scalable, and ready for the cloud.

# ==Module 4 Summary: Consolidate and Deploy Your Django App==

Congratulations! You have completed this module. At this point in the course, you know:

- Both function-based and class-based views are Python functions.
    
- When you build a class-based view, you define a class subclassing the Django View base class. Then you access some standard methods such as Get or Post. Next, you implement your logic to handle HTTP requests.
    
- To speed up development and solve common tasks, Django provides some built-in view classes called generic-based views for developers to reuse.
    
- Authentication is validating users’ identities using credentials such as username and password.
    
- After users are authenticated, authorization will check the users’ access permissions for resources such as databases.
    
- In Django, a user model is created to handle authentication and to work with other models, such as groups and permissions, to handle authorization.
    
- Developers can extend the User model to define application-specific users, such as instructors or learners inherited from the User model.
    
- Bootstrap, a free web front-end framework, facilitates web app development.
    
- Bootstrap provides many HTML and CSS templates to simplify Django template development.
    
- If you want to use Bootstrap CSS style classes without downloading Bootstrap, add a link to the latest Bootstrap version into the head element of your HTML template.
    
- To add static files to your apps, you first create folders for different static files, such as HTML templates, images, or CSS files.
    
- Under each folder to hold static files, you create a subfolder using the same app name. This creates name spacing to uniquely refer to static files that use the same name across multiple apps in a Django project. 
    
- Django provides a set of STACFILES_FINDERS for locating the static files in an app. It also provides a staticfiles app to collect all static files in a single directory when an app is deployed.
    
- To deploy reliable, scalable, and maintainable Django apps, you need to deploy them on web servers. 
    
- Since most web servers are not written in Python, Django apps need extra interfaces to talk to web servers.
    
- The Web Server Gateway Interface, or WSGI, is the main Python standard for communicating between Web servers and applications.
    
- The Django app supports the Asynchronous Server Gateway Interface, another web server interface.
    
- Infrastructure as a Service and Platform as a Service offering allows you to focus on your app development and deploy apps without worrying about the underlying Infrastructure and platform.

