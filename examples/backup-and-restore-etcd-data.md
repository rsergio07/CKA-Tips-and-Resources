# Backup and Restore etcd Data

## Objective
Create a snapshot of the etcd database at `https://127.0.0.1:2379` and save it to `/opt/etcd-snapshot.db`. Restore the etcd data from the snapshot to the directory `/var/lib/etcd-from-backup`.

## Solution
The solution involves using the `etcdctl` command to take a snapshot of the etcd database, restore it to the specified directory.

1. Create an etcd Snapshot
Run the following command to create a snapshot of the etcd data:
```bash
ETCDCTL_API=3 etcdctl snapshot save /opt/etcd-snapshot.db --endpoints=https://127.0.0.1:2379 --cacert=/etc/kubernetes/pki/etcd/ca.crt --cert=/etc/kubernetes/pki/etcd/server.crt --key=/etc/kubernetes/pki/etcd/server.key
```

2. Restore the etcd database using the snapshot
Run the following command to restore the snapshot of the etcd data:
```bash
ETCDCTL_API=3 etcdctl snapshot restore /opt/etcd-snapshot.db --data-dir=/var/lib/etcd-from-backup
```