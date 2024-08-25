# Backing Up and Restoring Etcd Cluster Data
## 1. Back up the etcd cluster data
### 1.1. Install the etcd-client
```
sudo apt install etcd-client
```
### 1.2. List all the pods in the kube-system namespace
```
kubectl get pods -n kube-system
```
### 1.3. Describe the etcd pod in the kube-system namespace and note the IP address
```
kubectl describe pods <etcd-pod-name> -n kube-system
```
### 1.4. After noting the client URL, set it as an environment variable and confirm its value
```
export advertise_url=<advertise-client-url>
echo $advertise_url
```
#### Note: Replace <advertise-client-url> with the actual advertise client URL value you retrieved.

### 1.5. Back up the etcd data
```
sudo ETCDCTL_API=3 etcdctl \
--endpoints $advertise_url \
--cacert /etc/kubernetes/pki/etcd/ca.crt \
--key /etc/kubernetes/pki/etcd/server.key \
--cert /etc/kubernetes/pki/etcd/server.crt snapshot save etcd_backup.db
```
### 1.6. Verify the etcd backup
```
sudo ETCDCTL_API=3 etcdctl \
    --endpoints="$advertise_url" \
    --cacert="/etc/kubernetes/pki/etcd/ca.crt" \
    --key="/etc/kubernetes/pki/etcd/server.key" \
    --cert="/etc/kubernetes/pki/etcd/server.crt" \
    --write-out=table snapshot status etcd_backup.db
```
## 2. Obtain the data from the etcd cluster
### 2.1.  Restore the etcd cluster data
```
sudo ETCDCTL_API=3 etcdctl \
--endpoints $advertise_url \
--cacert /etc/kubernetes/pki/etcd/ca.crt \
--key /etc/kubernetes/pki/etcd/server.key \
--cert /etc/kubernetes/pki/etcd/server.crt snapshot restore etcd_backup.db
```
### or
```
sudo ETCDCTL_API=3 etcdctl \
    --endpoints="$advertise_url" \
    --cacert="/etc/kubernetes/pki/etcd/ca.crt" \
    --key="/etc/kubernetes/pki/etcd/server.key" \
    --cert="/etc/kubernetes/pki/etcd/server.crt" \
    snapshot restore etcd_backup.db \
    --data-dir="/var/lib/etcd-restored" \
    --initial-cluster="default=$advertise_url" \
    --initial-cluster-token="etcd-cluster" \
    --initial-advertise-peer-urls="$advertise_url"
```
### 2.2. Set the proper ownership for the new data directory
```
stat -c %U:%G /var/lib/etcd
sudo chown -R root:root /var/lib/etcd
```
### 2.3. Confirm the state of the cluster
```
sudo ETCDCTL_API=3 etcdctl endpoint health \
--endpoints=$advertise_url \
--cacert=/etc/kubernetes/pki/etcd/ca.crt \
--cert=/etc/kubernetes/pki/etcd/server.crt \
--key=/etc/kubernetes/pki/etcd/server.key
```
