# ReplicaSet 

## What is a ReplicaSet?
- **Definition:** A ReplicaSet is a Kubernetes feature that maintains a stable set of replica Pods running at any given time.
- **Purpose:** It ensures that a specified number of pod replicas are running at all times.

## Functionality of a ReplicaSet
- **Scaling:** Automatically adds or deletes pods to match the desired number of replicas.
- **Redundancy:** Provides high availability and eliminates single points of failure.
- **Self-Healing:** Replaces failing pods to maintain the desired state.
- **Deployment Management:** Often created and managed by a Kubernetes Deployment for updates and rollbacks.

## Benefits of Using a ReplicaSet
1. **High Availability:** Ensures that there are always a defined number of pods running.
2. **Fault Tolerance:** Minimizes downtime by quickly replacing failed pods.
3. **Scalability:** Dynamically accommodates varying loads by adjusting the number of running pods.
4. **Load Distribution:** Allows for load balancing across multiple pods.

## Managing ReplicaSets
- **Recommended Practice:** Use Deployments rather than managing ReplicaSets directly.
- **Labels:** ReplicaSets use labels to manage pods, where each pod must have a set of labels that the ReplicaSet can identify and manage.
- **Creation:** Can be created with `kubectl apply` using a YAML file that defines the ReplicaSet configuration.

## Command Examples
- **Check ReplicaSet:** `kubectl get ReplicaSet`
- **Create Deployment (which creates a ReplicaSet):** `kubectl create -f deployment.yaml`
- **Scaling:** `kubectl scale --replicas=3 deployment/hello-Kubernetes`
- **Delete Pod:** `kubectl delete pod <pod-name>`

## Desired State Management
- **Automatic Adjustment:** If a pod fails or is deleted, the ReplicaSet creates a new one to maintain the desired number of replicas.
- **Over-provisioning:** If there are too many pods, the ReplicaSet will remove the excess pods to achieve the desired state.

## Use Cases
- **Creating ReplicaSets:** Typically done via a Deployment for ease of management.
- **Scaling:** Can be manually adjusted or automatically managed via autoscaling tools.
- **Maintaining State:** Constantly checks and adjusts the number of pods to match the desired state set by the user.

## Best Practices
- **Use Deployments:** It is recommended to manage ReplicaSets through Deployments for better lifecycle management and ease of updating pods.

## Summary
- A ReplicaSet is a fundamental component for ensuring reliability and scalability in Kubernetes environments.
- It's designed to handle the lifecycle of pods and their replicas, maintaining the desired state.
- While it's possible to work with ReplicaSets directly, the best practice is to manage them through Deployments for better control over rolling updates and rollbacks.

# Autoscaling 

## Definition and Benefits
- **Autoscaling**: Automatically scales a cluster in line with demand.
- **Optimizes resource usage** and costs.
- Works at **two levels**: cluster/node level and pod level.

## Autoscaler Types in Kubernetes
1. **Horizontal Pod Autoscaler (HPA)**
   - Scales the number of pod replicas.
   - Responds to changes in CPU or memory usage.
   - Example: Scaling up from 1 to 3 pods during peak load.

2. **Vertical Pod Autoscaler (VPA)**
   - Scales the resource requests and limits of pods.
   - Adjusts CPU and memory resources of the pods.
   - Example: Increasing resources at 11 am during peak demand.

3. **Cluster Autoscaler (CA)**
   - Scales the number of nodes in the cluster.
   - Acts when pods fail to schedule or when demand changes significantly.
   - Example: Adding/removing nodes based on the load.

## Creating Autoscaling
- Use the `autoscale` command with attributes:
  - **Min**: Minimum number of pods.
  - **Max**: Maximum number of pods.
  - **CPU-percent**: Triggers new pod creation at a certain CPU usage.

## Horizontal Pod Autoscaler (HPA) Operation
- **Scales out** (increases/decreases pod count) based on application usage.
- Controlled by cluster operator with metrics targets.
- Can be manually created with a YAML file:
  ```yaml
  apiVersion: autoscaling/v1
  kind: HorizontalPodAutoscaler
  metadata:
    name: example-hpa
  spec:
    scaleTargetRef:
      apiVersion: apps/v1
      kind: Deployment
      name: example-deployment
    minReplicas: 2
    maxReplicas: 5
    targetCPUUtilizationPercentage: 50
  ```

## Vertical Pod Autoscaler (VPA) Operation
- **Scales up** (increases/decreases resources of existing pod) based on application usage.
- Sets targets for metrics (CPU, memory).
- **Not to be used with HPA** on the same resource metrics.

## Cluster Autoscaler (CA) Operation
- Scales the cluster by adding/removing nodes.
- Works in tandem with HPA or VPA for pod scaling.
- Ensures compute power meets the task requirements without overpaying.

