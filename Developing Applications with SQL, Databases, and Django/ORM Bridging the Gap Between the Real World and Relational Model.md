# Introduction to Django 

## Overview
- **Django** is a high-level, accessible, open-source Python web framework.
- It adheres to the Model-View-Controller (MVC) pattern, promoting rapid development and code reusability.

## Key Features
- **Versatility:** Can be used to build various web applications like CMSs, social media platforms, business applications, and more.
- **“Batteries-Included”:** Offers a wide range of built-in features and functionalities.
- **Object Relational Mapping (ORM):** Allows defining data models using Python classes, simplifying database operations.
- **Built-In Template Engine:** Separates business logic from presentation, facilitating a clean and maintainable code structure.
- **Administration Interface:** Automatically generated and customizable, providing a user-friendly interface for content management.
- **Security:** Robust security features protect against web vulnerabilities (XSS, CSRF, SQL injection) and manage user sessions and password hashing.

## Authentication & Authorization
- Built-in mechanisms for user account management, permissions, and access restrictions.

## Expandability
- Django is extensible through modules (Django apps or packages), which are reusable components adding specific functionalities.
- Supports third-party packages and built-in modules for various functionalities, including form validation and captcha integration.

## Architecture
- Follows a **stateless (share-nothing) architecture**, with each server instance operating independently.
- This architecture supports easy scaling and session management across multiple application instances without data loss.

## Testing
- Supports various types of tests (unit, integration, functional) with a comprehensive testing framework and utilities.

## Platform-Agnostic
- Built on Python, it can run on various platforms and is supported by numerous cloud providers.
- The platform independence allows flexibility in choosing hosting platforms.

## Community & Adoption
- Has a vibrant and dedicated community contributing to its continuous improvement.
- Adopted by renowned platforms like Instagram, Spotify, YouTube, and The Washington Post for various purposes.

## Summary
- **Django is comprehensive:** With features like ORM, templates, admin interface, security mechanisms, and more.
- **Extensible and Versatile:** Supports modules and packages, used for various types of web applications.
- **Stateless Architecture:** Allows independent operation of server instances and easy scaling.
- **Testing Support:** Offers a robust testing framework.
- **Platform Independence:** Runs on various platforms and cloud providers.
- **Widely Adopted:** Used by various famous platforms and supported by a strong community.

# Introduction to Object-Oriented Analysis and Design (OOAD)

## Overview
- **OOAD** is a method for analyzing and designing a system by visualizing it as a group of interacting objects, each defined by their roles and responsibilities.

## Object-Oriented Programming (OOP)
- **Objects:** Core components that contain data and behaviors, reflecting the actions they can execute.
  - Example: An object representing a patient, "Nia Patel".
- **Classes:** Blueprints or templates for creating objects (instances).
  - Example: "Patient" class, with "Nia Patel" as an instance.
- **Instances:** Specific objects created from classes.
  - Example: "Nia Patel" is an instance of the "Patient" class.

## Objects and Classes
- **Classes:**
  - Define generic attributes (properties and methods).
  - Attributes are placeholders until an instance is created.
- **Objects (Instances):**
  - Created from classes during instantiation.
  - Assigned specific attribute values upon creation.

## Object-Oriented Analysis and Design (OOAD)
- **Purpose:** Provides a structured method for analyzing and designing systems using OOP languages.
- **Focus:** Objects and their interactions.
- **Advantages:** Facilitates concurrent development by multiple developers on different parts of an application.

## Unified Modeling Language (UML) Diagrams
- **Class Diagrams:** Visual tools for representing the structure of a system.
  - Show relationships and attributes of classes.
  - Example: "Doctor", "Nurse", "Technician" as subclasses of "Medical Personnel".
- **Behavioral Diagrams:** Illustrate the dynamic aspects of a system.

## Class Diagrams
- **Components:**
  - Boxes representing classes.
  - Attributes (properties and methods) within each class.
  - Relationships between classes.
- **Inheritance:** Subclasses inherit attributes from parent classes, with the possibility of adding more.
  - Example: "Specialist" as a subclass of "Doctor".

