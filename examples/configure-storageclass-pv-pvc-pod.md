```yaml
# Step 1: Create the StorageClass
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: fast-storage
provisioner: kubernetes.io/no-provisioner
volumeBindingMode: Immediate
```

**Instruction:** Save this YAML as `fast-storageclass.yaml` and apply it using:
```bash
kubectl apply -f fast-storageclass.yaml
```

Verify the StorageClass:
```bash
kubectl get storageclass fast-storage
```

---

```yaml
# Step 2: Create the PersistentVolume
apiVersion: v1
kind: PersistentVolume
metadata:
  name: fast-pv-cka
spec:
  capacity:
    storage: 50Mi
  accessModes:
    - ReadWriteOnce
  persistentVolumeReclaimPolicy: Retain
  storageClassName: fast-storage
  hostPath:
    path: "/tmp/fast-data"
```

**Instruction:** Save this YAML as `fast-pv.yaml` and apply it using:
```bash
kubectl apply -f fast-pv.yaml
```

Verify the PersistentVolume:
```bash
kubectl get pv fast-pv-cka
```

---

```yaml
# Step 3: Create the PersistentVolumeClaim
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: fast-pvc-cka
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 30Mi
  storageClassName: fast-storage
```

**Instruction:** Save this YAML as `fast-pvc.yaml` and apply it using:
```bash
kubectl apply -f fast-pvc.yaml
```

Verify the PersistentVolumeClaim:
```bash
kubectl get pvc fast-pvc-cka
```

---

```yaml
# Step 4: Create the Pod
apiVersion: v1
kind: Pod
metadata:
  name: fast-pod-cka
spec:
  containers:
    - name: nginx
      image: nginx:latest
      volumeMounts:
        - mountPath: "/app/data"
          name: fast-storage-volume
  volumes:
    - name: fast-storage-volume
      persistentVolumeClaim:
        claimName: fast-pvc-cka
```

**Instruction:** Save this YAML as `fast-pod.yaml` and apply it using:
```bash
kubectl apply -f fast-pod.yaml
```

Verify the Pod:
```bash
kubectl get pod fast-pod-cka
```

---

### **Testing the Volume**
Once the Pod is running, verify the mounted volume by executing:
```bash
kubectl exec fast-pod-cka -- ls /app/data
```

If you want to test writing data to the volume:
```bash
kubectl exec fast-pod-cka -- sh -c 'echo "Hello Kubernetes" > /app/data/test.txt'
kubectl exec fast-pod-cka -- cat /app/data/test.txt
```

---