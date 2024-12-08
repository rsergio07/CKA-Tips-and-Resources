# Set Node as Unavailable, Reschedule Pods, and Restore Node Readiness

## Objective
Set the node `node01` as unavailable, reschedule all pods running on it, and then restore the node to the `Ready` state.

## Solution

Verify the Node Status

```bash
kubectl get nodes
```

Drain the Node
Use the following command to make `node01` unavailable and reschedule all pods running on it:

```bash
kubectl drain node01 --ignore-daemonsets
```

Restore the Node to the Ready State

```bash
kubectl uncordon node01
```

Verify the Node Status

```bash
kubectl get nodes
```