## Summary
- **OOAD:** Planning approach based on objects and their interactions.
- **Objects:** Data containers with prescribed actions and behaviors.
- **Classes:** Templates for objects.
- **Class Diagrams:** Visual representations of class relationships and attributes in a system.



# Object-Relational Mapping (ORM) Tools Overview

## Introduction
- ORM tools bridge the gap between object-oriented programming languages and relational databases.
- They simplify database operations and eliminate the need for complex SQL queries.

## Python ORM Tools

### 1. **Django ORM**
   - Integrated within the Django web framework.
   - High-level API for database interaction.
   - Features: Model definition, query construction, database migrations, and automatic query optimization.

### 2. **SQLAlchemy**
   - Offers a flexible and expressive database API.
   - Supports both high-level and low-level ORM.
   - Provides abstraction levels to suit developers’ needs.

### 3. **web2py**
   - Open-source, full-stack web framework.
   - Simplifies web application development.
   - Includes a web server, database abstraction layer, and a development environment.

## Java ORM Tools

### 1. **Hibernate**
   - Widely used for mapping Java objects to relational databases.
   - Features: Lazy loading, caching, and transaction management.
   - Supports various database systems.

### 2. **EclipseLink**
   - Open-source framework supporting Java to database mapping.
   - Features: JPA, caching, advanced query capabilities.
   - Integrates with various application servers.

### 3. **Apache OpenJPA**
   - Implementation of the JPA specification.
   - Facilitates transparent persistence of Java objects.

## .NET ORM Tools

### 1. **Entity Framework**
   - Microsoft’s ORM for .NET applications.
   - Supports different database providers.
   - Features: Query capabilities, code-first, and database-first approaches.

### 2. **Dapper**
   - Micro-ORM focusing on performance and simplicity.
   - Suitable for scenarios requiring control over SQL queries.

### 3. **NHibernate**
   - Inspired by Hibernate for Java.
   - Bridges .NET programming and relational databases.

## Ruby ORM Tools

### 1. **ActiveRecord**
   - Default ORM in Ruby on Rails.
   - Features: Model associations, query generation, and database migrations.
   - Follows a convention-over-configuration approach.

### 2. **Sequel**
   - Emphasizes simplicity and a SQL-centric approach.
   - Supports various database systems.

### 3. **DataMapper**
   - Focuses on simplicity and flexibility.
   - Provides a clean API for database interaction.

## PHP ORM Tools

### 1. **Propel**
   - High-performance ORM with a focus on code generation.
   - Features: Lazy loading, eager loading, and caching.

### 2. **CakePHP ORM**
   - Built-in ORM component in CakePHP.
   - Provides a powerful API for database operations.

### 3. **Eloquent**
   - Default ORM in Laravel framework.
   - Simplifies database operations with expressive syntax.

## Conclusion
- Various ORM tools are available for different programming languages, each providing unique features and functionalities to streamline database operations and application development.

# Introduction to Object-Relational Mapping (ORM)

## Learning Objectives
* Understand differences between SQL and Object-Oriented Programming (OOP) paradigms.
* Grasp core concepts of ORM.
* Recognize pros and cons of using ORM.

## SQL vs OOP Paradigm
* SQL uses tables, rows, and columns to model data.
* OOP utilizes classes and objects.
* SQL assembles statements in application code executed via database APIs.
* Example provided of executing SQL in Python code.

## Object-Oriented Programming
* OOP models entities with classes and objects.
* Example: Course entity is defined as a class with attributes and methods.
* Entities and relationships can be modeled and manipulated with OOP.

## Object-Relational Mapping (ORM)
* ORM simplifies application development by bridging SQL and OOP paradigms.
* It allows using OOP languages for database interactions.
* Example: ORM helps transfer a Learner object into a Learner row in a database table.

### How ORM Works
1. ORM maps and transfers data stored in relational databases to objects and vice versa.
2. Developers focus on object operations, simplifying the process.
3. Example provided of a three-table join SQL query transformed into a single line of code with ORM.

