# Configure a Pod to Use PersistentVolume Storage

### Objective
Create a `PersistentVolume`, a `PersistentVolumeClaim`, and a Pod to demonstrate basic storage provisioning in Kubernetes.

### Solution

1. Create the PersistentVolume YAML file `pv-volume.yaml`:
    ```yaml
    apiVersion: v1
    kind: PersistentVolume
    metadata:
      name: pv-volume
    spec:
      capacity:
        storage: 10Gi
      accessModes:
        - ReadWriteOnce
      persistentVolumeReclaimPolicy: Retain
      hostPath:
        path: "/mnt/data"
    ```
    Apply the configuration:
    ```bash
    kubectl apply -f pv-volume.yaml
    ```
    Verify the PersistentVolume:
    ```bash
    kubectl get pv pv-volume
    ```

2. Create the PersistentVolumeClaim YAML file `pvc-volume.yaml`:
    ```yaml
    apiVersion: v1
    kind: PersistentVolumeClaim
    metadata:
      name: pvc-volume
    spec:
      accessModes:
        - ReadWriteOnce
      resources:
        requests:
          storage: 8Gi
    ```
    Apply the configuration:
    ```bash
    kubectl apply -f pvc-volume.yaml
    ```
    Verify the PersistentVolumeClaim:
    ```bash
    kubectl get pvc pvc-volume
    ```

3. Create the Pod YAML file `pod-using-pvc.yaml`:
    ```yaml
    apiVersion: v1
    kind: Pod
    metadata:
      name: pvc-pod
    spec:
      containers:
      - name: busybox
        image: busybox
        command: [ "sleep", "3600" ]
        volumeMounts:
        - mountPath: "/mnt/data"
          name: volume
      volumes:
      - name: volume
        persistentVolumeClaim:
          claimName: pvc-volume
    ```
    Apply the configuration:
    ```bash
    kubectl apply -f pod-using-pvc.yaml
    ```
    Verify the Pod:
    ```bash
    kubectl get pod pvc-pod
    ```

4. Verify that the storage is mounted:
    ```bash
    kubectl exec pvc-pod -- ls /mnt/data
    ```
    - This command will list the contents of the mounted volume inside the Pod.
