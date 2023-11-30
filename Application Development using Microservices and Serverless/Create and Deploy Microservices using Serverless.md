# IBM Cloud Code Engine

## Challenges of Self-Hosting Microservices

- **Configuration**: Microservices must be configured with necessary assets for production readiness.
- **Build**: Compilation into an executable binary for hosting environments.
- **Infrastructure**: Selection of web servers, operating systems, databases, etc.
- **Scalability**: Dynamic scaling to handle fluctuating traffic.
- **Communication**: Ensuring reliable and secure inter-microservice communication.
- **Monitoring**: Logging, monitoring, and dashboard analysis for stability and issue identification.

## Deploying Python-Based Microservices

- **WSGI**: Web Server Gateway Interface for synchronous calls.
  - Examples: Green Unicorn, uWSGI.
- **ASGI**: Asynchronous Server Gateway Interface for asynchronous calls.
  - Examples: Daphne, Hypercorn.
- **Infrastructure Needs**: From laptops to sophisticated clusters.

## IBM Cloud Code Engine (Code Engine)

- **Purpose**: Simplify the deployment of microservices with a focus on code development.
- **Features**:
  - Serverless platform that handles PaaS, CaaS, and serverless deployment models.
  - Manages the operational burden of building, deploying, and managing workloads.

### Use Cases for Code Engine

1. **Deploy Applications**: Serve HTTPS requests for microservices, web apps, console apps.
2. **Build and Deploy from Source**: Use Code Engine to build from source (GitHub, local workspace) and deploy automatically.
3. **Run Batch Jobs**: Execute data processing or analytics tasks within the same platform.

## Benefits of IBM Cloud Code Engine

- **Cluster Management**: Automates provisioning, configuration, scaling, and server management.
- **Rapid Deployment**: Builds and deploys apps in seconds, suitable for urgent updates.
- **Automatic Scaling**: Adjusts workload scaling as needed.
- **Access Management**: Controls permissions based on IBM Cloud infrastructure.
- **Security**: Ensures secure connections with TLS and workload isolation.
- **Integration**: Full access to IBM Cloud services catalog.

## Conclusion

- **Complexity of Self-Hosting**: Self-hosting microservices can be complex and challenging.
- **Managed Deployment**: IBM Cloud Code Engine manages the difficult aspects of deployment.
- **Code Focus**: Enables developers to concentrate on coding rather than infrastructure.
- **Versatility**: Supports application deployment, direct builds from source, and job execution.


# Project, Application, Build, and Jobs in IBM Cloud Code Engine

## Introduction
This note summarizes the key concepts of Project, Application, Build, and Jobs in IBM Cloud Code Engine, as explained in the video.

## Project in Code Engine
- **Definition**: Represents a group that contains and manages its resources and entities.
- **Functions**:
  - **Namespace**: Provides isolation and unique naming within a group.
  - **Resource Management**: Manages resources and access control.
- **Example**: 'my-project' with a summary of entities (e.g., 11 applications, 2 jobs).

## Application in Code Engine
- **Purpose**: To run code, serving HTTP requests or providing REST APIs.
- **Features**:
  - Supports WebSockets for long-running, session-based communication.
  - Automatic scaling of running instances based on workload.
- **UI Example**: 'my-application' under 'my-project', with deployment status and configuration options.

## Build in Code Engine
- **Definition**: Process of creating a container image from source code.
- **Methods**:
  - **Dockerfile**: Text file with commands to build a docker container image.
  - **Buildpack**: Provides executables for tasks like inspecting source code and producing an image.
- **Usage**: Deploy the built container image to Code Engine to create an application.

## Job in Code Engine
- **Definition**: One-time execution of code.
- **Characteristics**:
  - Runs executable code for specific tasks.
  - Creates instances based on workload, designed to run once and exit.
- **Examples**:
  - Data processing for querying and transforming data.
  - Machine learning model training.
  - Reporting and billing jobs.

## Summary
- **Project**: A grouping of entities like applications, jobs, and builds in Code Engine.
- **Application**: Runs code for HTTP requests or WebSocket sessions.
- **Build**: Process to create a container image from source code.
- **Job**: Executes one-time tasks with one or more instances of executable code.

# Building Container Images for Microservices

## What You Will Learn
- Understand what a Container is
- Comprehend what Docker is
- Learn how to build a Docker container image

## Containers
- Standalone, all-inclusive, executable unit of software
- Packs application source code, libraries, dependencies, and runtimes
- Runs on various platforms (laptops, desktop PCs, on-premises servers, cloud)
- Benefits: Small, fast, portable, and do not require a guest OS per instance

## Docker
- Leading software platform for building and running applications as containers
- Promotes widespread use of containerization
- Provides a comprehensive ecosystem with a variety of tools and technologies
- Central to IBM Cloud Engine for running containers

## Container Images
- Immutable files containing all the necessary application assets
- Read-only; changes result in a new image
- Analogous to a class in object-oriented programming, serves as a template for containers

## Building a Container Image
- Start by creating a Dockerfile, which is a blueprint for the container image
- Docker handles the build process based on the Dockerfile instructions

## Dockerfile Example for a Flask Microservice
```Dockerfile
# Use an official Python runtime as a parent image
FROM python:3.8-slim

# Set the working directory in the container
WORKDIR /app

# Copy the current directory contents into the container at /app
COPY . /app

# Install any needed packages specified in requirements.txt
RUN pip install --no-cache-dir -r requirements.txt

# Make port 8080 available to the world outside this container
EXPOSE 8080

# Define environment variable
ENV LISTEN_PORT=8080

# Run app.py when the container launches
CMD ["python", "app.py"]
```
- `FROM` specifies the base image
- `COPY` transfers files to the container's filesystem
- `ENV` sets environment variables
- `EXPOSE` informs Docker that the container listens on the specified network port at runtime
- `RUN` executes a command
- `CMD` sets the default command to run the container

