# Twelve-Factor App Methodology

## Introduction
- **Modern Software Development**: Software delivered as a service (SaaS), accessed via the internet.
- **Goal**: To create efficient and scalable SaaS applications.
- **Twelve-Factor App Methodology**: A set of principles for building software that is:
  - Easy to maintain.
  - Scalable.
  - Capable of being deployed on modern cloud platforms.

## Twelve Factors
The twelve factors are divided into three phases of the software delivery lifecycle: **Code**, **Deploy**, and **Operate**.

### Code
1. **Codebase**
   - A one-to-one relationship with the app.
   - Use version control (e.g., Git).
   - Single codebase with multiple deploys.

2. **Dependencies**
   - Explicitly declare and isolate dependencies.

5. **Build, release, run**
   - Separate build and run stages.
   - Codebase turns into a build.
   - Build combines with config to create a release.
   - Releases are executed in the run stage.

10. **Dev/prod parity**
   - Keep development, staging, and production as similar as possible.

### Deploy
3. **Config**
   - Store config in environment variables.

4. **Backend services**
   - Treat backing services as attached resources.

6. **Processes**
   - Execute the app as one or more stateless processes.

7. **Port binding**
   - Export services via port binding.

### Operate
8. **Concurrency**
   - Scale out via the process model.

9. **Disposability**
   - Fast startup and graceful shutdown.

11. **Logs**
   - Treat logs as event streams.

12. **Admin processes**
   - Run admin/management tasks as one-off processes.

## Summary
- **SaaS Applications**: Centrally hosted and managed.
- **Efficiency and Scalability**: Achieved by following the twelve factors.
- **Lifecycle Phases**: Each factor maps to a specific phase, ensuring best practices across the development lifecycle.


# What are Microservices?

## Overview
Microservices architecture is a method of developing software applications as a suite of small, independent services, each running in its own process and communicating with lightweight mechanisms.

## Characteristics
- **Loosely Coupled**: Services are independent and can be deployed separately.
- **Technology Diversity**: Services can use different technology stacks, including different programming languages and data storage technologies.
- **Business-driven**: Organized around business capabilities with services implementing a small set of related functions.

## Communication
- Services interact using APIs, often RESTful.
- Utilize event streaming and message brokers for service communication.

## Benefits
- **Independent Scaling**: Each microservice can be scaled independently, which can lead to cost savings and improved efficiency.
- **Ease of Deployment**: Individual components can be updated without redeploying the entire application.
- **Resilience**: Failures in one microservice do not necessarily cause system-wide failures.

## Scaling Microservices
- **Horizontal Scaling**: Adding more instances of services ("scaling out") rather than increasing the capacity of individual components ("scaling up").
- **Precise Scaling**: Only the components under heavy load are scaled, preventing unnecessary resource usage.

## Event Streaming
- Allows for broadcasting state changes among services, which is essential for keeping services up-to-date and scalable.

## Conclusion
Microservices architecture offers a flexible, scalable approach to building modern software applications, allowing for the use of diverse technologies and independent service scaling.

# Microservices Patterns

Microservices architecture enables various patterns to address common challenges and opportunities in software development.

## Patterns for Microservices

### Single-Page Application (SPA)
- **Concept**: A web application or site that interacts with the user by dynamically rewriting the current page rather than loading entire new pages from the server.
- **Technology**: Utilizes HTML, CSS, and JavaScript.
- **User Interface**: The landing page doesn't reload or navigate away, creating a seamless user experience.
- **Backend Services**: Dynamic service calls to REST-based services update parts of the page.

### Backend for Frontend (BFF)
- **Purpose**: Tailors backend services to specific frontend experiences (e.g., mobile vs. desktop).
- **Benefits**:
  - Customized user experiences.
  - Optimized performance for each channel.
- **Implementation**: Separate backends for each type of user interface, each being a microservice.

### Strangler Pattern
- **Metaphor**: Named after a vine that slowly overtakes a tree.
- **Application**: Refactors a monolithic application into microservices incrementally.
- **Process**:
  - **Transform**: Create a new site parallel to the existing one.
  - **Coexist**: Keep both sites live, gradually redirecting traffic to the new site.
  - **Eliminate**: Remove or decommission the old site once the new one is fully operational.

### Service Discovery
- **Necessity**: Service instances frequently change in a microservices architecture.
- **Functionality**: Enables services to discover each other for load balancing, health checks, and traffic rerouting.

### Additional Patterns
- **Entity and Aggregate Pattern**: Useful for e-commerce applications, grouping products by a buyer.
- **Adapter Pattern**: Serves to translate between incompatible systems, such as integrating with third-party APIs.

## Summary
- **SPA**: Offers dynamic updates to web pages through backend services.
- **BFF**: Allows for the development of channel-specific backend services.
- **Strangler Pattern**: Provides a method for transitioning from monolithic architecture to microservices.
- **Service Discovery**: Essential for dynamic service instance management and communication.

# Microservices Anti-Patterns

## Introduction
Understanding the common pitfalls in microservices architecture is crucial to avoid complications in development and operations.

## Common Anti-Patterns

### Don't Start With Microservices
- **Rule**: Begin with a monolithic architecture; only consider microservices when the complexity of the monolith hinders development and maintenance.
- **Rationale**: Early adoption without necessity can lead to premature and unnecessary fragmentation.

### Underestimating Automation
- **Concern**: Microservices increase the complexity of deployment and monitoring.
- **Solution**: Implement DevOps practices and utilize cloud services to manage the diverse and distributed nature of microservices.

### Avoid Nanoservices
- **Issue**: Over-segmenting services can lead to increased complexity with minimal gains.
- **Guideline**: Opt for larger services initially and split them only when necessary due to:
  - Difficult deployment.
  - Complex common data model.
  - Diverging loading and scaling requirements.

### Don't Confuse with SOA
- **Misconception**: Microservices and SOA are often mistakenly equated.
- **Differentiation**: Microservices should remain fine-grained with independent data storage (bounded context) to avoid becoming unwieldy like some SOA implementations.

### Don't Build a Gateway for Each Service
- **Problem**: Replicating authentication, throttling, and other non-functional concerns in each service is inefficient.
- **Solution**: Use an API Gateway as a singular management tool for these tasks.

## Conclusion
The goal of microservices is to enhance customer experience, adapt flexibly to new demands, and reduce operational costs with fine-grained services. Avoiding these anti-patterns is essential to ensure microservices become an asset rather than a liability.
