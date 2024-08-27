# Configuring replicasets in the Kubernetes Cluster
## Step 1: Configure and set up the replicaset files
#### 1.1. Create the YAML file
```
vi replicaset.yaml
```
#### 1.2. Use the cat command to validate the content of the replicaset.yaml file
```
cat replicaset.yaml
```
#### 1.3. Create the replicaset resource
```
kubectl create -f replicaset.yaml
```
#### 1.4. Verify the repicaset
```
kubectl get rs
```
#### 1.5. Verify the pods created by replicaset 
```
kubectl get pods
```
## Step 2: To edit the replicaset 
```
kubectl edit replicaset <replicaset.name> 
```
## Step 3: To Scale the replicaset 
```
kubectl scale replicaset <replicaset.name> --replicas=5
```
## Step 4: To delete the replicaset 
```
kubectl delete replicaset <replicaset.name>
```
