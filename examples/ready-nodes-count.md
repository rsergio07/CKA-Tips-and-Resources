# Count Ready Nodes

### Objective
Check the number of ready nodes and save the count to `/opt/KUSC00402/kusc00402.txt`.

### Solution
1. Use the following command to get the count of ready nodes:
    ```bash
    kubectl get nodes --no-headers | grep -w "Ready" | wc -l
    ```
2. Save the output to the specified file:
    ```bash
    kubectl get nodes --no-headers | grep -w "Ready" | wc -l > /opt/KUSC00402/kusc00402.txt
    ```
