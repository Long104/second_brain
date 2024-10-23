---
date: 2024-10-20T00:00:00.000Z
tags:
  - kubernetes
hubs:
  - '[[]]'
urls:
  - 'https://www.youtube.com/watch?v=_BfC7yk6zco&t=327s'
---
# Contents

<!-- toc -->

- [Kubernetes or k8s](#kubernetes-or-k8s)
  - [What it is?](#what-it-is)
  - [Usage](#usage)
  - [Kubernetes cluster](#kubernetes-cluster)
  - [Load balancer](#load-balancer)
  - [using Kubernetes in docker destop is not like real case](#using-kubernetes-in-docker-destop-is-not-like-real-case)
  - [Services](#services)

<!-- tocstop -->

# Kubernetes or k8s

## What it is?

- It is **Container Orchestration System** just like when the app in the vm clash it take time and its not good
  and have to create lots of instance manually which is not good

- Managing container automatic which will have application running and working
  together

## Usage

- Easy to rollback
- No force connect to cloud
- more stable
- manage server automatic and easy to deploy and more complicated
- serverless
- Can manage api and database separate

## Kubernetes cluster

- **Cluster** is like a big white space which in the big space there is worker node which is like one computer
- In the **worker node** there is Kubernetes in there there is two component. One
  is managing and second is application. In the application there is container
  which in the pod. The container run in the pod
- **Worker node**:
  - **kubelet**: it role is to communicate with main api
  - **Docker**: Container Engine
  - **Kube Proxy**: network what to connect to the pod
- Can run many pod in one worker node up to the usage
- **Master node**:
  - Use to manage worker node which have:
    - **API serve**: developer shoot api to the server and let it manage worker node in which
      what we want to do and what we need to manage the worker node which can
      control many worker node
    - **Scheduler**: We want to increase the pod the Scheduler can increase the pod
      by increase pod to the new worker node if the old worker node memory is already
      full and if not the it will increase the pod to the worker node if the
      worker memory is not full
    - **Controller Manager**: look for the resource when the pod is crash the
      controller will communicate with Scheduler to increase the new pod
      to the worker node which master node is working automatic

![[Screenshot 2567-10-22 at 15.47.28.png]]

## Load balancer

- when the client use the application through load balancer when send request
  to web app and web api and web api will communicate with database

## using Kubernetes in docker destop is not like real case

- in real case there is worker node and master node but when we use for testing
  everything is it single node
- single node:
  ![[Screenshot 2567-10-22 at 16.32.30.png]]

## Services

- **Node Port**: role is to open the port so the user can communicate with
  application work like node balancer:
  - Node Port range is between 30000 - 32767
- **Cluster IP**: Is like node port but use only internal inside the kubernetes
  cluster. If user outside want to use they can't only the internal. Use for
  pod and services
- **Load Balancer**: Role is to load balance the resouce form the outside and it's
  load balancer
- **External (Ingress)**: Add later to kubernetes it's external which is
  ingress:
  - real: it's not service but like component or object it's import for spread
    the traffic to other survice up to the routing rule that we choose it work
    like load balance
  - example:
    - xxx.com/api -> api Service
    - xxx.com/images -> Storage service
    - xxx-com -> web service

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: example-ingress
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  rules:
    - host: example.com
      http:
        paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: frontend-service
                port:
                  number: 80
          - path: /api
            pathType: Prefix
            backend:
              service:
                name: api-service
                port:
                  number: 80
          - path: /admin
            pathType: Prefix
            backend:
              service:
                name: admin-service
                port:
                  number: 80
```

- **DNS (service)**: for the kubernetes the metadata is already the http name for
  example **mango-deployment** will be **"mongodb://mongo-service"** or the
  backend can be **("<http://server-service>")** we use cluster ip
- pvc persistent volume cliam: use for store persistent data from database
