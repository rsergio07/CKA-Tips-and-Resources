# Configure PersistentVolumeClaim and Expand Capacity

### Objective
Create a `PersistentVolumeClaim` named `pv-volume` and a pod that mounts it. Expand the PVC capacity to 70Mi afterward.

### Solution
1. Create the PVC and pod YAML file:
    ```yaml
    apiVersion: v1
    kind: PersistentVolumeClaim
    metadata:
      name: pv-volume
    spec:
      accessModes:
      - ReadWriteOnce
      resources:
        requests:
          storage: 50Mi
    ---
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
          name: pvc-storage
      volumes:
      - name: pvc-storage
        persistentVolumeClaim:
          claimName: pv-volume
    ```
2. Apply the configuration:
    ```bash
    kubectl apply -f pvc-and-pod.yaml
    ```
3. Expand the PVC capacity:
    ```yaml
    apiVersion: v1
    kind: PersistentVolumeClaim
    metadata:
      name: pv-volume
    spec:
      resources:
        requests:
          storage: 70Mi
    ```
4. Apply the updated PVC configuration:
    ```bash
    kubectl apply -f pvc-expand.yaml
    ```
5. Verify the expansion:
    ```bash
    kubectl describe pvc pv-volume
    ```