## Popular ORM Libraries
* Python: Django Model, SQLAlchemy
* Java: Hibernate, OpenJPA
* JavaScript: Sequelize, TypeORM

## Pros of ORM
* Class designs define the databases.
* Developers can interact with databases without writing SQL.
* ORM interfaces manage multiple database systems, abstracting SQL syntax differences.
* ORM can accelerate application delivery.

## Cons of ORM
* Imperfect mapping due to language differences.
* Increased code coupling: database changes affect application and data access logic.
* Debugging challenges due to hidden implementation details.
* Potential reduction in application performance as ORM may not guarantee optimized SQL translations.

## Video Summary
* SQL and OOP have distinct data modeling approaches.
* ORM facilitates the interaction between SQL and OOP, allowing developers to use databases without SQL.
* While ORM offers rapid development, it also presents challenges like imperfect mapping, code coupling, debugging difficulty, and potential performance issues.

# Django Model

## Learning Objectives
* Understand core concepts of Django ORM.
* Convert entity-relationship diagrams into Django models.

## Django ORM Overview
* Django ORM is a popular Object-Relational Mapping (ORM) library for Python.
* It abstracts databases, automatically mapping objects and methods to tables and SQL queries.

## Core Concepts

### Models and Fields
* Each Django model corresponds to a database table.
* Class objects represent table rows, and fields represent table columns.
* Example: A `User` class in Django ORM creates a `User` table in the database.

### Field Definitions
* Fields in models should be defined as Field classes.
* Each field maps to a specific column type.
* Field metadata (like type and constraints) are specified using parameters in Django Field classes.

### Relationships
* Django ORM supports various relationships: One-To-One, Many-To-One, and Many-To-Many.
* Relationships between entities are modeled using specific fields (like One-To-One fields for One-To-One relationships).

### Relationship Examples
* One-To-One: A `User` class holds common fields, and an `Instructor` class has additional fields. One user corresponds to one instructor.
* Many-To-One: A `Course` class can have many associated `Project` classes, but each `Project` belongs to one `Course`.
* Many-To-Many: A `Course` can have many enrolled `Learners`, and each `Learner` can enroll in many courses.

### Intermediate Relationships
* Additional information about relationships can be stored in intermediate models (e.g., `Enrollment` table storing data on enrollments between `Learners` and `Courses`).

### Model Inheritance
* Model inheritance in Django is similar to standard Python inheritance.
* Different modes: multi-table mode, abstract base classes, and proxy models.
* Example: Multi-table inheritance creates a new table and a One-To-One field in the subclass.

## Summary of Example Database
* Example database for an online course system created with Django ORM.
* Various tables (like `User`, `Learner`, `Instructor`, `Course`, `Project`, `Enrollment`) represent different entities and relationships.
* Tables created automatically by Django ORM.

## Conclusion
* Django models map to database tables, with fields mapping to column types.
* Fields have customizable parameters.
* Django ORM supports common relationship patterns.
* The understanding and use of Django ORM simplify database interactions and application development in Python.

# Django Models CRUD 

## Learning Objectives
* Understand and use Django Model APIs for CRUD operations on objects.

## Key Concepts

### Introduction
* CRUD operations refer to Create, Read, Update, and Delete.
* Django Models provide APIs for these operations without the need for SQL queries.

### Example Models
* **User Model**: Base model with common information.
  * **Instructor Model**: Inherits from User, with additional fields.
  * **Learner Model**: Also inherits from User with different additional fields.
* **Course Model**: Has Many-To-Many relationships with both Instructor and Learner models, and Many-To-One with Project model.

### Create Operation
* Create an object and call the model’s `save` method to insert it into the database.
* For objects with foreign keys, use related model reference to establish relationships.

### Read Operation
* To read objects, construct a QuerySet using a Manager on the model class.
* The Manager, usually accessed through `objects`, acts as an interface to database records.
* Use the Manager’s `all` method to retrieve all records, returning a QuerySet.
* For specific subsets, use the `filter` method with various lookup parameters.
* Use `exclude` method to return a QuerySet of records that do not match given lookup parameters.
* For multiple filters, chain `exclude` and `filter` methods or use multiple lookup parameters in one filter method.
* For a single object retrieval, use the `get` method.

