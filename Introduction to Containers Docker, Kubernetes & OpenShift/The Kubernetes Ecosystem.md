#  Introduction to Red Hat OpenShift

## Overview of OpenShift
- **OpenShift**: Enterprise-ready Kubernetes container platform by Red Hat.
- **Purpose**: Manages hybrid, multicloud, and edge deployments.
- **Foundation**: Built on Linux, containers, and automation.

## Features of OpenShift
- Scalable across hundreds of nodes.
- Flexible infrastructure for hybrid deployment.
- Open source standards with Kubernetes and OCI containers.
- Full-stack automated operations.
- Self-service provisioning for developers.
- Includes developer tools, multilanguage support, and CI/CD integration.
- Supports over-air platform upgrades.
- One-click upgrades for services from OperatorHub.
- Streamlined container/app builds and deployments.
- Enhanced edge support for smaller-footprint topologies.
- Policy management across multiple clusters.
- Built-in access controls, threat detection, and vulnerability management.
- Supports persistent storage solutions.
- Extensive partner ecosystem.

## OpenShift vs Kubernetes
- **OpenShift**: A product with enterprise features and integrations.
- **Kubernetes**: An open-source project with broad installation flexibility.
- OpenShift has a user-friendly web console; Kubernetes console is less intuitive.
- OpenShift integrates with Jenkins for CI/CD; Kubernetes CI/CD requires additional tools.
- OpenShift provides comprehensive networking solutions; Kubernetes relies on third-party plugins.
- OpenShift's installation and security policies are stricter; Kubernetes offers more flexibility.

## OpenShift Architecture & Components
- **Architecture**: Microservices-based.
- **Components**:
  - REST APIs for core object exposure.
  - Controllers to maintain cluster state.
  - Docker for container image packaging.
  - Kubernetes for cluster management.
- OpenShift adds:
  - Source code, build, and deployment management.
  - Image promotion and application management at scale.
  - Developer organization tracking and networking infrastructure.

## OpenShift CLI (oc)
- **Functionality**: Admin and development operations from the terminal.
- **Compatibility**: Windows, Linux, Mac.
- **Extended Support**: OpenShift features like DeploymentConfigs, Routes, ImageStreams.
- **Commands**: `new-app`, integrated `kubectl`, login for authentication.

## Key Takeaways
- OpenShift extends Kubernetes with enterprise-level features.
- Facilitates development through automated operations and developer tools.
- Integrates natively with various Red Hat and third-party services.

# OpenShift Builds 

## Definition of a Build
- A Build is the transformation process of inputs (like source code) into a resultant object (e.g., a container image).

## BuildConfig
- BuildConfig: A configuration file defining build strategy and input sources.
  
## Build Strategies
- Source-to-Image (S2I): Combines application source with a builder image.
- Docker: Uses Dockerfile and “docker build” command to create images.
- Custom: User-defined builder images for specialized build outputs.

## Build Inputs (Precedence Order)
1. Inline Dockerfile
2. Content from existing images
3. Git repositories
4. Binary/Local inputs
5. Input secrets
6. External artifacts

## ImageStreams
- Abstraction for referencing container images within OpenShift.
- Updates tags (like `latest`, `dev`, `test`) that point to images in registries.
- Triggers automatic builds and deployments when image versions change.

## Build Triggers
- **Webhook Triggers**: API requests initiated by events like new commits.
- **Image Change Triggers**: Start builds when base images are updated.
- **Configuration Change Triggers**: Initiate builds upon new BuildConfig creation.

## BuildConfig Process Steps
1. Define BuildConfig name and run policy (Serial or Parallel).
2. Specify triggers for automatic build initiation.
3. Set source type (Git, Dockerfile, binary).
4. Choose build strategy (S2I, Docker, Custom).
5. Determine output repository for the built image.
6. (Optional) Configure post-commit build hooks.

## Build Strategies Explained
- **Source-to-Image (S2I)**: Merges source code with builder image without Dockerfile.
- **Docker Build**: Requires Dockerfile; OpenShift runs `docker build`.
- **Custom Build**: For specialized outputs; requires custom builder image.

## Automation in CI/CD
- CI/CD automates merging, building, testing, and deploying to various environments.

## Summary
- Builds convert source inputs into deployable images.
- BuildConfig file is crucial for defining the build process.
- ImageStreams and Build Triggers help automate the build process.
- S2I, Docker, and Custom are the primary build strategies in OpenShift.

# Operators

## Definition and Purpose
- **Operator**: A method to automate cluster tasks; acts as a custom controller to extend the Kubernetes API.
- **Purpose**: Automate application creation, configuration, and management via real-time decisions.

## Components
- **Custom Controllers**: Extend Kubernetes API, working alongside CRDs.
- **Custom Resource Definitions (CRDs)**: Extend Kubernetes functionality, modularizing the API.
- **Operator Pattern**: Combination of CRDs and custom controllers, offering a declarative API.
- **Operator Hub**: A web console to find and install Operators.
- **Operator Framework**: Includes tools like the Operator SDK for building Operators and the Operator Lifecycle Manager (OLM) for management.
- **Operator Maturity Model**: Phases from Basic Install to Auto Pilot, indicating sophistication of the Operator's logic.

