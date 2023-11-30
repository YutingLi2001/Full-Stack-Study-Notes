# Container Orchestration 

## Introduction
- Container Orchestration:
  - Automates the container lifecycle of containerized applications.
  - Deployment, management, scaling, networking, and availability.
- Why it's essential:
  - Streamlines complexity.
  - Enables hands-off deployment and scaling.
  - Integrates into CI/CD workflows & DevOps.
  - Efficient resource usage.
  - Critical for "SOAR" requirements: Security, Orchestration, Automation, Response.

## Challenges Without Orchestration
- Managing a single container is easy, but scaling leads to challenges.
- Managing and scaling hundreds or thousands of containers can become chaotic.

## Key Features of Container Orchestration
1. Define container images and their registry locations.
2. Automate provisioning and deployment.
3. Secure network connections between containers.
4. Ensure availability: relocate containers during outages or resource shortages.
5. Scale and load balance containers.
6. Handle resource allocation and scheduling.
7. Rolling updates & rollbacks.
8. Conduct health checks and auto-recovery.

## Configuration and Management
- Uses configuration files in YAML or JSON.
- Configuration ensures:
  - Resource location
  - Network establishment
  - Log storage
- Schedules new container deployment to clusters.
- Manages container lifecycle based on the configuration.

## Popular Container Orchestration Tools
1. **Marathon**: Framework for Apache Mesos, scales container infrastructure.
2. **HashiCorp’s Nomad**: Supports Docker & other applications across infrastructures.
3. **Docker Swarm**: For Docker-specific environments.
4. **Kubernetes (K8s)**:
   - Developed by Google, maintained by CNCF.
   - De facto standard for container orchestration.
   - Features: deployment, storage provisioning, load balancing, self-healing.
   - Supported by major cloud providers with managed services.

## Benefits of Container Orchestration
1. **Increased Productivity**: Focus on application improvements.
2. **Faster Deployments**: Rapid container & app deployment.
3. **Reduced Costs**: Containers use fewer resources.
4. **Stronger Security**: Resource sharing & process isolation.
5. **Easier Scalability**: Scale with a single command.
6. **Faster Error Recovery**: Auto-detection & resolution.

## Summary
- Managing a vast number of containers is challenging.
- Container orchestration offers automated lifecycle management.
- Popular tools: Marathon, Nomad, Docker Swarm, Kubernetes.
- Benefits: Enhanced productivity, speed, cost-efficiency, security, and recovery.

# Introduction to Kubernetes 

## Overview
- Kubernetes:
  - Open-source system for automating deployment, scaling, and management of containerized apps.
  - Developed by Google, now maintained by the Cloud Native Computing Foundation.
  - Portable across clouds and on-premises.
  - Recognized as the "go-to" container orchestration solution.

## What Kubernetes is NOT
- Not an all-inclusive platform as a service (PaaS).
- Not opinionated; supports diverse workloads.
- Doesn't provide CI/CD pipelines or deploy source code.
- Doesn't prescribe logging, monitoring, or alerting solutions.
- Doesn't provide built-in middleware, databases, or other services.

## Core Kubernetes Concepts
1. **Pods**: Smallest deployable compute objects.
2. **Services**: Expose applications running on sets of Pods.
3. **Storage**: Supports both persistent and temporary storage.
4. **Configuration**: Provisions resources for configuring Pods.
5. **Security**: Enforces Pod and API access security.
6. **Policies**: Ensure Pods are matched to Nodes.
7. **Scheduling and Eviction**: Manages Pods on resource-limited Nodes.
8. **Preemption**: Prioritizes and terminates lower priority Pods for higher ones.
9. **Cluster Administration**: Details to create/administer a cluster.

## Kubernetes Capabilities
1. Automated rollouts and rollbacks.
2. Storage orchestration.
3. Horizontal scaling.
4. Automated bin packing: Efficiently places containers based on resource requirements.
5. Secret & Configuration management: Manages sensitive data without rebuilding images.
6. IP handling: Assigns both IPv4 and IPv6 addresses.
7. Batch execution and CI workload management.
8. Self-healing: Auto-repairs failing/unresponsive containers.
9. Service discovery & Load balancing.
10. Designed for extensibility.

## Kubernetes Ecosystem
- The ecosystem supports various tasks for running containerized applications.
  1. Building container images.
  2. Storing images in a registry.
  3. Application logging & monitoring.
  4. CI/CD capabilities.

- Key Players in the Ecosystem:
  - **Public Cloud Providers**: Prisma, IBM, Google, AWS.
  - **Framework Providers**: Red Hat, VMWare, SUSE, Mesosphere, Docker, Cloud Foundry.
  - **Management Providers**: Digital Ocean, loodse, SUPERGIANT, etc.
  - **Tool Providers**: Jfrog, Univa, Aspen Mesh, Bitnami, Cloud 66.
  - **Monitoring & Logging**: sumalogic, DATADOG, New Relic, Grafana, etc.
  - **Security Providers**: GUARDCORE, BLACKDUCK, yubico, etc.
  - **Load Balancing Providers**: AVI networks, VMware, NGiNX.

