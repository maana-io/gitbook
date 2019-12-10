# Deploy and Use Your Service

Your custom Knowledge microservice is not useful to anyone until it is deployed to your hosting environment \(e.g., Microsoft Azure\).  In this lesson, you will learn how to use Docker and the Maana CLI to deploy your service to a Kubernetes cluster, register your service with your Maana Q instance, and include it in a test workspace.

### Prerequisites

* Completion of [Wrap-and-Map a Library](wrap-and-map-a-library.md)
* **Dependencies**:
  * VS Code
  * Maana CLI
  * Python 3.7 \(+PIP\)
  * Docker

## Step-by-Step Instructions

**Step 1.** Build a docker image

The project templates installed by the Maana CLI include a `Dockerfile` and other support needed to _containerize_ your service for deployment.  If you are unfamiliar with the process of containerization, there are a number of useful online resources, such as:

* [https://jaxenter.com/containerization-vs-virtualization-docker-introduction-120562.html](https://jaxenter.com/containerization-vs-virtualization-docker-introduction-120562.html)
* [https://code.tutsplus.com/articles/introduction-to-docker-and-kubernetes--cms-25406](https://code.tutsplus.com/articles/introduction-to-docker-and-kubernetes--cms-25406)
* [https://www.coursera.org/lecture/google-kubernetes-engine/what-are-containers-Ad1z3](https://www.coursera.org/lecture/google-kubernetes-engine/what-are-containers-Ad1z3)

Maana has tried to simplify the process through scripts and boilerplate projects so that you can focus on just writing your code and not worrying \(too much\) about the plumbing.

**Step 1a.** Stop the existing service

Return to VS Code terminal and stop the service \(`ctrl+c`\), if it is still running.

**Step 1b.** Add support for `numpy`

In the previous lesson, we added support for `numpy` locally.  Here, since we are concerned with deployment, we need to include it in the `Dockerfile`.

Additionally, this Python template includes a very small base Docker image that uses [Alpine Linux](https://alpinelinux.org/about/), known for providing a tiny, stable core.  Unfortunately, it is so tiny, it lacks support needed by numpy.  Therefore, we also switch to a different base image \(from the same provider, fortunately\).

Update your `Dockerfile` to be the same as:

```bash
FROM tiangolo/uvicorn-gunicorn:python3.7

RUN pip install uvicorn gunicorn ariadne graphqlclient asgi-lifespan
RUN pip install numpy

COPY ./app /app
COPY start.sh /start.sh
WORKDIR /
```

**Step 1c.** Build a Docker image

From the same terminal, enter the following \(slightly modified\) from the `README.md` file:

```bash
docker build -t <your name>-goap ./
```

**Step 2.** Test your containerized custom microservice locally

You can run your custom microservice from within the Docker image you just built by running the following shell command:

```bash
docker run -it -p 4000:80 -t <your name>-goap
```

Validate that your service is running correctly at [http://0.0.0.0:4000/graphql](http://0.0.0.0:4000/graphql).

**Step 3.** Deploy your custom microservice using the CLI `mdeploy` command

 The Maana CLI `mdeploy` command does two important things:

* Uploads your Docker image to a [Container Registry](https://docs.docker.com/registry/)
* Deploys to Kubernetes to run your image at scale

**Step 3a.** Login to the Docker Container Registry

Using the credentials provided by your IT Administrator, use the shell login:

```bash
docker login <server>
Username: <user name>
Password: <password>
Login Succeeded
```

**Step 3b.**  Deploy the service

```bash
gql mdeploy

Target platform    : Private Docker Registry
Service name       : <your name>-goap
Dockerfile path    : .
Container registry : <your container registry>
Version tag        : v1
Pods               : 1
Port               : 80
```

**Step 4.** Test your deployed service

If your deployment was successful, then you will receive the IP address for your service.  You can test it, just like you did locally.  Open the endpoint in a browser and test using your query.

**Step 5.** Register your service with Maana Q

**Step 5a.** Login to your Q instance

**Step 5b.** Open the Services tab

**Step 5c.** Scroll to the bottom

**Step 5d.** Click the **ADD** button

**Step 5e.** Fill in the form

Fill in the form using the appropriate values.

![](../../../.gitbook/assets/image%20%28177%29.png)

You can click **TEST** to have it _introspect_ your service and populate the text editor with its schema.

Be sure to **SAVE** your changes.

**Step 6.**  Test your service

With your custom microservice deployed and registered with Q, people can now use the service in their solutions.

**Step 6a.** Create a new workspace `<your name> GOAP Test`

**Step 6b.** Search for **service** `<your name>-goap` and add it to the workspace inventory

**Step 6c.** Activate it in inventory and try a query in GraphiQL

![](../../../.gitbook/assets/image%20%28123%29.png)

## Conclusions

In this lesson, we covered:

* Modifying the `Dockerfile` to include new base images and Python dependencies
* Build a Docker image for your custom microservice
* Test the Docker image locally to ensure your custom microservice works inside a Docker container
* Use the Maana CLI `mdeploy` command to upload your Docker image to a Component Registry and provision a Pod within your organization's Kubernetes  service cluster
* Register your custom microservice with Maana Q
* Test your custom microservice from within Maana Q

