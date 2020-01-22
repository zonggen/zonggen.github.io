---
layout: post
title:  "Access network of MongoDB service on OKD with docker-compose"
categories: [ blog, work]
featured-img: work-update-2
---

I was trying to set up a Golang server with a MongoDB database
for [FCOS Pinger Backend](https://github.com/zonggen/fcos-pinger-backend) using
docker-compose (alias docker-compose=podman-compose), but I was struggling to
access the MongoDB container from server container with error message saying `Connection refused`.
Tried adding a router, but that didn't work.

After researching and learning about networks on Openshift/Kubernetes, it turns out that
the server code `clientOptions := options.Client().ApplyURI("mongodb://localhost:27017")` needs
to be `clientOptions := options.Client().ApplyURI("mongodb://mongodb:27017")` since the pods
have different Ip addresses and the `localhost:27017` in server container will not be the port that
MongoDB is listening on.

```Dockerfile
version: '3'
services:
  mongodb:
    image: mongo
    container_name: pinger-mongodb
    network_mode: host
    ports:
      - "27017:27017"
  backend:
    image: quay.io/zonggen/fcos-pinger-backend:latest
    container_name: pinger-backend
    network_mode: host
    ports:
      - "5000:5000"
    depends_on:
      - mongodb

```

Note that only the name `mongodb` will work on Openshift. None of `localhost`, `mongo`, or
`pinger-mongodb` would work. However, `mongodb`, `localhost` and `pinger-mongodb` would work with
`docker-compose up`. It makes sense given the meaning of the names: host internet `localhost`,
service name `mongodb`, image name `mongo` and container name `pinger-mongodb`.

Since containers are wrapped inside pods in Openshift/Kubernetes, communications between
containers/pods are through services. Therefore, it makes sense to use service name for
DNS server instead of localhost/container/image name.

In local docker-compose environment, since containers are using host network directly,
it makes sense that `localhost` will work. Also since there's no layer between containers
in docker-compose environment, accessing another container network through container name
or service name makes sense.

After hours of learning networks and Openshift/Kubernetes, the backend is finally up and running. :)
