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
    Verify the PersistentVolume:
    ```bash
    kubectl get pv pv-storage
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
    Verify the PersistentVolumeClaim:
    ```bash
    kubectl get pvc pvc-storage
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
    Verify the Pod:
    ```bash
    kubectl get pod pvc-pod
    ```

4. Expand the PersistentVolumeClaim capacity by editing the existing `pvc-storage.yaml`:
    Update the `resources.requests.storage` value in the file:
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
          storage: 70Mi
      storageClassName: manual
    ```
    Re-apply the updated configuration:
    ```bash
    kubectl apply -f pvc-storage.yaml
    ```

5. Verify the expansion:
    ```bash
    kubectl describe pvc pvc-storage
    ```

6. Check the updated storage in the Pod:
    ```bash
    kubectl exec pvc-pod -- df -h /usr/share/nginx/html
    ```
