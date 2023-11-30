1. Use the `scale` command to scale up your Deployment. Make sure to run this in the terminal window that is not running the `proxy` command.

1. `kubectl scale deployment hello-world --replicas=3`

![](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/cc201/labs/3_K8sScaleAndUpdate/images/step_4.1.png)  

2. Get Pods to ensure that there are now three Pods instead of just one. In addition, the status should eventually update to “Running” for all three.
1. `kubectl get pods`

![](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/cc201/labs/3_K8sScaleAndUpdate/images/step_4.2.png)  

3. As you did in the last lab, ping your application multiple times to ensure that Kubernetes is load-balancing across the replicas.
1. ``for i in `seq 10`; do curl -L localhost:8001/api/v1/namespaces/sn-labs-$USERNAME/services/hello-world/proxy; done``

![](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/cc201/labs/3_K8sScaleAndUpdate/images/step_4.3.png)  

You should see that the queries are going to different Pods because of the effect of load-balancing.

4. Similarly, you can use the `scale` command to scale down your Deployment.

1. `kubectl scale deployment hello-world --replicas=1`

![](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/cc201/labs/3_K8sScaleAndUpdate/images/step_4.4.png)  

5. Check the Pods to see that two are deleted or being deleted.
1. `kubectl get pods`

![](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/cc201/labs/3_K8sScaleAndUpdate/images/step_4.5.png)  

6. Please wait for some time & run the same command again to ensure that only one pod exists.
1. `kubectl get pods`