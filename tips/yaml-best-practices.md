# YAML Best Practices for CKA

## Key Points
1. Maintain proper indentation (always use spaces, not tabs).
2. Validate syntax using `kubectl apply --dry-run=client`.
3. Use meaningful names for resources.

### Example
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
spec:
  containers:
  - name: nginx
    image: nginx:1.17
```
