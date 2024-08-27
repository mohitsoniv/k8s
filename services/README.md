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
## Step 2: To delete the service 
```
kubectl delete service <service.name>
```
