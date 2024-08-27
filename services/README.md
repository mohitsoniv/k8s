# Configuring Service in the Kubernetes Cluster
## Step 1: Configure and set up the service file
#### 1.1. Create the YAML file
```
vi my-service.yaml
```
#### 1.2. Use the cat command to validate the content of the my-service.yaml file
```
cat my-service.yaml
```
#### 1.3. Create the resource for my-service.yaml
```
kubectl create -f my-service.yaml
```
#### 1.4. Verify the service
```
kubectl get svc
```
## Step 2: Execute the Apache services
#### 2.1. Access the container in pod apache2 and change the content in htdocs/index.html
```
kubectl exec -it apache2 bash
echo “Hello from pod1 ” > htdocs/index.html
cat htdocs/index.html
exit
```
#### 2.2. Access the container in pod apache3 and change the content in htdocs/index.html
```
kubectl exec -it apache3 bash
echo “Hello from pod2 ” > htdocs/index.html
cat htdocs/index.html
exit
```
#### 2.3. Validate if the myservice service is connected to apache2 and apache3 
```
kubectl get svc -o wide
```
#### 2.4. Copy the IP and port number and write
```
curl <ClusterIP:PortNumber>
```
* Note: Initially, execute the curl command only for the service named myservice by using the curl 10.101.183.1:8081 command. However,if you do not see both the services running and messages being displayed for pods apache2 and apache3, then execute both the services kubernetes and myservice as shown in the next step.
#### 2.5. Execute the curl command to complete the task
#### By following these steps, you have successfully completed the configuration of pods in a cluster, service file creation, and Apache service execution to enhance the management of containerized applications within Kubernetes.
## Step 3: To delete the service 
```
kubectl delete service <service.name>
```