### Querying Related Records
* Django automatically handles SQL JOIN operations for queries on related records.
* You can create lookup parameters on related fields in other objects.

### Update Operation
* Update object fields and call the `save` method to apply changes to the database.
* Update operations can be applied to both primitive fields and related fields.

### Delete Operation
* Use the `delete` method on a model object or QuerySet to remove records from the database.
* Django supports various "on delete" options to be explored later.

## Conclusion
* Django Model APIs facilitate seamless CRUD operations on database data without writing SQL.
* The APIs allow for the creation, reading, updating, and deletion of objects, simplifying data manipulation tasks.

#  Related Objects 

## Learning Objectives
* Utilize Django Model APIs to access and delete related objects.

## Key Concepts

### Introduction
* Models in the online course scenario are interrelated.
  * **User Model**: One-To-One relationship with Instructor and Learner.
  * **Course Model**: Many-To-Many relationship with Instructor and Learner; Many-To-One with Project.

### Forward and Backward Access
* Django requires defining model relationships on one side— “forward access”.
  * **Example**: Defining a One-To-One field reference from Learner to User is sufficient.
* Django automatically creates a “backward access” or implicit reference.
  * Accessing related models, in both directions, becomes straightforward.

### Inheritance Relationship
* Similar to a One-To-One relationship.
* For example, the Learner class inherits from User, creating accessible references between them.

### One-To-Many and Many-To-One Relationships
* Defined using a Foreign Key field.
  * Forward reference from Project to Course allows explicit access to the course for a project.
  * Backward reference automatically created by Django lets you access projects related to a course.

### Many-To-Many Relationships
* Handled similarly to other relationships.
  * Forward and backward access available, facilitating interaction with related objects.

### Deletion of Related Objects
* Django's behavior during deletion depends on the “on delete” options set.
  * **CASCADE**: Deletes all related objects.
  * **PROTECT**: Prevents deletion if related objects exist.
  * **SET NULL**: Retains related objects, setting foreign keys to null (requires nullable foreign key).
  * **SET DEFAULT/SET**: Assigns related objects to a default or different object upon deletion.
  * **DO_NOTHING**: Leaves related objects untouched, potentially leading to orphan objects.

### Additional Methods for Handling Related Objects
* **add**: Includes an object in the related object set.
* **create**: Constructs a new object with related objects specified through parameters.
* **remove**: Excludes specific objects from the related set.
* **clear**: Erases all related objects.
* **set**: Replaces related objects with a new set.

## Conclusion
* Django Models offer a convenient API for manipulating and reading related objects, simplifying tasks involving interconnected data.
* With explicit relationships defined, Django automatically generates implicit backward relationships.
* The set “on delete” options govern the behavior during object deletion, providing control over the handling of related objects.

# ==Module 2 Summary: ORM: Bridging the Gap Between the Real World and Relational Model==

- The Object-Oriented Programming (OOP) and SQL paradigm model data differently.
    
- Object Relational Mapping, or ORM bridges the gap between OOP and SQL.
    
- ORM libraries or tools can map and transfer data stored in a relational database as rows into objects or objects into rows.
    
- ORM allows developers to use OOP to query and manipulate data because it transfers objects into rows and rows into objects.
    
- Django ORM is a Python ORM component that belongs to the Django web application framework.
    
- Django ORM can help speed up database development because you define maps to a database table for each Django model.
    
- Each Django field maps to a column type.
    
- Django automatically creates tables once models and fields are defined.
    
- Django APIs can perform Create, Read, Update, and Delete (CRUD) operations on database objects.
    
- In a Django model, you create an object and call the model’s save method to insert it into the database as a record.
    
- You must construct a QuerySet using a Manager on your model class to read objects using Django Model API.
    
- There are several ways to update database records in Django by updating objects.
    
- To delete records in a database, you call Django ORM’s Delete method on a model object or query set.

