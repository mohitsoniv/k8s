## Step 1: Create a pod
```
vi init1-pod.yaml
```
```
kubectl create -f init1-pod.yaml
```
```
kubectl get pods
```
## Step 2: Create the services
### 2.1. Create myservice  
```
vi init1-myservice.yaml
```
```
kubectl create -f init1-myservice.yaml
```
```
kubectl get services
```
### 2.2. Create mydb service
```
vi init1-mydb.yaml
```
```
kubectl create -f init1-mydb.yaml
```
```
kubectl get services
```
## Step 3: Verify the pod’s state
```
kubectl get pods
```