## Summary
- Kubernetes is a flexible, open-source container orchestration platform.
- Key Concepts: Pods, Services, Storage, Configuration, Security, Scheduling.
- Capabilities: Rollouts, Storage, Scaling, IP Handling, Self-healing, Load balancing.
- A vast ecosystem surrounds Kubernetes, including cloud providers, tools, security, and more.

# Kubernetes Architecture 

## Overview
- Kubernetes Cluster: A deployment of nodes running containerized applications.
  - Master Node: Kubernetes Control Plane.
  - Worker Nodes: Run user applications.

## Control Plane Components
- **Kubernetes API Server (kube-apiserver)**
  - Front-end of the control plane.
  - Scales horizontally.
- **Etcd**
  - Distributed key-value store.
  - Contains all cluster data.
  - Ensures actual state matches desired state.
- **Kubernetes Scheduler (kube-scheduler)**
  - Assigns Pods to nodes.
  - Selects optimal node based on resources and scheduling principles.
- **Kubernetes Controller Manager**
  - Runs controller processes.
  - Ensures cluster state matches desired state.
- **Cloud Controller Manager**
  - Interfaces with cloud provider APIs.
  - Allows Kubernetes and cloud providers to evolve independently.

## Worker Plane Components
- **Nodes**
  - Can be virtual or physical machines.
  - Managed by the control plane.
  - Runs applications and Kubernetes components.
- **Pods**
  - Smallest deployable units in Kubernetes.
  - Contains one or more containers sharing the node's resources.
- **Kubelet**
  - Manages Pods and containers on a node.
  - Communicates with API server.
  - Reports Pods' health and status.
- **Container Runtime**
  - Downloads images and runs containers.
  - Supports pluggability with Container Runtime Interface (CRI).
  - Examples: Docker, Podman, Cri-o.
- **Kubernetes Proxy (kube-proxy)**
  - Network proxy on each node.
  - Manages network rules for pod communication.

## Key Concepts
- Kubernetes runs on various infrastructures via cloud providers.
- Control Plane acts like a thermostat: setting desired state and regulating the system to maintain it.
- Worker Plane runs the components and user applications.
- Communication within the cluster is through the Kubernetes API

# Kubernetes Objects – Part 1 

## Overview
- Define Kubernetes objects and properties.
- Describe basic Kubernetes objects and features.
- Demonstrate how Kubernetes objects relate to each other.

## Kubernetes Objects
- **Kubernetes Object:** Persistent entity with identity, state, and behavior.
- **Examples:** Pods, Namespaces, ReplicaSets, Deployments.
- **Consists of:**
  - **Object Spec:** Provided by the user, dictates the desired state.
  - **Status:** Provided by Kubernetes, describes the current state.
- **Kubernetes Goal:** Match current state to desired state.

## Working with Kubernetes Objects
- **Kubernetes API:** Interface to interact with objects.
- **Client Libraries:** For programming language interaction.
- **kubectl:** Command-line tool for object management.

## Identification and Grouping
- **Labels:** Key/value pairs for object identification (not unique).
- **Label Selectors:** Core grouping method, identifies a set of objects.

## Namespaces
- **Purpose:** Isolate groups of resources within a single cluster.
- **Use Cases:** Multiple teams/projects, cluster sharing, resource isolation.
- **Uniqueness:** Object names must be unique within a namespace.
- **Examples:** `kube-system` (system use), `default` (user applications).

## Core Kubernetes Objects
### Pods
- **Definition:** Smallest deployable unit, represents a single application instance.
- **Composition:** Typically one or more containers.
- **Scaling:** Horizontal scaling via Pod replication.

### YAML Example for Pod
```yaml
kind: Pod
spec:
  containers:
  - name: nginx
    image: nginx
    ports:
    - containerPort: 80
```

### ReplicaSets
- **Purpose:** Manage sets of identical, horizontally scaled Pods.
- **Configuration:** Different from Pods; specifies desired replica count.
- **Pod Template:** Included in the spec to define the Pod configuration.
- **Selector:** Matches labels to manage Pods.

### Deployments
- **Purpose:** Higher-level object to manage ReplicaSets and Pods.
- **Use Cases:** Stateless applications, rolling updates, version management.
- **Features:** More control and management capabilities than ReplicaSets.

### YAML Example for Deployment
```yaml
kind: Deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx
        ports:
        - containerPort: 80
```

## Advanced Deployment Strategies
- **Rolling Updates:** Allows zero-downtime updates, gradually replacing old versions with new ones.

## Recap
- **Persistent Entities:** Kubernetes objects with desired and current states.
- **Namespaces:** For resource isolation within a cluster.
- **Pods:** Basic unit of deployment, representing an app instance.
- **ReplicaSets:** Manages a set of Pods.
- **Deployments:** Updates and scales Pods and ReplicaSets, suitable for stateless applications.

