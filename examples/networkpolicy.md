# Create a NetworkPolicy for External Access

### Objective
Create a `NetworkPolicy` named `allow-external-access` in the `frontend` namespace to allow pods in the `backend` namespace to connect to port 8080 in `frontend`.

### Solution
1. Create the NetworkPolicy YAML file:
    ```yaml
    apiVersion: networking.k8s.io/v1
    kind: NetworkPolicy
    metadata:
      name: allow-external-access
      namespace: frontend
    spec:
      podSelector: {}
      ingress:
      - from:
        - namespaceSelector:
            matchLabels:
              name: backend
        ports:
        - protocol: TCP
          port: 8080
    ```
2. Apply the configuration:
    ```bash
    kubectl apply -f networkpolicy.yaml
    ```
