# Twelve-Factor App Methodology
---

## Build, release, run
---
- Build: Transform a codebase into an executable unit called a build
- Release: Combine build with configuration so that it's ready for execution
- Run: Run the application 

## Dev/production parity
---
- Minimize differences between development and production environments
- Use same backend services across environments 

## Dependencies
---
- Assume an app is only as reliable as its least reliable dependency
- Explicitly declare any dependencies
	- No assumption that any dependencies already exist on their machine

## Backend services
---
- Do not distinguish between local and third-party services
- Access all services by a URL and credentials so that they can be swapped without changing the code 
	- Spin up new database without having to change the codes 

# What are Microservices
---

## Characteristics of microservices
---
- Application composed of many ==loosely coupled== and ==independently deployable== smaller services 
	- Each have their own technology stack 
		- Each microservices can even have different programming languages 
		- dependent on each other via an API 

## Benefits of microservices
---
### Benefits
- Ease of development and update 
- Flexible to use different tech stacks and add new technology
### Drawbacks:
- Security challenges
- Debugging

## Practices
---
- Start with monolithic and refactor into microservices
- Don't build nanoservices; the complexity will outweigh the gains 
- Don't build gateway for each service, use API Gateways instead 

# Web API Essentials: REST API and GraphQL
--- 

## What is REST?
--- 
- REST(REpresentational State Transfer)
	- Flexible and lightweight way to integrate applications 
	- Defines how apps should communicate on a network 

## Key REST Characteristics
---
- Requests managed through HTTP
	- To perform standard CRUD(Creating Reading Updating and Deleting ) functions
		- Create = POST
		- Read = GET
		- Update = PUT
		- Delete = DELETE
- Stateless client-server 
	- Each request contains all the necessary information 
	- API requests for resources should look the same regardless of origin
	- One identifier = One URI(Uniform Resource Identifier)
	- Complete information 
- Uniform interface between components 

## Introduction to API Gateway
---

### What is an API Gateway? 
---
- API management tool
- Sits between client and collection of backend services 

### Why do you use an API Gateway
---
- Protect your APIs
- Analyze your API usage
- Monetize your APIs
- Present a single point of contact to microservices
- Add and remove APIs seamlessly 