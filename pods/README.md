# Configuring Pods in the Kubernetes Cluster
### Step 1: Configure and set up the pod files
#### 1.1. Create the YAML file
```
vi pod.yaml
```
#### 1.2. Use the cat command to validate the content of the pod.yaml file
```
cat pod.yaml
```
#### 1.3. Create the pod resource
```
kubectl create -f pod.yaml
```
#### 1.4. Create another pod file 
```
 vi pink-pod.yaml
```
#### 1.5.  Use the cat command to validate the content of the pink-pod.yaml file
```
cat pink-pod.yaml
```
#### 1.6. Create the pod resource 
```
kubectl create -f pink-pod.yaml
```
### Step 2: To delete a pod 
```
kubectl delete pod <pod.name>
```
