# Create an Ingress Resource

## Objective
Create an `Ingress` named `my-ingress` in the `default` namespace, exposing the service `my-service` on path `/my-path` using port `8080`.

## Solution

1. Save the following YAML to a file named `my-ingress.yaml`

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: my-ingress
  namespace: default
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: "/"
spec:
  rules:
    - http:
        paths:
          - path: /my-path
            pathType: Prefix
            backend:
              service:
                name: my-service
                port:
                  number: 8080
```

2. Apply the Configuration

Create the Ingress resource:
```bash
kubectl apply -f my-ingress.yaml
```

3. Verify the Ingress
Check the Ingress resource:
```bash
kubectl get ingress my-ingress
```