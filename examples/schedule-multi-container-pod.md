# Schedule a Pod with Multiple Containers

## Objective
Schedule a Pod named `multi-container-pod` with two containers: `nginx` and `busybox`. The `busybox` container should run a command to print `Hello from Busybox` and then sleep for 3600 seconds.

## Solution
1. Generate a Basic Pod YAML File:  
   Use the `kubectl run` command with `--dry-run=client` to generate a Pod YAML file for the `nginx` container:
   ```bash
   kubectl run multi-container-pod --image=nginx:latest --dry-run=client -o yaml > multi-container-pod.yaml
   ```

2. Edit the YAML File to Add a Second Container:  
   Open `multi-container-pod.yaml` and modify the `containers` section to include the second container with the specified command:
   ```yaml
   apiVersion: v1
   kind: Pod
   metadata:
     name: multi-container-pod
     labels:
       app: multi-container
   spec:
     containers:
     - name: nginx-container
       image: nginx:latest
       ports:
       - containerPort: 80
     - name: busybox-container
       image: busybox:latest
       command: ["sh", "-c", "echo Hello from Busybox && sleep 3600"]
   ```

3. Apply the Updated YAML:  
   Once the YAML file has been updated, apply it to create the Pod:
   ```bash
   kubectl apply -f multi-container-pod.yaml
   ```

4. Verify the Pod:  
   Check the Pod’s status to confirm it is running:
   ```bash
   kubectl get pod multi-container-pod
   ```