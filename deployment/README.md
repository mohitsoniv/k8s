# Configuring Deployment in the Kubernetes Cluster
## Step 1: Configure and set up the deployment file
#### 1.1. Create the YAML file
```
vi httpd-deployment.yaml
```
#### 1.2. Use the cat command to validate the content of the httpd-deployment.yaml file
```
cat httpd-deployment.yaml
```
#### 1.3. Create the resource for httpd-deployment.yaml
```
kubectl create -f httpd-deployment.yaml
```
#### 1.4. Verify the deployment
```
kubectl get deployment
```
## 
## Step : To delete the deployment
```
kubectl delete deployment <deployment.name>
```
