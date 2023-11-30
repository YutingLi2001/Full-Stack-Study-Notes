# Introduction to Serverless Computing

## Definition of Serverless Computing
Serverless computing is defined by the Cloud Native Computing Foundation (CNCF) as:
> "The concept of building and running applications that do not require server management."

It involves applications deployed as one or more functions that are executed, scaled, and billed based on demand.

## Concepts of Serverless Computing
- **Function-as-a-Service (FaaS)**: Platforms to run functions.
- **Backend-as-a-Service (BaaS)**: Backend cloud services like databases and storage.

## Evolution of IT Computing
1. **Traditional Computing**: Physical machines with significant upfront investment and long deployment times.
2. **Virtualization**: Enables faster provisioning, scalability, and virtual machines (VMs) or containers.
3. **Containers**: Quick deployment and short-lived, based on OS virtualization.
4. **Serverless Computing**: Milliseconds to deploy, lifespan of seconds, abstracts infrastructure and software environments.

## Characteristics of Serverless Computing
- Hostless
- Elastic and autoscaling
- Automated load balancing
- Stateless
- Event-driven
- High availability
- Usage-based billing

## Function Workflow in Serverless Computing
1. Write code in a supported programming language.
2. Upload the function to the cloud.
3. Define events to trigger the function.
4. On event occurrence, the function is executed by the cloud provider.

## Developer Advantages
- Focus on creating optimized applications.
- Use any popular programming language.
- Add features and perform better testing.
- Improve user experience.

## Cloud Provider Responsibilities
- Infrastructure management and maintenance.
- OS updates and security patches.
- Autoscaling and high availability.
- Security, performance, monitoring, and logging.

## Comparison of Cloud Service Models
- **Traditional**: You manage everything.
- **Infrastructure as a Service (IaaS)**: You manage from OS upwards.
- **Platform as a Service (PaaS)**: You manage applications and data.
- **Serverless**: You manage only the application.
- **Software as a Service (SaaS)**: Cloud provider manages all.

## Key Takeaways
- Serverless computing allows for building applications without server management.
- Cloud providers manage the infrastructure, leading to zero operational considerations for the user.
- Billing is based only on usage, not CPU idle time.


# Serverless Pros and Cons

## Benefits of Serverless Computing

- **Infrastructure Management**: Cloud providers manage infrastructure, reducing maintenance requirements and costs.
- **High Availability and Fault Tolerance**: Reliability is offloaded to the cloud provider, ensuring service continuity.
- **Developer Focus**: Developers can concentrate on writing code and application development rather than infrastructure concerns.
- **Resource Optimization**: Serverless functions run only when needed, saving resources.
- **Speed**: Functions execute in milliseconds, compared to containers or VMs that take seconds or minutes.
- **Integrated Development Environment (IDE)**: Cloud IDEs expedite development, deployment, and updates.
- **Cost-Effective**: Billing is based on pay-per-request, not idle resources.
- **Language Flexibility**: Supports various popular programming languages.
- **Third-Party Services**: Abundant support for authentication, database, and backend services.
- **Innovation**: Encourages innovation with the ability to quickly test and deploy new features.
- **Green Computing**: Reduction in infrastructure leads to more sustainable computing practices.

## Constraints of Serverless Computing

- **Cost for Long-Running Processes**: Traditional computing may be more cost-effective for applications with long-running processes.
- **Vendor Lock-In**: Reliance on specific cloud technologies can lead to platform dependency.
- **Cold Starts**: Applications may experience delays when restarting after inactivity.
- **Latency**: Not suitable for time-sensitive applications due to potential delays.
- **Security**: New security concerns arise as the attack surface shifts.
- **Monitoring and Debugging**: Distributed systems make these tasks more complex.
- **Language Support**: Limited to the languages supported by the cloud provider.
- **Lack of Control**: No direct server optimization or performance tuning.
- **Statelessness**: Previous execution state is not preserved across function invocations.

## Serverless vs Containers

- **Serverless**:
  - More cost-effective, only pay for usage.
  - Automatic scalability by the provider.
  - Quick deployment in milliseconds.
  - Allows companies to focus on core business.
- **Containers**:
  - Easier local or cloud testing.
  - OS, language, and provider agnostic, enabling easy portability.
  - Suitable for long-running and time-critical tasks.
  - Configurable apps and resource usage.

## Serverless vs Traditional Computing

- **Serverless**:
  - Developers write high-quality code without infrastructure concerns.
  - Pay-per-use cost structure.
  - Automatic scalability and available libraries/integrations.
- **Traditional**:
  - Data and network control within the organization.
  - Standard security implementations within network perimeter.
  - Reduced chance of vendor lock-in due to self-managed infrastructure.

## Conclusion

