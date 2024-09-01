step-01: Introduction
   1. Create Azure AKS Cluster
   2. Connect to Azure AKS Cluster using Azure Cloud Shell
   3. Explore Azure AKS Cluster Resources
   4. Install Azure CLI and Connect to Azure AKS Cluster using Azure CLI on local desktop
   5. Deploy Sample Application on AKS Cluster and test

Step-02: Create AKS Cluster
   1.Create Kubernetes Cluster
Basics
            Subscription: Subscription
            Resource Group: Creat New: aks-rg1
            Cluster preset configuration: Standard
            Kubernetes Cluster Name: aksdemo1
            Region: (US) Central US
            Availability zones: Zones 1, 2, 3
            AKS Pricing Tier: Free
            Kubernetes Version: Select what ever is latest stable version
            Automatic upgrade: Enabled with patch (recommended)
            Node Size: Standard DS2 v2 (Default one)
            Scale method: Autoscale
            Node Count range: 1 to 5
 Node Pools
            leave to defaults
 Access
            1. Authentication and Authorization: Local accounts with Kubernetes RBAC
            2. Rest all leave to defaults
Networking
   Network Configuration: Azure CNI
   Review all the auto-populated details
Virtual Network
Cluster Subnet
    Kubernetes Service address range
    Kubernetes DNS Service IP Address
    DNS Name prefix
Traffic routing: leave to defaults
Security: Leave to defaults
Integrations
Azure Container Registry: None
All leave to defaults
   Advanced
      All leave to defaults
Tags
leave to defaults
Review + Create
   Click on Create



*Configure kubectl to connect to AKS Cluster

# Template
az aks get-credentials --resource-group <Resource-Group-Name> --name <Cluster-Name>

# Replace Resource Group & Cluster Name
az aks get-credentials --resource-group aks-rg1 --name aksdemo1

# List Kubernetes Worker Nodes
kubectl get nodes 
kubectl get nodes -o wide



STEP-4:  Explore Cluster Control Plane and Workload inside that
# List Namespaces
kubectl get namespaces
kubectl get ns

# List Pods from all namespaces
kubectl get pods --all-namespaces

# List all k8s objects from Cluster Control plane
kubectl get all --all-namespaces


STEP-5: Local Desktop - Install Azure CLI and Azure AKS CLI
# Install Azure CLI (MAC)
brew update && brew install azure-cli

# Login to Azure
az login

# Install Azure AKS CLI
az aks install-cli

# Configure Cluster Creds (kube config)
az aks get-credentials --resource-group aks-rg1 --name aksdemo1

# List AKS Nodes
kubectl get nodes 
kubectl get nodes -o wide

Step-07: Deploy Sample Application and Test
# Deploy Application
kubectl apply -f kube-manifests/

# Verify Pods
kubectl get pods

# Verify Deployment
kubectl get deployment

# Verify Service (Make a note of external ip)
kubectl get service

# Access Application
http://<External-IP-from-get-service-output>


Step-08:cleanup.
# Delete Applications
kubectl delete -f kube-manifests/

REFERENCES:
https://docs.microsoft.com/en-us/cli/azure/install-azure-cli-macos?view=azure-cli-latest


Why Managed Identity when creating Cluster?
https://docs.microsoft.com/en-us/azure/aks/use-managed-identity
