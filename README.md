# Certified Kubernetes Administrator (CKA) - Tips and Resources

Welcome to the ultimate guide to help you pass the **Certified Kubernetes Administrator (CKA)** exam! This repository includes tips, curated resources, and hands-on examples to boost your preparation.

## What's Inside
- 🌟 **Official Resources**: Links to documentation and tools.
- 📚 **Courses and Labs**: Recommendations for structured learning.
- 🛠️ **Practice Examples**: Real-world scenarios you might face during the exam.
- 📝 **Pro Tips**: Learn the tricks to master CLI, YAML, and vim.

## Key Highlights
- 🚀 Fully hands-on preparation with practice labs and mock exams.
- 📖 Open book exam tips: Learn how to navigate Kubernetes documentation efficiently.
- ⏰ Time management strategies for the 2-hour exam.

## How to Use This Repository
1. Explore the `resources/` folder for recommended courses, simulators, and official links.
2. Practice with `examples/` to get familiar with real exam-like scenarios.
3. Learn essential skills in `tips/`.

---

## Examples Categorized by Domain

### Cluster Architecture
1. [Backup and Restore etcd Data](examples/backup-and-restore-etcd-data.md)  
   **Objective**: Create a snapshot of etcd data and restore it to recover the cluster state.
2. [ClusterRole and ServiceAccount](examples/clusterrole-serviceaccount.md)  
   **Objective**: Create a `ClusterRole` and bind it to a `ServiceAccount`.

### Services and Networking
1. [Create an Ingress Resource](examples/create-ingress-resource.md)  
   **Objective**: Configure an Ingress resource to route traffic for multiple services.
2. [NetworkPolicy](examples/networkpolicy.md)  
   **Objective**: Create a `NetworkPolicy` to control traffic flow between namespaces.

### Storage
1. [Create a PersistentVolume for Logs Storage](examples/create-persistentvolume-logs-storage.md)  
   **Objective**: Configure a PersistentVolume and verify its usage.
2. [Create a PersistentVolumeClaim and Pod](examples/create-persistentvolumeclaim-and-pod.md)  
   **Objective**: Create a PVC to claim storage from a PV and use it in a Pod.

### Workloads and Scheduling
1. [Schedule a Multi-Container Pod](examples/schedule-multi-container-pod.md)  
   **Objective**: Configure a Pod with multiple containers.
2. [Expose Deployment via NodePort](examples/expose-deployment-via-nodeport.md)  
   **Objective**: Expose a deployment using a NodePort service.

### Troubleshooting
1. [Node Maintenance](examples/node-maintenance.md)  
   **Objective**: Set a node to unavailable and reschedule pods.
2. [Ready Nodes Count](examples/ready-nodes-count.md)  
   **Objective**: Count the number of ready nodes, excluding those with the NoSchedule taint.

---

## Tips for Success
1. Explore the `tips/` folder:
   - [Linux Basics](tips/linux-basics.md)
   - [Mastering Vim](tips/mastering-vim.md)
   - [YAML Best Practices](tips/yaml-best-practices.md)
2. Use the `resources/official-links.md` for curated Kubernetes documentation and tools.

---

## License
This project is licensed under the MIT License.