- **Serverless** allows teams to focus on development with benefits like high availability, quick function run times, and pay-per-request billing but has challenges for time-critical apps, monitoring, and lacks state persistence.
- **Containers** offer advantages like easy testing, low latency, and support for any language, ideal for specific long-running applications.
- **Hybrid Solutions**: Serverless and containers can be combined for a balanced approach.
- **Traditional Computing** has its place with full control over data and infrastructure, but lacks the scalability and cost-effectiveness of serverless solutions.

Both serverless and traditional computing paradigms have distinct advantages and trade-offs, and the choice between them depends on the specific needs of the application and the organization.

# Introduction to the FaaS Model

After completing this module, you will be able to:

- Describe what FaaS is.
- Explain the benefits of a FaaS model.
- Describe the principles and best practices of FaaS.

## What is Function-as-a-Service (FaaS)?

Function-as-a-Service, or FaaS, is a type of cloud-computing service that allows you to execute code in response to events, which eliminates the need for complex infrastructure typically associated with building and launching microservices applications.

### Characteristics of FaaS:

- It is a subset of serverless computing.
- Applications are created as multiple functions.
- Functions are small, independent pieces of code written in any programming language.
- Deployable on hybrid clouds and on-premises environments.
- Stateless but can maintain state using external services.
- Functions execute in milliseconds, processing requests in parallel.
- Scalability is instantaneous.
- Utilizes a decoupling architecture mechanism.
- Billed based on the time taken to run functions, not server size.

## Benefits of the FaaS Model

- Reduces time-to-market by allowing focus on app code.
- Cost-effective: Pay only for the action as it occurs.
- Automatically and independently scalable.
- High availability across regions and zones.
- Deployable without incremental costs.

## Serverless Stack Components

1. **Function-as-a-Service (FaaS)**
2. **Backend-as-a-Service (BaaS)**
3. **API Gateway**

### Workflow of Serverless Stack:

- Event requests (HTTP requests, webhooks, scheduled jobs) are received.
- Requests pass through the API Gateway.
- Functions process the requests.
- Backend services are used if necessary for further processing/storage.
- The response is sent back to the client via FaaS and the API Gateway.

## Real-World Example

- **Use Case:** Uploading and processing a profile picture with thumbnail creation.
- **Process:**
  - User uploads a profile photo to object storage.
  - This triggers a cloud function to process the photo and create a thumbnail.
  - The thumbnail is stored in object storage for website access.

## Best Practices for FaaS

- Functions should do a single piece of work in response to an event.
- Code should be limited in scope, efficient, and lightweight for quick execution.
- Minimize the number of functions to reduce costs and maintain function isolation.
- Avoid excessive third-party libraries to keep function initialization fast.

## FaaS Providers

### Managed FaaS Providers:

- AWS Lambda
- Google Cloud Functions
- Azure Functions
- Cloud Functions by IBM
- OpenShift Cloud Functions by Red Hat
- Netlify, Oracle, Twilio

### Self-Managed FaaS Options:

- Fission (Serverless functions on Kubernetes)
- Fn Project (Container-native serverless platform)
- Knative (Kubernetes-based serverless workload management)
- OpenFaaS (Turns any process into a function)

## Summary

- FaaS is a cloud-computing service that simplifies code execution in response to events.
- It's part of serverless computing and focuses on function-based applications.
- Offers a cost-effective, scalable, and highly available system.
- Comprises of FaaS, BaaS, and API Gateway in the serverless stack.
- There is a variety of managed and self-managed FaaS platforms available.

# The Serverless Framework

This document will guide you through understanding the Serverless Framework and how to get started with creating and testing a basic Serverless function.

## What is the Serverless Framework?

The Serverless Framework is a free, open-source web framework written in Node.js. It is designed to help you quickly and safely provision your cloud functions, events, and resources.

### Supported Providers:

- Amazon Web Services (AWS)
- Microsoft Azure
- Google Cloud Platform
- Apache OpenWhisk

### Features:

- Command Line Interface (CLI) for structure, automation, and best practices.
- Focus on building event-driven architectures.
- Functions as units of execution.
- Triggered by events from resources like HTTP requests or file uploads.
- Organized into services managed by `serverless.yml` files.

## Creating a Basic Serverless Function

To create a basic Serverless function, you need to follow these steps:

1. **Install the Serverless CLI**: You can install it globally using npm with the command `npm install -g serverless`.
2. **Set up your provider's credentials**: For AWS, make sure your credentials are configured.
3. **Create a new service**: Use the `serverless` command to initiate a new service.
4. **Define your function and events in `serverless.yml`**: This file controls your service's setup.

### Example of a 'Hello World' Function in AWS:

```yaml
# serverless.yml

service: hello-world

provider:
  name: aws
  runtime: python3.8

functions:
  hello:
    handler: handler.hello
    events:
      - http:
          path: /
          method: get
```

