# Introduction to Containers

## Overview
- **Goals**: 
  - Understand traditional software development challenges.
  - Define and understand characteristics of containers.
  - Recognize benefits and challenges of containers.
  - Familiarize with leading container vendors.
- **Key Concept**: Cloud-native development uses containers for scalable, dynamic, hybrid cloud-friendly software.

## Analogy: Shipping Container
- **Shipping Industry**: Standardized container sizes.
- **Benefits**: Improved efficiency and transport flexibility.

## Containers in Tech
- **Purpose**: Ensure software portability across platforms.
- **Definition**: A unit of software encapsulating code, runtime, tools, libraries, and settings.
- **Advantages**:
  - Address underlying infrastructure issues.
  - Move apps between environments (laptop, testing, production, VMs, clouds) with reliability.

## Traditional Computing Challenges
- **Isolation**: Can't separate apps and allocate dedicated resources.
- **Server Utilization**: Often under or overutilized.
- **Provisioning & Maintenance**: Expensive and comprehensive.
- **Scalability**: Limited by physical server constraints.
- **Portability**: Incompatibility across environments/OSs.
- **Hardware Resiliency**: Time-consuming, complex, and costly.
- **Automation**: Difficult across multiple platforms.

## Container Benefits
- **Virtualization**: Container engines virtualize OS.
- **Characteristics**:
  - Lightweight, fast, isolated, portable, and secure.
  - Platform and OS independent.
  - Language and IDE independent.
- **Advantages**:
  - Facilitate quick deployment.
  - Optimize resource utilization (CPU, memory).
  - Seamless porting across environments.
  - Support for next-gen apps (e.g., microservices).

## Container Challenges
- **Server Security**: Vulnerabilities if OS is compromised.
- **Management**: Challenges with managing numerous containers.
- **Legacy Migration**: Complexity in transforming monolithic apps.
- **Right-Sizing**: Adjusting containers for specific scenarios.

## Popular Container Vendors
- **Docker**: Leading container platform.
- **Podman**: More secure, daemon-less engine.
- **LXC**: Chosen for data-intensive operations.
- **Vagrant**: Provides maximum isolation.

## Recap
- Containers help overcome challenges in isolation, utilization, provisioning, etc.
- A **container** encapsulates everything necessary for software application deployment.
- **Key Features**: OS, language, and platform independence; automation, resource optimization.
- **Challenges**: Management, migration, sizing.
- **Top Vendors**: Docker, Podman, LXC, Vagrant.

# Introduction to Docker

## Overview
- **Goals**: 
  - Define Docker.
  - Understand Docker's underlying process and technology.
  - Enumerate benefits and challenges of Docker containers.

## Docker Defined
- **Official Definition**: Open platform for developing, shipping, and running applications as containers.
- **Popularity**: 
  - Simple architecture.
  - Scalability and portability across platforms and environments.
- **Isolation**: Docker separates applications from infrastructure, such as hardware, OS, and container runtime.
- **Technical Details**: 
  - Written in Go programming language.
  - Uses Linux kernel features.
  - Leverages namespaces for isolated workspaces (containers). Each container runs in a distinct namespace.

## Innovations Inspired by Docker
- **Complementary Tools**: Docker CLI, Docker Compose, Prometheus.
- **Plugins**: Various, including storage plugins.
- **Orchestration Technologies**: Docker Swarm, Kubernetes.
- **Development Methodologies**: Microservices, serverless.
# Building and Running Containers

## Overview
- **Goals**: 
  - Build a container image using a Dockerfile.
  - Create a running container from an image.
  - Understand essential Docker commands.

## Development Process of a Running Container
1. Create a **Dockerfile**.
2. Use the Dockerfile to **generate a container image**.
3. Use the image to **initiate a running container**.

## Sample Dockerfile
```Dockerfile
FROM <base_image>
CMD ["echo", "Hello World!"]
```
- **FROM**: Sets the base image.
- **CMD**: Executes commands, here it prints "Hello World!".

## Building an Image
```bash
docker build -t my-app:v1 .
```
- **build**: Docker command to construct an image.
- **-t**: Tag the image with a name and version.
- **my-app:v1**: Repository and tag.
- **.**: Current directory (location of Dockerfile).

**Output Messages**:
- Sending build context to Docker daemon.
- Successfully built `<image id>`.
- Successfully tagged my-app:v1.

To **check created images**:
```bash
docker images
```

## Creating a Running Container
```bash
docker run my-app:v1
```
- Outputs "Hello, World!".
- To **view details** of the created container:
```bash
docker ps -a
```

## Key Docker Commands
- **build**: Craft container images from a Dockerfile.
- **images**: List all available images.
- **run**: Generate and start a container from an image.
- **push**: Store images in a designated registry.
- **pull**: Retrieve images from a specified registry.

## Recap
- **Docker Build**: Craft container images using a Dockerfile.
- **Docker Run**: Start a container using an image.
- **Essential Dockerfile Commands**: build, images, run, pull, and push.

## Benefits of Docker
- **Consistency**: Offers stable application deployments.
- **Speed**: Quick deployments, lightweight images.
- **Development Process**: Reusable images speed up development.
- **Automation**: Minimizes errors and simplifies maintenance.
- **Supports Practices**: Agile, CI/CD DevOps.
- **Versioning**: Accelerates testing, rollbacks, redeployments.
- **Application Management**: Easy refresh, cleanup, repair.
- **Collaboration**: Quick issue resolution, container scaling.
- **Portability**: Platform-independent images.

