# Deploying to Azure

## About this Tutorial

After completing this tutorial, you should be able to set up a Kubernetes cluster on Azure, and deploy one or more services to the Kubernetes cluster and expose them to users with access to the network.

## Set Up

### 1. Setting up a Kubernetes cluster

```text
az aks create -g [RESOURCE_GROUP] -n [NAME_OF_THE_CLUSTER] --location WestUS2 --kubernetes-version 1.10.9 --enable-addons http_application_routing --generate-ssh-keys
```

```text
az aks get-credentials --resource-group [RESOURCE_GROUP] --name [NAME_OF_THE_CLUSTER]
```

### 2. Setting up dev spaces for the cluster

```text
az aks use-dev-spaces -g [RESOURCE_GROUP] -n [NAME_OF_THE_CLUSTER]
```

### 3. Launch AKS dashboard  

```text
az aks show --resource-group [RESOURCE_GROUP] --name[NAME_OF_THE_CLUSTER] --query addonProfiles.httpApplicationRouting.config.HTTPApplicationRoutingZoneName -o table
```

```text
az aks browse --resource-group [RESOURCE_GROUP] --name [NAME_OF_THE_CLUSTER]
```

### 4. Create assets for deployment <a id="AzureKubernetesDeployment-Createassetsfordeployment"></a>

```text
azds prep --public
```

```text
kubectl create clusterrolebinding kubernetes-dashboard -n kube-system --clusterrole=cluster-admin --serviceaccount=kube-system:kubernetes-dashboard\n
```

### 5. Launch application <a id="AzureKubernetesDeployment-Launchapplication"></a>

```text
azds up
```

## Deploying multiple services with Docker-Compose

### 1. Create a Docker Compose file for Kubernetes

1. [Kompose](https://github.com/kubernetes/kompose) - _**TODO:** Blob + steps_ 

### 1. Create a namespace in Kubernetes

`kubectl create ns <NAMESPACE_FOR_YOUR_SERVICE>`

### 2. Apply docker-compose files to the namespace

`kubectl apply -n  [<PATH_TO_DOCKER_COMPOSE FILE>] -f` 

### 3. Expose your application

`kubectl expose deployment <DEPLOYMENT> --type=LoadBalancer --name=<NAME_FOR_EXPOSED_SERVICE> --namespace=<NAMESPACE_FOR_YOUR_SERVICE>`

