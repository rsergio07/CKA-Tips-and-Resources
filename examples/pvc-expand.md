# Configure a Pod to Use a PersistentVolume for Storage

### Objective
Create a `PersistentVolumeClaim` with a storage request of `50Mi` using the `standard` storage class. Then, configure a Pod to use this PVC for storage. Finally, expand the PVC capacity to `70Mi` to demonstrate how to dynamically adjust storage in Kubernetes.

### Solution

1. Create the PersistentVolumeClaim YAML file `pvc-storage.yaml`:
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
      storageClassName: standard
    ```
    Apply the configuration:
    ```bash
    kubectl apply -f pvc-storage.yaml
    ```
    Verify the PersistentVolumeClaim:
    ```bash
    kubectl get pvc pvc-storage
    ```

2. Create the Pod YAML file `pvc-pod.yaml`:
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

3. Expand the PersistentVolumeClaim capacity by editing the existing `pvc-storage.yaml`:
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
      storageClassName: standard  # Use a suitable storage class
    ```
    Re-apply the updated configuration:
    ```bash
    kubectl apply -f pvc-storage.yaml
    ```

4. Verify the expansion:
    ```bash
    kubectl describe pvc pvc-storage
    ```

5. Check the updated storage in the Pod:
    ```bash
    kubectl exec pvc-pod -- df -h /usr/share/nginx/html
    ```
