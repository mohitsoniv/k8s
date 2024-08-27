# k8s with Mohit Soni (mohitsoniv)
## Installation of Kubernetes on Ubuntu machine 
### System Requirements
* Operating System: Ubuntu 20.04 or 22.04 (Other versions may work but are not officially recommended)
* CPU: At least 2 cores (4+ cores recommended for better performance)
* RAM: At least 2 GB (4 GB or more recommended)
* Disk Space: At least 10 GB (SSD recommended for better performance)
* Network: Full network connectivity between all machines in the cluster
* Swap: Swap should be disabled
* User Permissions: Root or a user with sudo privileges

### Step 1: Update the System
```
sudo apt-get update
sudo apt-get upgrade -y
```
### Step 2: Disable Swap
```
sudo swapoff -a
sudo sed -i '/ swap / s/^\(.*\)$/#\1/g' /etc/fstab
```
### Step 3: Install Docker (Container Runtime)
```
sudo apt-get install -y apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt-get update
sudo apt-get install -y docker-ce
```
### Step 4: Install Kubernetes (kubeadm, kubelet, kubectl)
```
sudo apt-get update
sudo apt-get install -y apt-transport-https ca-certificates curl
sudo curl -fsSL https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
sudo apt-add-repository "deb http://apt.kubernetes.io/ kubernetes-xenial main"
sudo apt-get update
sudo apt-get install -y kubelet kubeadm kubectl
sudo apt-mark hold kubelet kubeadm kubectl
```
### Step 5: Change the hostnames of all machines
* Skip the step 5 if you are creating single node cluster 
#### 5.1. On the master node
```
sudo hostnamectl set-hostname master.example.com 
exec bash
```
#### 5.2. On worker1
 * If we are deploying the cluster on multiple nodes so create the worker node
```
sudo hostnamectl set-hostname worker-node-1.example.com
exec bash
```
#### 5.3. On worker2 
* If we are deploying the cluster on multiple nodes so create the worker node
```
sudo hostnamectl set-hostname worker-node-2.example.com
exec bash
```
### Step 6: Initialize the Kubernetes Cluster (Control Plane Node Only)
```
sudo kubeadm init --pod-network-cidr=192.168.0.0/16
```
* After initialization, set up the kubectl command to manage your cluster:
```
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```
### Step 7: Install a Pod Network Add-On
```
kubectl apply -f https://docs.projectcalico.org/manifests/calico.yaml
```
#### 7.1. To verify the master node's status
```
kubectl get nodes
```
#### 7.2. To generate a token for joining the worker nodes
* Skip step 7.2 if you are creating single node cluster 
```
sudo kubeadm token create --print-join-command
```
#### Step 8: (Optional) Join Worker Nodes to the Cluster
```
sudo kubeadm join <control-plane-ip>:<control-plane-port> --token <token> --discovery-token-ca-cert-hash sha256:<hash>
```
### Step 9: Verify Installation
```
kubectl get nodes
```
