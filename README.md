Sure, here's the README file in Markdown format:

# Deploying a Voting App on Kubernetes on Azure

This guide will help you deploy a simple voting application on Kubernetes running on Azure. The application consists of a front-end voting web app and a Redis cache to store the votes.

## Prerequisites

- Azure Subscription
- Docker installed on your local machine
- Azure CLI installed and configured
- Kubernetes cluster on Azure (AKS)

## Step 1: Build and Push Docker Images

1. Clone the repository containing the application code:

```bash
git clone https://github.com/roth-ben/kubernetes-hello-world.git
```

2. Navigate to the `vote` directory and build the Docker image for the voting app:

```bash
cd voting-app/vote
docker build -t your-dockerhub-username/vote-app:v1 .
```

3. Push the Docker image to your Docker Hub repository:

```bash
docker push your-dockerhub-username/vote-app:v1
```

## Step 2: Create Kubernetes Deployment and Service

1. Replace `your-dockerhub-username` with your actual Docker Hub username in the downloaded `voting-app-deploy.yaml` YAML file.

2. Deploy the resources to your Kubernetes cluster:

```bash
kubectl apply -f voting-app-deploy.yaml
kubectl apply -f redis-deploy.yaml
kubectl apply -f voting-app-service.yaml
kubectl apply -f redis-service.yaml
```

3. Verify that the pods and services are running:

```bash
kubectl get pods
kubectl get services
```

You should see the `voting-app-deploy` pods, `voting-service`, `redis-deploy` pod, and `redis-service`.

6. Get the external IP address of the `vote-service`:

```bash
kubectl get service vote-service
```

You can now access the voting app by navigating to the external IP address in your web browser.

## Step 3: Deploy to Azure Kubernetes Service (AKS)

1. Create a new AKS cluster on Azure:

```bash
az aks create --resource-group your-resource-group --name your-cluster-name --node-count 3 --generate-ssh-keys
```

2. Connect to the AKS cluster:

```bash
az aks get-credentials --resource-group your-resource-group --name your-cluster-name
```

3. Deploy the voting app and Redis cache to the AKS cluster by following Step 2 above.

4. Get the external IP address of the `vote-service` on the AKS cluster:

```bash
kubectl get service vote-service --watch
```

Once the external IP is provisioned, you can access the voting app by navigating to the external IP address in your web browser.

Congratulations! You have successfully deployed the voting application on Kubernetes running on Azure Kubernetes Service (AKS).