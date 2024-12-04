# Create a NetworkPolicy

### Objective
Create a `NetworkPolicy` named `allow-port-from-namespace` in the `fubar` namespace to allow pods in the `internal` namespace to connect to port 9000 in `fubar`.

### Solution
1. Create the NetworkPolicy YAML file:
    ```yaml
    apiVersion: networking.k8s.io/v1
    kind: NetworkPolicy
    metadata:
      name: allow-port-from-namespace
      namespace: fubar
    spec:
      podSelector: {}
      ingress:
      - from:
        - namespaceSelector:
            matchLabels:
              name: internal
        ports:
        - protocol: TCP
          port: 9000
    ```
2. Apply the configuration:
    ```bash
    kubectl apply -f networkpolicy.yaml
    ```
