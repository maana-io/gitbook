# Deploying with Kubernetes

## Deploying and Registering a Q Service with Kubernets

This document provides instructions for how to deploy a graphQL microservice using Kubernetes and then register it with the Maana Q Catalog service. These steps should be used whenever you wish to make a new service available for use within the Maana Q platform.

## BEFORE YOU BEGIN

This section describes a collection of prerequisites which you will need to complete before deploying a new microservice. These prerequisites usually will need to be performed only once.

### Install the Command Line Tools

In this cookbook, we will be using command line tools to invoke Docker and Kubernetes commands. If you have not already done so, navigate to the web page below and install the _docker_ and _kubectl_ tools for your operating system.

* [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)
* [docker](https://docs.docker.com/v17.09/engine/installation/)

### Configure Kubernetes

In order for kubectl to access a Kubernetes cluster you will need a kubeconfig file. Check that kubectl is configured by querying the cluster state:

```
kubectl cluster-info
```

If you see an error message, then Kubernetes has not been configured properly. If you are using a cloud service provider, you may be able to use your provider's command line tool to setup access to your cluster. For example:

```
# Microsoft Azure
az aks --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME
# Google Cloud
gcloud container clusters get-credentials $CLUSTER_NAME
# Amazon AWS
aws eks --region $REGION update-kubeconfig --name $CLUSTER_NAME
```

Alternatively, you may be provided with a config file by your system administrator. Copy this file to the ~./kube folder using the following commands:

```
mkdir ~/.kube
mv config ~/.kube/config
```

## RECIPES

### How do I Push My Service's Image to A Container Repository?

Assuming that you have created a docker image for your service, you will need to push that image to a container repository that is accessible from your cloud provider. You can use the docker command line tool to push your image as normal:

```
docker tag $CONTAINER_SVC_URL/$IMG_NAME
docker push $CONTAINER_SVC_URL/$IMG_NAME
```

where $CONTAINER\_SVC\_URL is the host name for your docker container registry, and $IMG\_NAME is the name of the docker image that you want to deploy.

### How do I Deploy A Service Using Kubernetes

Once the docker image has been pushed to the repository, you can start the service on the kubernetes cluster with the following command:

```
kubectl run $MY_SVC_NAME --image=$CONTAINER_SVC_URC/$IMGNAME --port=$PORT --replicas=$N
```

Where $MY\_SVC\_NAME is a name that you will use to identify your service in kubernetes, and $PORT is the port that your service is running on. The optional paramter $N controls how many replicas of your service will be started; if this parameter is omitted, it is assumed to be 1.

To expose your service, you need to start a load balancer. The load balancer will redirect traffic that it receives to one of the service pods. Start the load balancer using the following command:

```
kubectl expose deployment $MY_SVC_NAME --type=LoadBalancer --port=$PORT --target-port=$PORT
```

It may take several minutes for your load balancer to be fully deployed. You can view the status of your load balancer by executing the following command:

```
kubectl get svc $MY_SVC_NAME
```

when your load balancer is fully deployed, the column named "EXTERNAL-IP" will contain an IP address that can be used to access your service's graphQL endpoint.

### How Do I Find the IP Address of My Service?

When your load balancer is running, you can use the command below to get the IP address.

```
kubectl get svc $MY_SVC_NAME
```

The column named "EXTERNAL-IP" will contain an IP address that can be used to access your service's graphQL endpoint.

### How Do I Update the Image of the Service That I am Running?

You can update the docker image for your service with the following command:

```
kubectl set image deployment $MY_SVC_NAME $MY_SVC_NAME=$NEW_IMAGE_NAME
```

Updates incrementally replace each of the running pods with the new image. You can monitor the status of the update with the following command:

```
kubectl get svc $MY_SVC_NAME
```

### How Do I Stop My Service When I am Not Using It?

You should shut down your service when you are done using it. This prevents you from incurring excess usage charges. You can use the command below to stop your service:

```
# Stop the service's replicas
kubectl delete svc $MY_SVC_NAME
# Stop the load balancer
kubectl delete deployment $MY_SVC_NAME
```

### How Do I Register My Service With the Maana Catalog?

You can use your service in the Maana Q portal, however you will need to register it first. To register your service, follow the steps below:

* Log into the Maana Q Portal
* Navigate to the Admin panel
* Click on the "Add" button on the bottom of the page.
* Fill out the name and endpoint fields with the name and IPAddress \(including port number\) for your service. For example:

  ```
  Name : My Wonderful Service
  Endpoint URL : http://10.11.12.13:8050/graphql
  ```

* Click the save button.

If you get a 601 error, you have probably mistyped the endpoint url. Check that you have the correct IP address and port number, and that you have prefixed the URL with the correct protocol \(e.g. http:// \) and have the correct path to the graphQL endpoint \(e.g. /graphql \).

![Register Service](https://github.com/maana-io/gitbook/tree/79e6d5f96bc846be314bfa73d9ee832df2839ef8/product-guide/reference-guide/q-platform-and-microservices/deployment/deploying-with-kubernetes/RegisterService.png)

