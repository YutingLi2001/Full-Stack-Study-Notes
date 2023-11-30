# Pull an image from Docker Hub and run it as a container

- Use the `docker` CLI to list your images.
	- `docker images`
- Pull your first image from Docker Hub.
	- ``docker pull hello-world``
- Run the `hello-world` image as a container.
	- `docker run hello-world`
- List the containers to see that your container ran and exited successfully.
	- `docker ps -a`
	- It should show like:
```
CONTAINER ID   IMAGE         COMMAND    CREATED              STATUS                          PORTS     NAMES
fc17ec09fbc4   hello-world   "/hello"   About a minute ago   Exited (0) About a minute ago             festive_gagarin
```
- Note the CONTAINER ID from the previous output and replace the **<container_id>** tag in the command below with this value. This command ==removes== your container.
	- `docker container rm <container_id>`
	- In this case, it should be `docker container rm fc17ec09fbc4`

# Build image
- Run the following command to build the image:
	- `docker build . -t myimage:v1`
- List images to see your image tagged `myimage:v1` in the table.
	- `docker images`

# Run the image as a container
- Now that your image is built, run it as a container with the following command:
	- `docker run -dp 8080:8080 myimage:v1`
	- The output is a unique code allocated by docker for the application you are running.
- Run the `curl` command to ping the application as given below.
	- `curl localhost:8080`

![](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/cc201/labs/1_ContainersAndDocker/images/run_img_as_ctr_3.png)  

- If you see the output as above, it indicates that **‘Your app is up and running!’.**

- Now to stop the container we use `docker stop` followed by the container id. The following command uses `docker ps -q` to pass in the list of all running containers:
	- `docker stop $(docker ps -q)`

![](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/cc201/labs/1_ContainersAndDocker/images/run_img_as_ctr_4.png)  

- Check if the container has stopped by running the following command.
	- `docker ps`

![](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/cc201/labs/1_ContainersAndDocker/images/run_img_as_ctr_5.png)
# Push the image to IBM Cloud Container Registry
- The environment should have already logged you into the IBM Cloud account that has been automatically generated for you by the Skills Network Labs environment. The following command will give you information about the account you’re targeting:
	- `ibmcloud target`

![](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/cc201/labs/1_ContainersAndDocker/images/push_img_1.png)  

- The environment also created an IBM Cloud Container Registry (ICR) namespace for you. Since Container Registry is multi-tenant, namespaces are used to divide the registry among several users. Use the following command to see the namespaces you have access to:
	- `ibmcloud cr namespaces`

![](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/cc201/labs/1_ContainersAndDocker/images/push_img_2.png)  

- You should see two namespaces listed starting with `sn-labs`:
	- The first one with your username is a namespace just for you. You have full _read_ and _write_ access to this namespace.
	- The second namespace, which is a shared namespace, provides you with only Read Access

-  Ensure that you are targeting the region appropriate to your cloud account, for instance `us-south` region where these namespaces reside as you saw in the output of the `ibmcloud target` command.
	- `ibmcloud cr region-set us-south`

![](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/cc201/labs/1_ContainersAndDocker/images/push_img_3.png)  

- Log your local Docker daemon into IBM Cloud Container Registry so that you can push to and pull from the registry.
	- `ibmcloud cr login`

![](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/cc201/labs/1_ContainersAndDocker/images/push_img_4.png)  

- Export your namespace as an environment variable so that it can be used in subsequent commands.
	- `export MY_NAMESPACE=sn-labs-$USERNAME`

![](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/cc201/labs/1_ContainersAndDocker/images/push_img_5.png)  

- Tag your image so that it can be pushed to IBM Cloud Container Registry.
	- `docker tag myimage:v1 us.icr.io/$MY_NAMESPACE/hello-world:1`

![](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/cc201/labs/1_ContainersAndDocker/images/push_img_6.png)  

- Push the newly tagged image to IBM Cloud Container Registry.
	- `docker push us.icr.io/$MY_NAMESPACE/hello-world:1`

![](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/cc201/labs/1_ContainersAndDocker/images/push_img_7.png)  

- Verify that the image was successfully pushed by listing images in Container Registry.
	- `ibmcloud cr images`

![](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/cc201/labs/1_ContainersAndDocker/images/push_img_8.png)  

- Optionally, to only view images within a specific namespace.
	- `ibmcloud cr images --restrict $MY_NAMESPACE`

![](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/cc201/labs/1_ContainersAndDocker/images/push_img_9.png)  