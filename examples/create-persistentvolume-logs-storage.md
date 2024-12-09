# Create a PersistentVolume for Logs Storage

## Objective
Create a `PersistentVolume` named `logs-storage` with a capacity of 5Gi, `ReadWriteMany` access mode, and a `hostPath` at `/var/logs-storage`.

## Solution
The solution involves creating a PersistentVolume (PV) resource in Kubernetes using a YAML configuration file. The PV will be backed by the `/var/logs-storage` directory on the host system, allowing multiple Pods to read and write to it.

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: logs-storage
spec:
  capacity:
    storage: 5Gi
  accessModes:
    - ReadWriteMany
  hostPath:
    path: "/var/logs-storage"
```

1. Save the above YAML to a file named `logs-storage-pv.yaml`.

2. Apply the configuration to create the PersistentVolume:
   ```bash
   kubectl apply -f logs-storage-pv.yaml
   ```

3. Verify that the PersistentVolume has been created and is available:
   ```bash
   kubectl get pv logs-storage
   ```