# Example: Create and Bind a ClusterRole

## Context
You are tasked with creating a `ClusterRole` for a deployment pipeline and binding it to a `ServiceAccount`.

### Objective
1. Create a `ClusterRole` named `deployment-clusterrole`.
2. Allow the `create` action for `Deployment`, `StatefulSet`, and `DaemonSet`.
3. Create a `ServiceAccount` named `cicd-token` in the `app-team1` namespace.
4. Bind the `ClusterRole` to the `ServiceAccount`.

### Solution
```bash
kubectl create clusterrole deployment-clusterrole --verb=create --resource=deployments,statefulsets,daemonsets
kubectl create serviceaccount cicd-token -n app-team1
kubectl create clusterrolebinding cicd-rolebinding --clusterrole=deployment-clusterrole --serviceaccount=app-team1:cicd-token
```
