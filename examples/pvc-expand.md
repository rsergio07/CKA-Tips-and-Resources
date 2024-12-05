# Configure a Pod to Use a PersistentVolume for Storage

### Objective
Create a `PersistentVolume`, a `PersistentVolumeClaim`, and a Pod that uses the PVC for storage. Expand the PVC capacity to 70Mi afterward.

### Solution

1. Create the PersistentVolume YAML file `pv-storage.yaml`:
    ```yaml
    apiVersion: v1
    kind: PersistentVolume
    metadata:
      name: pv-storage
    spec:
      capacity:
        storage: 100Mi
      accessModes:
        - ReadWriteOnce
      persistentVolumeReclaimPolicy: Retain
      storageClassName: manual
      hostPath:
        path: "/mnt/data"
    ```
    Apply the configuration:
    ```bash
    kubectl apply -f pv-storage.yaml
    ```

2. Create the PersistentVolumeClaim YAML file `pvc-storage.yaml`:
    ```yaml
    apiVersion: v1
    kind: PersistentVolumeClaim
    metadata:
      name: pvc-storage
    spec:
      accessModes:
        - ReadWriteOnce
      resources:
        requests:
          storage: 50Mi
      storageClassName: manual
    ```
    Apply the configuration:
    ```bash
    kubectl apply -f pvc-storage.yaml
    ```

3. Create the Pod YAML file `pvc-pod.yaml`:
    ```yaml
    apiVersion: v1
    kind: Pod
    metadata:
      name: pvc-pod
    spec:
      containers:
      - name: nginx
        image: nginx
        volumeMounts:
        - mountPath: "/usr/share/nginx/html"
          name: storage
      volumes:
      - name: storage
        persistentVolumeClaim:
          claimName: pvc-storage
    ```
    Apply the configuration:
    ```bash
    kubectl apply -f pvc-pod.yaml
    ```

4. Expand the PersistentVolumeClaim capacity. Create the YAML file `pvc-expand.yaml`:
    ```yaml
    apiVersion: v1
    kind: PersistentVolumeClaim
    metadata:
      name: pvc-storage
    spec:
      resources:
        requests:
          storage: 70Mi
    ```
    Apply the updated configuration:
    ```bash
    kubectl apply -f pvc-expand.yaml
    ```

5. Verify the expansion:
    ```bash
    kubectl describe pvc pvc-storage
    ```

6. Check the updated storage in the Pod:
    ```bash
    kubectl exec pvc-pod -- df -h /usr/share/nginx/html
    ```