### Deploying the Function:

- Run `serverless deploy` in your project directory.
- After deployment, you will receive a URL endpoint.
- Accessing the URL in a browser will execute your function.

## Testing Your Serverless Function

After deployment, you can test your function by:

- Navigating to the provided URL endpoint in a web browser.
- Checking the response to ensure it matches your expected output.

## Summary

- The Serverless Framework offers a streamlined approach to deploying serverless applications.
- It supports multiple cloud providers and simplifies the process of setting up functions, events, and resources.
- The `serverless.yml` file is central to configuring your service.
- Testing is as simple as deploying your service and navigating to the provided endpoint.
# Serverless Reference Architecture and Use Cases

By the end of this module, you will be able to:

- Explain a Web Application reference architecture using the Serverless Framework.
- Describe various use cases of the Serverless Framework.

## Web Application Reference Architecture

### Components of a Serverless Web Application:

1. **Front-end:**
   - Static content generated by Create React App.
   - Hosted on AWS Amplify Console.
   - Utilizes HTML, CSS, JavaScript, and images.
   - Interacts with the backend via REST API calls.

2. **Back-end:**
   - Business logic implemented in AWS Lambda functions.
   - Accessed by the front-end through Amazon API Gateway.
   - Data is stored in Amazon DynamoDB.
   - REST API used for communication.

3. **User Registration and Authentication:**
   - Managed by Amazon Cognito User Pools.
   - Allows user registration and authentication.
   - Ensures users access only their To Do items.

### Architecture Overview:

- AWS Lambda for business logic execution.
- Amazon API Gateway for REST API endpoints.
- Amazon DynamoDB as the database.
- Amazon Cognito for user management.
- AWS Amplify Console for hosting static content.

## Use Cases of Serverless Framework

1. **Event Streaming:**
   - Deploy applications without upfront infrastructure.
   - Triggered by pub/sub topics or event logs.
   - Provides scalable event pipelines without maintenance.

2. **Post-processing:**
   - Image and Video Manipulation like resizing or transcoding.
   - Utilizing AI for tasks like image recognition.

3. **Multi-language Support:**
   - Avoids language lock-in, allowing the use of multiple programming languages.

## Summary

- The serverless web application architecture is event-driven and comprises three main components: front-end, back-end, and user registration/authentication.
- Utilizes AWS services such as Lambda, API Gateway, DynamoDB, Cognito, and Amplify Console.
- Serverless use cases include event streaming, post-processing, and support for multiple programming languages in application development.

# Popular Serverless Platforms

## Introduction
This document outlines the most popular Serverless Platforms, their differentiators, and use cases. Serverless computing allows users to run code without server management, scaling automatically according to the application's needs.

## AWS Lambda
- **Provider**: Amazon Web Services (AWS)
- **Characteristics**: 
  - Event-driven, automatic scaling
  - Charges for function execution and data transfer only
- **Use Cases**: 
  - File processing
  - Web applications
  - IoT and mobile back-ends

## Google Cloud Functions
- **Provider**: Google Cloud Platform
- **Characteristics**: 
  - Simple developer experience
  - Scales to zero instantaneously
  - Real-time data sync with Firebase
- **Use Cases**: 
  - Lightweight ETL functions
  - Event-driven execution

## Microsoft Azure Functions
- **Provider**: Microsoft Azure
- **Characteristics**: 
  - Supports multiple programming languages
  - DevOps integration
  - Different plans for various needs
- **Use Cases**: 
  - Run code on file upload/change
  - Data processing from IoT devices
  - Scheduled code execution

## IBM Cloud Functions
- **Provider**: IBM Cloud
- **Characteristics**: 
  - Pay-for-what-you-use pricing
  - Integration with IBM Watson
  - High availability across multiple regions
- **Use Cases**: 
  - Cognitive services (e.g., object detection in images/videos)
- **Development Tools**: 
  - Log Analysis with LogDNA
  - IBM Cloud Monitoring

## Knative
- **Provider**: Open-source
- **Characteristics**: 
  - Kubernetes-based, avoids vendor lock-in
  - Platform-agnostic
  - Customizable rollout strategies
- **Advantages**: 
  - Deployable on any Kubernetes-supporting cloud
  - Traffic shifting for gradual deployment

## Summary
- **AWS Lambda** offers event-driven scalability with a pay-as-you-go model.
- **Google Cloud Functions** focuses on a simple developer experience and integrates with Firebase for real-time data updates.
- **Microsoft Azure Functions** emphasizes cloud and edge computing with strong DevOps features.
- **IBM Cloud Functions** provides high availability and integrates with cognitive services.
- **Knative** leverages Kubernetes to provide a serverless solution without vendor lock-in.
