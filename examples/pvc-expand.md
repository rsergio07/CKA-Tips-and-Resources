# Configure a Pod to Use PersistentVolume Storage

### Objective
Create a `PersistentVolume` named `task-pv-volume`, a `PersistentVolumeClaim` named `task-pv-claim`, and a Pod named `task-pv-pod` that uses the PVC for storage. The storage will be mounted into the Pod at `/usr/share/nginx/html`.

---

### Solution

1. **Create the PersistentVolume (`pv-volume.yaml`)**
    ```yaml
    apiVersion: v1
    kind: PersistentVolume
    metadata:
      name: task-pv-volume
      labels:
        type: local
    spec:
      storageClassName: manual
      capacity:
        storage: 10Gi
      accessModes:
        - ReadWriteOnce
      hostPath:
        path: "/mnt/data"
    ```
    Apply the configuration:
    ```bash
    kubectl apply -f pv-volume.yaml
    ```
    Verify the PersistentVolume:
    ```bash
    kubectl get pv task-pv-volume
    ```

---

2. **Create the PersistentVolumeClaim (`pvc-claim.yaml`)**
    ```yaml
    apiVersion: v1
    kind: PersistentVolumeClaim
    metadata:
      name: task-pv-claim
    spec:
      storageClassName: manual
      accessModes:
        - ReadWriteOnce
      resources:
        requests:
          storage: 3Gi
    ```
    Apply the configuration:
    ```bash
    kubectl apply -f pvc-claim.yaml
    ```
    Verify the PersistentVolumeClaim:
    ```bash
    kubectl get pvc task-pv-claim
    ```

---

3. **Create the Pod (`pod-using-pvc.yaml`)**
    ```yaml
    apiVersion: v1
    kind: Pod
    metadata:
      name: task-pv-pod
    spec:
      volumes:
        - name: task-pv-storage
          persistentVolumeClaim:
            claimName: task-pv-claim
      containers:
        - name: task-pv-container
          image: nginx
          ports:
            - containerPort: 80
              name: "http-server"
          volumeMounts:
            - mountPath: "/usr/share/nginx/html"
              name: task-pv-storage
    ```
    Apply the configuration:
    ```bash
    kubectl apply -f pod-using-pvc.yaml
    ```
    Verify the Pod:
    ```bash
    kubectl get pod task-pv-pod