## Best Practices
- Use a combination of autoscalers for optimal performance and cost.
- Analyze specific scenarios to select the appropriate autoscaler type.
- Avoid using VPA with HPA on the same metrics (CPU, memory).

## Key Takeaways
- Autoscaling allows for flexibility and cost optimization.
- Kubernetes provides three types of autoscalers to handle different scaling needs.
- The combination of HPA, VPA, and CA can lead to a stable and cost-efficient environment.

# Deployment Strategies

## Overview
- Purpose: Automate application lifecycle, maintain object state, minimize risk.
- Uses: Deploy/update/rollback objects, pause/resume, scale deployments.

## Deployment Strategies
### 1. Recreate Strategy
- Steps: Shutdown v1 Pods, create v2 Pods, reverse for rollback.
- Pros: Simple, complete replacement.
- Cons: Downtime during switch.

### 2. Rolling (Ramped) Strategy
- Steps: Replace v1 Pods with v2 one by one, repeat until all are updated.
- Pros: Minimal downtime, stateful app suitable.
- Cons: Time-consuming, no traffic control.

### 3. Blue/Green Strategy
- Steps: Create identical prod env., test new version, switch traffic.
- Pros: Zero downtime, instant rollout.
- Cons: High cost, testing complexity, stateful app challenges.

### 4. Canary Strategy
- Steps: Route some traffic to v2, test and iterate, then full rollout.
- Pros: Reliable monitoring, quick rollback.
- Cons: Slow rollout.

### 5. A/B Testing Strategy
- Steps: Route certain users to v2 based on traits, analyze, full rollout.
- Pros: Parallel versioning, traffic control.
- Cons: Troubleshooting complexity, requires advanced load balancing.

### 6. Shadow Strategy
- Steps: Deploy shadow version, receive same traffic without impacting users.
- Pros: Real traffic testing, no user impact.
- Cons: High cost, complex, potential misinterpretation.

## Deployment Strategies Summary
- **Recreate**: Full replacement, noticeable downtime.
- **Ramped**: Incremental update, no downtime, slow.
- **Blue/Green**: Instant switch, costly, no downtime.
- **Canary**: Gradual rollout to all, traffic testing, zero downtime.
- **A/B Testing**: Targeted user testing, full control, complex setup.
- **Shadow**: Real traffic, no response to users, no impact.

## Strategy Selection Considerations
- **Product Type and Audience**: Choose based on application complexity and user sensitivity.
- **Real User Requests**: Shadow and Canary involve live traffic without impacting all users.
- **Feature Changes**: A/B is for minor/UI changes, Canary for gradual exposure.
- **Complex/Critical Apps**: Blue/Green for thorough monitoring, zero downtime.
- **Non-Critical Apps**: Recreate for simplicity despite short downtime.

## Key Selection Criteria
- Zero Downtime: Ramped, Blue/Green, Canary, A/B Testing, Shadow.
- Real Traffic Testing: Canary, Shadow.
- Targeted Users: A/B Testing.
- Cloud Cost: High for Blue/Green and Shadow.
- Rollback Duration: Varies, quickest with Blue/Green.
- User Impact: None for Blue/Green, Canary, A/B Testing, Shadow.
- Setup Complexity: High for A/B Testing and Shadow.

# Rolling Updates

## Understanding Rolling Updates
- **Definition**: Automated, controlled app changes deployed across pods on a schedule.
- **Compatibility**: Works with pod templates like deployments.
- **Rollback**: Changes can be reverted if needed.

## Pre-Steps for Rolling Updates
1. **Add Probes**: Insert liveness and readiness probes to deployments.
2. **Rolling Update Strategy**: Define a strategy in the YAML file.
   - **Example Strategy**:
     - **Desired pods**: 10
     - **Minimum availability**: 50%
     - **maxSurge**: 2 (only two pods can be added beyond the desired number)
     - **maxUnavailable**: 0 (for zero-downtime)
     - **100% maxSurge**: Creates a complete replica set before the old one is taken down.
     - **minReadySeconds**: Adds a delay before updating the next pod.

## Implementing Rolling Updates
- **Updating an Application**:
  1. **Build, tag, and upload** the new Docker image to Docker Hub.
     - Example tag: `upkar/hello-kubernetes:2.0`
  2. **Apply the new image** to the deployment.
  3. **Verify the update** using `kubectl rollout status`.
  4. **Check the application**: New message "Hello world v2!" should be visible.

## Rolling Back Updates
- **Commands for Rollback**:
  - Use `kubectl rollout undo` to revert changes.
  - Confirm rollback with `kubectl get pods`.

## Rolling Update Strategies
- **All-at-Once Rollout/Rollback**:
  - Replace all old pods with new ones simultaneously.
  - User access is temporarily blocked during the swap.