## Container Registry
- A service to manage container images
- Examples: Docker Hub, IBM Cloud Container Registry
- Use an image name consisting of hostname, repository, and tag to pull the image

## Summary
- Containers encapsulate software with its dependencies
- Docker simplifies the containerization process
- Dockerfile instructs Docker on how to build an image
- Container images are stored and managed in registries and identified by unique names

# Deploying and Running Applications

## Overview
After completing this module, you will be able to:
- Explain two main modes of deploying a container image-based application.
- Describe how to use IBM Cloud Console for app deployment.
- Describe how to use IBM Cloud CLI for app deployment.

## Two Modes of Deployment
### IBM Cloud Code Engine Deployment
- **Container Registry Deployment**: Build and push your container image to a private or public container registry. Cloud Code Engine pulls the image by the unique name after granting registry access.
- **Build from Source**: Specify a dockerfile or a buildpack along with your code. Cloud Engine builds the application from the source code and then deploys it.

### IBM Cloud Console
- A user-friendly web portal to manage IBM cloud services and deploy applications with ease.
- Steps for application deployment via console:
  1. Specify the application's name.
  2. Choose to deploy from a Container image or Source code.
  3. Provide the image reference and, if necessary, registry access.

## IBM Cloud CLI
- Alternative for users familiar with command-line interfaces.
- Deploy apps with more precision.
- Command to create and deploy an application: `ibmcloud ce app create`.
- Arguments include the application name, image reference, and registry access.
- Test the application with: `ibmcloud ce app get`.

## Example Commands
```bash
# To create an application:
ibmcloud ce app create --name 'helloworldapp' --image us.icr.io/myimage --registry-secret 'myregistry'

# To test the deployed application:
ibmcloud ce app get --name 'helloworldapp' --output url
```
## Application Endpoints

- Once deployed, the Code Engine provides an endpoint URL for your application.
- This URL leads to the main page or the entry endpoint of your microservice.

## Conclusion

- Two deployment options: use a pushed container image or build from source.
- IBM Cloud Console and CLI are both available for application deployment.

# Updating Deployed Applications

## Overview
After completing this module, you will be able to:
- Describe common scenarios of updating applications.
- Update applications using IBM Cloud Console.
- Update applications using IBM Cloud CLI.

## Updating Applications: Common Scenarios
- Migrating databases (e.g., from SQL DB to NoSQL DB).
- Developing and building a new container image for a DB service.
- Adding new environment variables.
- Allocating more computational resources.

## Code Engine Application Revisions
- Code Engine manages application revisions, allowing updates without redeployment.
- New revisions are created automatically during an update.

## IBM Cloud Console
- Suitable for simple updates like adding an environment variable.
- Steps to update via console:
  1. Access the Environment variables table.
  2. Click "Add environment variable" to update or add new variables.

## IBM Cloud CLI
- Provides precision for complex updates.
- Main command: `ibmcloud ce application update`.

### Example: Adding an Environment Variable
```bash
ibmcloud ce app update --name 'pet_db_service' --env DB_HOST=localhost
```
- Verify the update with:
```bash
ibmcloud ce app get --name 'pet_db_service'
```

## Application Visibility
- Types of URLs: Internal (within the app) and External (public or IBM private network).
- Update visibility through the system Domain mappings tab or CLI.

### Example: Updating Application Visibility to Private
```bash
ibmcloud ce app update --name 'pet_db_service' --visibility private
```

## Updating Image References
- Change in the Console UI via the “Code” tab.
- CLI command includes the application name, image reference, and registry secret.

### Example: Updating Image Reference
```bash
ibmcloud ce app update --name 'pet_db_service' --image us.icr.io/petshop/no_sql_pet_db_service --registry-secret 'myregistry'
```

## Updating Runtime Resources
- Update CPU, memory, and storage on the `Runtime` tab in the Console UI.
- Adjust scaling and concurrency settings.

### Example: Updating Runtime Resources via CLI
```bash
ibmcloud ce app update --name 'pet_db_service' --cpu 2 --memory 16G
```

## Conclusion
- Application updates are straightforward with IBM Cloud Console or CLI.
- IBM Cloud Code Engine simplifies revision management during updates.

# Module 4 Summary

- Self-hosted microservices can be very complex and challenging
    
- IBM Cloud Code Engine is a fully managed platform that takes care of all the hard deployment work, allowing developers to focus on their code
    
- IBM Cloud Code Engine has three main use cases: 1) deploy applications, 2) build and deploy applications, and 3) run jobs
    
- A project is a grouping of Code Engine entities such as applications, jobs, and builds
    
- An application runs your code to serve HTTP requests or to create WebSocket sessions
    
- A build is a process to create a container image from your source code
    
- A job runs one or more instances of your executable code
    
- A container is a standalone executable software unit packaged with all its dependencies
    
- Docker is a popular container building and running platform
    
- You can compose a Dockerfile to instruct the Docker platform to build a container image
    
- After the container image is built, it can be pushed to the container registry and then be pulled by its image name
    
- You can create a Cloud Engine application either from a pushed container image or a source code repository
    
- As per your preference, you can choose to use the IBM Cloud Console or IBM Cloud CLI to perform the application deployment tasks