# Launching the Kubernetes Dashboard
## Step 1: Implement the dashboard deployment
```
kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.7.0/aio/deploy/recommended.yaml
```
## Step 2: Validate the pod, service, and deployment creation
#### 2.1. To create Pod, Deployment & Service 
```
kubectl get pods -n kubernetes-dashboard -o wide
kubectl get deployment -n kubernetes-dashboard -o wide
kubectl get svc -n kubernetes-dashboard -o wide
```
#### 2.2. To access the service outside the cluster, edit the service type from ClusterIP to NodePort
```
kubectl edit svc -n kubernetes-dashboard kubernetes-dashboard
```
## Step 3: Confirm the dashboard service type
#### 3.1. To confirm that the service type has been changed to NodePort
```
kubectl get svc -n kubernetes-dashboard -o wide
```
#### 3.2. To determine the location of the pod
```
kubectl get pods -n kubernetes-dashboard -o wide
kubectl get svc -n kubernetes-dashboard -o wide 
kubectl get nodes -o wide
```
* Note: In this case, the Pod is running on worker-node1. Note down the IP and NodePort of node1.
#### 3.3. Use the INTERNAL-IP as 172.31.25.191, and PORT(S) as 30087, and copy the link: https://172.31.25.191:30087
* Note: In your case, the IP and NodePort will be different. Change the IP and NodePort 
accordingly:
 https:// your worker-node-1:NodePort
## Step 4: Access the master node IP
#### 4.1. Navigate to the LMS dashboard and click on master then desktop
#### 4.2. Open Firefox, paste the copied link from step 3.3 into the search bar, and press Enter
#### 4.3. Click on the Advanced button
#### 4.4. Click Accept the Risk and Continue
## Step 5: Log into the service dashboard
#### 5.1. Create a service account
```
vi ServiceAccount.yaml
```
```
kubectl create -f ServiceAccount.yaml
```
#### 3 5.2. Create a yaml file for cluster role binding
```
vi ClusterRoleBinding.yaml
```
```
kubectl create -f ClusterRoleBinding.yaml
```
#### 5.3. Retrieve the token to log 
```
kubectl -n kubernetes-dashboard create token admin-user
```
#### 5.4. Copy the token and paste it into the Kubernetes dashboard login screen, then click Sign in
## Step 6: Access the Kubernetes dashboard
#### 6.1. Click on the All namespaces drop down menu
#### 6.2. Select kube-system
#### 6.3. Use the search bar to find and select kube-apiserver
#### View the logs of the kube-apiserver.
#### 6.4. [OPTIONAL] Cleanup: To delete the Kubernetes dashboard version 2.5, in the master node
```
kubectl delete -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.5.0/aio/deploy/recommended.yaml
```
#### By following these steps, you will be able to deploy the Kubernetes Dashboard, establish secure access, and navigate the interface to monitor and manage your Kubernetes cluster.

