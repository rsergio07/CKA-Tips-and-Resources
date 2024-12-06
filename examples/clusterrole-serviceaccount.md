# Create and Bind a ClusterRole for Monitoring

## Objective
You are tasked with creating a `ClusterRole` for monitoring resources and binding it to a `ServiceAccount`.

1. Create a `ClusterRole` named `monitoring-clusterrole`.
2. Allow the `get`, `list`, and `watch` actions for `Pods`, `Services`, and `Endpoints`.
3. Create a `ServiceAccount` named `monitoring-token` in the `monitoring-team` namespace.
4. Bind the `ClusterRole` to the `ServiceAccount`.

## Solution
```bash
kubectl create clusterrole monitoring-clusterrole --verb=get,list,watch --resource=pods,services,endpoints
kubectl create serviceaccount monitoring-token -n monitoring-team
kubectl create clusterrolebinding monitoring-rolebinding --clusterrole=monitoring-clusterrole --serviceaccount=monitoring-team:monitoring-token
