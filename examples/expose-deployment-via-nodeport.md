# Expose a Deployment via NodePort

## Objective
Reconfigure the `web-app` deployment to expose port `8080/tcp` of the `httpd` container and create a `NodePort` service named `web-app-svc`.

## Solution
Expose the web-app deployment on port 8080 and map it to a NodePort service
```bash
kubectl expose deployment web-app --name=web-app-svc --type=NodePort --port=8080 --target-port=8080
