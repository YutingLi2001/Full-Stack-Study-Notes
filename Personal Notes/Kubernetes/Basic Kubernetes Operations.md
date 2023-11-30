### 0. Configurations 
- `kubectl` requires configuration so that it targets the appropriate cluster. Get cluster information with the following command:
	- `kubectl config get-clusters`
- A `kubectl` context is a group of access parameters, including a cluster, a user, and a namespace. View your current context with the following command:
	- `kubectl config get-contexts`
- List all the Pods in your namespace. If this is a new session for you, you will not see any Pods.
	- `kubectl get pods`

### 1. Create a Pod with an imperative command
- Export your namespace as an environment variable so that it can be used in subsequent commands 
	- `export MY_NAMESPACE=sn-labs-$USERNAME`
- Find the `Dockerfile`. This is the file that will be used to build our image.
	- `docker build -t us.icr.io/$MY_NAMESPACE/hello-world:1 . && docker push us.icr.io/$MY_NAMESPACE/hello-world:1`
- Run the `hello-world` image as a container in Kubernetes.
	- `kubectl run hello-world --image us.icr.io/$MY_NAMESPACE/hello-world:1 --overrides='{"spec":{"template":{"spec":{"imagePullSecrets":[{"name":"icr"}]}}}}'`

### Get informations about your pod
- `kubectl describe pod hello-world`

### 2. Create a Pod with imperative object configuration
- Go to the `yaml` configuration file
- You need to insert your namespace where it says `<my_namespace>`. Make sure to save the file when you’re done.
- Imperatively create a Pod using the provided configuration file.
	- `kubectl create -f hello-world-create.yaml`

### 3. Create a Pod with a declarative command
- 1. Go to the `yaml` configuration file
- We are creating a Deployment (`kind: Deployment`).
- There will be three replica Pods for this Deployment (`replicas: 3`).
- The Pods should run the `hello-world` image (`- image: us.icr.io/<my_namespace>/hello-world:1`).
- Use the `kubectl apply` command to set this configuration as the desired state in Kubernetes.
	- `kubectl apply -f hello-world-apply.yaml`

### Load balancing the application
- In order to access the application, we have to expose it to the internet using a Kubernetes Service.
	- `kubectl expose deployment/hello-world`
- List Services in order to see that this service was created.
	- `kubectl get services`
- Since the cluster IP is not accessible outside of the cluster, we need to create a proxy
	- `kubectl proxy`
- Ping the application to get a response.
	- `curl -L localhost:8001/api/v1/namespaces/sn-labs-$USERNAME/services/hello-world/proxy`
	- 