- **One-at-a-Time Rollout/Rollback**:
  - Update pods one at a time.
  - No interruption in user access.

## Key Takeaways
- Rolling updates ensure app changes without downtime.
- Rollbacks are straightforward in Kubernetes.
- Strategies for updates and rollbacks include all-at-once or one-at-a-time.

# ConfigMaps and Secrets

## ConfigMap Essentials
- **Purpose**: Stores non-confidential data in key-value pairs.
- **Use Case**: Keep configuration separate from application code.
- **Size Limit**: Data cannot exceed 1 megabyte.
- **Fields**: 
  - `data` for string data.
  - `binaryData` for binary data.
  - No `spec` field; uses valid DNS subdomain names.
- **Flexibility**: Reusable across multiple deployments.

## Creating ConfigMaps
1. **String Literals**: Create with key-value pairs directly in the command.
2. **Properties File**: Utilize an existing file containing `key=value` pairs.
3. **YAML Descriptor**: Apply a YAML file with the ConfigMap configuration.

## Consuming ConfigMaps in Deployments
- **Environment Variables**: Use `configMapKeyRef` to reference ConfigMap data.
- **Volume Mounts**: Mount ConfigMap data as a file using volumes.

## Secrets Overview
- Similar to ConfigMaps, but for storing sensitive information.
- Encoded and not displayed in plaintext.
- Size should be limited for efficiency.

## Creating Secrets
1. **String Literals**: Direct creation with literals using Kubernetes commands.
2. **Environment Variables**: Use existing environmental variables to create secrets.
3. **Volume Mounts**: Deploy secrets as files using volumes in pods.

## Using ConfigMaps and Secrets in Deployment
- **Deployment Descriptor Updates**: Add environment sections pointing to ConfigMaps or Secrets.
- **File-based Configurations**: Can mount an entire directory or specific files as a ConfigMap or Secret.
- **YAML-based Applications**: Apply configuration using a YAML file for both ConfigMaps and Secrets.

## Practical Examples
- **Deployment**: Update applications dynamically by changing ConfigMap or Secret without altering the code.
- **Node.js Usage**: Access variables through `process.env.VARIABLE_NAME`.
- **Secrets in Files**: Mount secrets to a file path for applications to read.
- **Verifications**: Use `kubectl describe` and `kubectl get` to confirm configurations.



# Service Binding

## Definition & Goals
- **Service Binding**: The process of consuming external services (like REST APIs, databases, event buses) in applications.
- **Goals**:
  - Manages configuration and credentials for back-end services.
  - Protects sensitive data by making service credentials available as a Kubernetes Secret.

## Binding to Kubernetes Cluster
- **Process**:
  1. **Provision** an instance of the service.
  2. **Bind** the service to your Kubernetes Cluster.
  3. **Create Service credentials** using the public cloud service endpoint.
  4. **Store credentials** in a Kubernetes Secret.
  5. **Configure app** to access the credentials in the Kubernetes Secret.

## IBM Cloud Service Example: Tone Analyzer
- **Steps**:
  1. Provision a Tone Analyzer service instance via CLI or IBM Cloud catalog.
  2. Bind the service instance to your Cluster using `service bind` command.
  3. IBM Cloud Service binding creates a Kubernetes Secret with encoded credentials.

## Commands to Retrieve Secrets
- List all Secrets: `kubectl get secrets`
- Access Secret data:
  - **Mount as Volume**: Creates a JSON file with credentials in the Pod.
  - **Reference in Environment Variables**: Use variables like `binding.APIkey`, `binding.username`, `binding.password`.

## Code Example
```javascript
// Node.js application using environment variables for service credentials
const express = require('express');
const app = express();

// Use environment variables binding.APIkey, binding.username, binding.password
```

## Key Takeaways
- Service binding simplifies the use of external services by managing credentials.
- Automatically provides credentials within application code when bound to a deployment.
- Options to consume secrets:
  - **Volume Mounts**: For file-based credential access.
  - **Environment Variables**: For direct access in application code.

# Summary & Highlights

Congratulations! You have completed this module. At this point, you know: 

- A ReplicaSet enables scaling by creating or deleting pods. 
    
- A ReplicaSet always tries to match the actual state to the desired state. 
    
- Autoscaling enables scaling as needed at the cluster or node level, and the pod level. 
    
- Autoscaler types include horizontal pod (HPA), vertical pod (VPA), and cluster (CA).  
    
- Rolling updates roll out app changes in a controlled and automated way. 
    
- Rolling updates and rollback can be performed using all-at-once and one-at-a-time strategies. 
    
- ConfigMaps are used to provide variables for your application. 
    
- Secrets are used to provide sensitive information to your application. 
    
- Binding an external Service to your deployment automatically provides the credentials to use the Service inside the code. 
    
- Binding manages configuration and credentials for back-end Services while protecting sensitive data.