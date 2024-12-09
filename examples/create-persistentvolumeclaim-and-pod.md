# Create a PersistentVolumeClaim and a Pod to Use Logs Storage

## Objective
Create a `PersistentVolumeClaim` named `logs-pvc` that requests storage from the `logs-storage` PersistentVolume. Then, create a Pod named `logs-pod` that mounts the storage at `/app/logs`.

## Solution
The solution involves two steps:
1. Creating a PersistentVolumeClaim to request storage from the `logs-storage` PersistentVolume.
2. Creating a Pod that uses the PVC and mounts the storage.

1. Create the PersistentVolumeClaim
Save the following YAML to a file named `logs-pvc.yaml`:
```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: logs-pvc
spec:
  accessModes:
    - ReadWriteMany
  resources:
    requests:
      storage: 3Gi
  storageClassName: ""
```
Apply the configuration:
```bash
kubectl apply -f logs-pvc.yaml
```

2. Create the Pod
Save the following YAML to a file named `logs-pod.yaml`:
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: logs-pod
spec:
  containers:
  - name: logs-container
    image: busybox
    command: ["sh", "-c", "while true; do echo Hello from Logs; sleep 10; done"]
    volumeMounts:
    - name: logs-volume
      mountPath: "/app/logs"
  volumes:
  - name: logs-volume
    persistentVolumeClaim:
      claimName: logs-pvc
```
Apply the configuration:
```bash
kubectl apply -f logs-pod.yaml
```

## Verification
1. Verify the PVC:  
   Check the status of the PVC to ensure it is bound to the `logs-storage` PersistentVolume:
   ```bash
   kubectl get pvc logs-pvc
   ```
   Example output:
   ```
   NAME       STATUS   VOLUME         CAPACITY   ACCESS MODES   STORAGECLASS   AGE
   logs-pvc   Bound    logs-storage   5Gi        RWX                           15s
   ```

2. Verify the Pod:  
   Check the Pod's status to ensure it is running:
   ```bash
   kubectl get pod logs-pod
   ```
   Example output:
   ```
   NAME       READY   STATUS    RESTARTS   AGE
   logs-pod   1/1     Running   0          9s
   ```