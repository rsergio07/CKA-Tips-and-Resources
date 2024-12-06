# Count Ready Nodes Excluding NoSchedule Taint

## Objective
Count how many Kubernetes nodes are in the `Ready` state, excluding those with the `NoSchedule` taint, and write the resulting count to the file `/var/log/node-ready-count.txt`.

## Solution
1. Verify the taints on the `controlplane` and `node01` nodes:
    ```bash
    kubectl describe nodes controlplane | grep Taint
    kubectl describe nodes node01 | grep Taint
    ```
    Example output for `controlplane`:
    ```
    Taints:             node-role.kubernetes.io/control-plane:NoSchedule
    ```
    Example output for `node01`:
    ```
    Taints:             <none>
    ```

2. Use the following command to list all nodes with their taints:
    ```bash
    kubectl get nodes -o custom-columns="NAME:.metadata.name,STATUS:.status.conditions[-1].type,TAINTS:.spec.taints"
    ```
    Example output:
    ```
    NAME           STATUS   TAINTS
    controlplane   Ready    [map[key:node-role.kubernetes.io/control-plane effect:NoSchedule]]
    node01         Ready    <none>
    ```

3. Count the number of `Ready` nodes without taints and write the result to `/var/log/node-ready-count.txt` using `echo`:
    ```bash
    echo 1 > /var/log/node-ready-count.txt
    ```

    Replace `1` with the actual count after manually verifying the nodes and their taints from the output above.
