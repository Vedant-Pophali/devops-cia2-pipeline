# DevOps CIA-2 Pipeline

This repository contains the commands required to access the Azure Kubernetes Service (AKS) cluster and retrieve the external IP address of the deployed application.

## 1. Access the Azure AKS Cluster

1. Open the **Azure Portal**.
2. Navigate to the terminal (Azure Cloud Shell).
3. Execute the following command to connect `kubectl` to the AKS cluster:

```bash
az aks get-credentials \
  --resource-group devops-cia2-rg \
  --name devops-aks-central \
  --overwrite-existing
```

This command:
- Retrieves the credentials for the specified AKS cluster.
- Updates the local Kubernetes configuration (`kubeconfig`).
- Allows `kubectl` to communicate with the AKS cluster.

## 2. Retrieve the Service IP Address

Execute the following command to list all Kubernetes services:

```bash
kubectl get services
```

This displays information such as:

| Column | Description |
|---|---|
| NAME | Name of the Kubernetes service |
| TYPE | Service type (ClusterIP, NodePort, LoadBalancer) |
| CLUSTER-IP | Internal IP address of the service |
| EXTERNAL-IP | Publicly accessible IP address, if assigned |
| PORT(S) | Ports exposed by the service |

## 3. Access the Application

- If the service is of type `LoadBalancer`, use the IP displayed under `EXTERNAL-IP`.
- If the service is of type `NodePort`, access the application using the node's IP address and the assigned NodePort.
- If the service is of type `ClusterIP`, it is accessible only within the Kubernetes cluster by default.

**Note:** If the `EXTERNAL-IP` displays `<pending>`, wait for Azure to provision the external load balancer IP and run `kubectl get services` again.