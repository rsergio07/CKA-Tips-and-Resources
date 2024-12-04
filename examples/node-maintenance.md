# Example: Set Node as Unavailable and Reschedule Pods

## Objective
Set the node `node01` as unavailable and reschedule all pods running on it.

### Solution
```bash
kubectl drain node01 --ignore-daemonsets --delete-emptydir-data
kubectl cordon node01
```