# Kubernetes Objects – Part 2 

## Service in Kubernetes
- **Purpose:** Provides a stable IP and DNS name for a set of Pods.
- **Properties:** Load balances across Pods, supports multiple protocols and ports.
- **Uses:** Enables service discovery and communication within a cluster.

## Types of Services
1. **ClusterIP:**
   - **Default Service:** Accessible only within the cluster.
   - **Use Case:** Inter-service communication within a cluster.

2. **NodePort:**
   - **Extension of ClusterIP:** Exposes the service on each Node’s IP at a static port.
   - **Use Case:** Publicly accessible services, although not recommended for production security-wise.

3. **LoadBalancer:**
   - **Extension of NodePort:** Uses an external load balancer to route traffic to the NodePort and ClusterIP services.
   - **Use Case:** Exposing services to the internet, often used in cloud environments.

4. **ExternalName:**
   - **Maps to DNS name:** Does not use selectors, instead maps a Service to the `spec.externalName` field.
   - **Use Case:** Represents external services and facilitates inter-namespace communication.

## Ingress
- **API Object + Controller:** Manages external access to services.
- **Properties:** Provides routing rules, typically exposes services on HTTP/HTTPS ports.
- **Use Case:** Used when a single entry point to multiple services is needed.

## DaemonSet
- **Objective:** Ensure that all (or some) Nodes run a copy of a specified Pod.
- **Properties:** Adds Pods to new Nodes, removes from decommissioned Nodes.
- **Use Case:** Ideal for running system daemons like log collectors, monitoring agents.

## StatefulSet
- **Purpose:** Manages stateful applications.
- **Properties:** Handles deployment, scaling of Pods, maintains a sticky identity, and provides persistent storage volumes.
- **Use Case:** Databases and any application where the identity or state needs to be preserved.

## Job
- **Objective:** Execute Pods that are expected to terminate successfully after completing a task.
- **Properties:** Tracks Pod completions, retries on failures.
- **Use Case:** Batch processing, one-off tasks.

## CronJob
- **Based On:** Jobs, but executed on a scheduled time.
- **Use Case:** Regularly scheduled tasks like backups, report generation.

## Recap
- **Services:** Provide a consistent way to access Pods.
- **Ingress:** Manages external access with routing rules.
- **DaemonSet:** Ensures Pods run on all Nodes.
- **StatefulSet:** Manages stateful applications with unique identities and persistent storage.
- **Jobs/CronJobs:** Manage Pods that perform tasks and can be scheduled to run at specific times.

# Using Kubectl 

## What is Kubectl?
- **Definition:** Kubernetes Command Line Interface (CLI).
- **Functionality:** Deploys applications, manages cluster resources, views logs, etc.
- **Alias:** Kube Command Tool Line.

## Kubectl Command Structure
- **Order:** `kubectl <command> <type> <name> <flags>`
  - **Command:** The operation, e.g., `create`, `get`, `apply`, `delete`.
  - **Type:** The resource type, e.g., `pod`, `deployment`, `ReplicaSet`.
  - **Name:** The resource name (if applicable).
  - **Flags:** Options/modifiers to adjust default behavior.

## Command Types
1. **Imperative Commands:**
   - **Direct:** Create, update, and delete objects with specific instructions.
   - **Advantages:** Easy to learn and quick to run.
   - **Disadvantages:** No audit trail, limited flexibility, not ideal for production.

2. **Imperative Object Configuration:**
   - **Template-based:** Use YAML/JSON files for object definitions.
   - **Advantages:** Reproducible setups, version control friendly, and audit trails.
   - **Disadvantages:** Requires schema knowledge and file management.

3. **Declarative Object Configuration:**
   - **State-focused:** Configuration files define the desired state.
   - **Advantages:** Kubernetes automatically applies necessary operations, ideal for production.
   - **Disadvantages:** May have a learning curve for writing and managing configuration files.

## Common Kubectl Commands
- `get`: Lists resources.
- `delete`: Removes resources.
- `autoscale`: Implements autoscaling.
- `apply`: Applies changes from configuration files.
- `scale`: Adjusts the number of replicas.

## Examples
- **List Services:** `kubectl get services`
- **Delete Pod:** `kubectl delete pod <pod_name>`
- **Autoscale Deployment:** `kubectl autoscale deployment <deployment_name> --min=2 --max=5`
- **Apply Configuration:** `kubectl apply -f ./configs/`
- **Scale ReplicaSet:** `kubectl scale --replicas=3 replicaset <replicaset_name>`

## Creating Deployments
- **Command:** `kubectl apply -f <file_name>`
- **Output:** Confirms creation and status of resources like deployments, pods, etc.

## Conclusion
- Kubectl is essential for interacting with Kubernetes clusters.
- Different command types offer flexibility between ease of use and configuration management.
- Declarative object configuration is recommended for production due to its scalability and ease of management.