## Operators vs. Service Brokers
- **Operators**: 
  - Long-running processes
  - Continuous operations (upgrades, failover, scaling)
  - On-cluster and off-cluster services
- **Service Brokers**: 
  - Short-running processes
  - Operations limited to installation time
  - Primarily off-cluster services

## CRDs and Custom Controllers
- **CRDs**: Store and retrieve Kubernetes API objects, accessible using `kubectl`.
- **Custom Controllers**: Reconcile actual cluster state with the configured state from CRDs.

## Operator Framework and Tools
- **Operator SDK**: Facilitates Operator building without deep Kubernetes API knowledge.
- **Operator Lifecycle Manager (OLM)**: Manages Operator installation, upgrades, and RBAC.
- **Operator Registry**: Stores CRDs and Operator metadata.

## Operator Examples
- Deploying applications, managing resources like Secrets, ConfigMaps.
- Scaling applications using multiple replicas.
- Automating tasks like backup and restore.
- Integration with Kubernetes ecosystem tools, e.g., Istio service mesh.

## OperatorHub and Operator Types
- **OperatorHub**: Platform for one-click Operator installation.
- **Types of Operators**:
  - Red Hat Operators
  - Certified Operators from service vendors
  - Community Operators (open-source)
  - Custom Operators by users

```plaintext
// Example: Deploying an Application using an Operator
1. Create a custom resource for the application.
2. Create a custom controller for the CRD.
3. Operator logic reconciles actual and configured states.
4. CRD involves creating deployments, services, storage, etc.
5. OperatorHub allows one-click installation of Operators.
```
# Istio

## Understanding Service Mesh

- **Service Mesh**: A layer that ensures secure and reliable service-to-service communication.
  - **Functions**: Traffic management, security (encryption), and observability.

## Istio's Four Key Concepts

1. **Connection**: Manages traffic for canary deployments, A/B tests, etc.
2. **Security**: Provides authentication, authorization, and encryption.
3. **Enforcement**: Enforces policies across the services.
4. **Observability**: Allows monitoring of traffic flow and metrics.

## Benefits and Challenges of Istio with Microservices

- **Benefits**:
  - Easy updates with independent service scaling.
  - Diverse tech stacks for each service.
- **Challenges**:
  - Secure communication (encryption) needed.
  - Canary deployments and A/B testing for feature rollout.
  - Preventing cascading failures with retries and circuit breaking.

## Istio's Components

- **Control Plane**: Configures and updates proxy servers dynamically.
- **Data Plane**: Handles communication between services with Envoy proxy.

## Istio and Microservices

- **Traffic Shifting**: Gradual migration of traffic to newer service versions.
- **Request Routing**: Directs specific users to different service versions for A/B testing.
- **Security**: Protects against attacks with encryption and access control.

## Istio's Service Communication Metrics

- **Latency**: Measures the time taken for requests.
- **Traffic**: Monitors the amount of traffic a service receives.
- **Errors**: Tracks the rate of failed requests.
- **Saturation**: Gauges the overall load on the service.

---

```
// Example of Service Architecture
UI --> Ordering Service --> Inventory Service --> Database
```

---

Remember, Istio is often used in Kubernetes environments for managing complex microservices architectures. It provides a robust set of tools for traffic management, security, and observability, which are essential for modern cloud-native applications.
# Summary & Highlights

- OpenShift® is an enterprise-ready Kubernetes container platform built for open hybrid cloud.  
    
- OpenShift is easier to use, integrates with Jenkins, and has more services and features.  
    
- Custom resource definitions (CRDs) extend the Kubernetes API. 
    
- CRDs paired with custom controllers create new, declarative APIs in Kubernetes. 
    
- Operators use CRDs and custom controllers to automate cluster tasks. 
    
- A build is a process that transforms inputs into an object. 
    
- An ImageStream is an abstraction for referencing container images in OpenShift. 
    
- A service mesh provides traffic management to control the flow of traffic between services, security to encrypt traffic between services, and observability of service behavior to troubleshoot and optimize applications. 
    
- Istio is a service mesh that supports four concepts of connection, security, enforcement, and observability. It is commonly used with Microservices applications. 
    
- Istio provides service communication metrics for basic service monitoring needs: latency, traffic, errors, and saturation.


https://s9tingli-3000.theiaopenshift-0-labs-prod-theiaopenshift-4-tor01.proxy.cognitiveclass.ai

1. `kubectl run -i --tty load-generator --rm --image=busybox:1.36.0 --restart=Never -- /bin/sh -c "while sleep 0.01; do wget -q -O- https://s9tingli-3000.theiaopenshift-0-labs-prod-theiaopenshift-4-tor01.proxy.cognitiveclass.ai; done"`