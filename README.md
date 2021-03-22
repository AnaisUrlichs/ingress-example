## Ingress Example

## Install

The installation will slightly depend on the type of cluster that you are using. 

For this tutorial, we are going to be using the docker-desktop cluster

We need two main components

1. Ingress Controller
2. Ingress resources

Let's set everything up.

We are going to be using the NGINX Ingress Controller. With the NGINX Ingress Controller for Kubernetes, you get basic load balancing, SSL/TLS termination, support for URI rewrites, and upstream SSL/TLS encryption

First off, let's clone this repository

```
git clone <repository>
```

```
cd ingress-example
```

```
cd app-one
```

now build your Docker image

```
docker build -t anaisurlichs/flask-one:1.0 .
```

You can test it out through

```
docker run -p 8080:8080 anaisurlichs/flask-one:1.0
```

And then we are going to push the image to our Docker Hub

```
docker push anaisurlichs/flask-one:1.0
```

We are going to do the same in our second example application

```
cd ..
cd app-two
```

build the docker image

```
docker build -t anaisurlichs/flask-two:1.0 .
```

push it to your Docker Hub

```
docker push anaisurlichs/flask-two:1.0
```

Now apply the deployment-one.yaml and the deployment-tow.yaml

```
kubectl apply -f deployment-one.yaml
kubectl apply -f deployment-two.yaml
```

Make sure they are running correctly 

```
kubectl get all
```

Installing Ingress Controller

```
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v0.44.0/deploy/static/provider/cloud/deploy.yaml
```

**Installing Ingress Resource**

```
kubectl apply -f ingress.yaml
```

make sure that everything is running correctly

```
kubectl get all -n ingress-nginx
```

Making paths happen [https://github.com/kubernetes/ingress-nginx/issues/3762](https://github.com/kubernetes/ingress-nginx/issues/3762)