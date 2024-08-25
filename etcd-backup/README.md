```
sudo ETCDCTL_API=3 etcdctl \
--endpoints $advertise_url \
--cacert /etc/kubernetes/pki/etcd/ca.crt \
--key /etc/kubernetes/pki/etcd/server.key \
--cert /etc/kubernetes/pki/etcd/server.crt snapshot save etcd_backup.db
```

```
sudo ETCDCTL_API=3 etcdctl \
    --endpoints="$advertise_url" \
    --cacert="/etc/kubernetes/pki/etcd/ca.crt" \
    --key="/etc/kubernetes/pki/etcd/server.key" \
    --cert="/etc/kubernetes/pki/etcd/server.crt" \
    --write-out=table snapshot status etcd_backup.db
```