## Docker's Limitations
Docker may not be suitable for applications that:
- Require high performance or security.
- Are based on a monolithic architecture.
- Use rich GUI features.
- Perform standard desktop or limited functions.

## Recap
- **Docker**: Open platform for containerized applications.
- **Key Features**: Speeds up deployment, uses namespace technology for isolation, supports Agile and CI/CD DevOps.
- **Considerations**: Not ideal for monolithic, high-performance, or security-intensive applications.

# Introduction to Docker Objects

## Overview
- **Goals**:
  - Identify and describe Docker objects.
  - Recognize essential Dockerfile commands.
  - Understand container image naming format.
  - Explain how Docker uses networks, storage, and plugins.

## Docker Objects
- **Dockerfile**: A text file with instructions to create an image.
- **Images**: Read-only templates to create Docker containers.
- **Container**: A runnable instance of an image.
- **Network**: Isolates container communications.
- **Storage Volumes**: Persists data even after a container stops running.
- **Plugins and Add-ons**: Extend Docker's functionality.

## Dockerfile Instructions
- **FROM**: Defines a base image (e.g., OS or programming language).
- **RUN**: Executes commands.
- **CMD**: Specifies the default command for execution. Only one CMD should exist in a Dockerfile.

## Docker Images
- Created from Dockerfile instructions.
- Images consist of **layers**. Each Docker instruction generates a new layer.
- **Layer Reuse**: Only the changed layers are rebuilt, saving disk space and network bandwidth.
- A writeable container layer is added to read-only layers when creating a container.

## Image Naming Format
- **Hostname**: Identifies the image registry (e.g., docker.io).
- **Repository**: Group of related container images.
- **Tag**: Provides details about an image's specific version or variant.
- Example: `docker.io/ubuntu:18.04`.

## Docker Containers
- Runnable instances of images.
- Can be created, started, stopped, or deleted using the Docker API or CLI.
- Highly isolated from other containers and the host machine.

## Docker Networks
- Ensures container communication remains isolated.

## Docker Storage
- **Volumes & Bind Mounts**: Enables data persistence beyond the container's lifecycle.

## Docker Plugins
- **Storage Plugins**: Facilitate connections to external storage platforms.

## Recap
- **Docker Objects**: Dockerfiles, images, containers, networks, storage volumes, plugins, and add-ons.
- **Essential Dockerfile Instructions**: FROM, RUN, and CMD.
- **Docker Containers**: Runnable instances of images.
- **Image Name Format**: Consists of hostname, repository, and tag.
- **Docker Networks**: Used to isolate container communications.
- **Docker Storage**: Uses volumes and bind mounts for data persistence.
- **Plugins**: Like storage plugins, connect to external storage platforms.



# Docker Architecture 

## Docker Components

1. **Client-Server Architecture**
   - **Docker Client**:
     - Communicates via Docker Command Line Interface or REST APIs.
     - Can communicate with local and remote Docker hosts.
     - Sends instructions to Docker host server (host).
   - **Docker Host (Server)**:
     - Contains `dockerd` (daemon) which processes Docker commands.
     - Does the heavy lifting to build, run, and distribute containers.
     - Manages:
       - Images
       - Containers
       - Namespaces
       - Networks
       - Storage
       - Plugins and add-ons.
     - Docker daemons can communicate with other daemons to manage services.
   - **Registry**:
     - Stores container images.
     - Access can be public (e.g., Docker Hub) or private.
     - Hosted using third-party providers (like IBM Cloud Container Registry) or self-hosted.

## Docker Containerization Process

1. **Creating a Container Image**:
   - Start with a base image or a Dockerfile.
   - Use the `build` command to create a container image.
   - Use the `push` command to store the image in the registry.
2. **Running a Container**:
   - Use the `run` command with the image name.
   - Host checks locally for the image.
   - If not found, Docker client pulls the image from the registry.
   - Daemon creates a running container using the image.

## Summary

- Docker architecture includes:
  - Docker Client
  - Docker Host with `dockerd` daemon
  - Registry
- Docker Client interacts with Docker Host using commands and REST APIs.
- Docker Host manages various components and processes commands.
- Containerization involves building, pushing, and running an image to get a running container.

```docker
# Example Commands (based on context)
docker build -t image_name .
docker push image_name:tag
docker run image_name:tag
```


# ==Summary & Highlights==

- A container is a unit of software that encapsulates everything needed to build, ship, and run applications.  
    
- Containers lower deployment time and costs, improve utilization, automate processes, and support next-gen applications (microservices). Major container vendors include Docker, Podman, LXC, and Vagrant. 
    
- Docker is an open platform used for developing, shipping, and running applications as containers. 
    
- Docker containers are not a good fit for applications based on monolithic architecture or applications that require high performance or security. 
    
- Docker architecture consists of the Docker client, the Docker host, and the container registry. 
    
- The Docker host contains objects such as the Dockerfiles, images, containers, networks, storage volumes, and other objects, such as plugins and add-ons. 
    
- Docker uses networks to isolate container communications. 
    
- Docker uses volumes and binds mounts to persist data even after a container stops running. 
    
- Plugins, such as storage plugins, provide the ability to connect to external storage platforms.

