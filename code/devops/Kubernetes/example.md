---
date: 2024-10-22T00:00:00.000Z
tags:
  - kubernetes
hubs:
  - '[[]]'
urls:
  - null
---
# practical

- pod is the smallest unit in kubernetes:

  - In pod there is container and application in there

- multiple of pod

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: client-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: client
  template:
    metadata:
      name: cilent-pods
      labels:
        app: client
    spec:
      containers:
        - name: client
          image: dekcode/todo-app:v4
```

- single pod

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: cilent-pods
  labels:
    app: client
spec:
  containers:
    - name: client
      image: dekcode/todo-app:v4
```

## Everthing

- for client

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: client-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: client
  template:
    metadata:
      name: cilent-pods
      labels:
        app: client
    spec:
      containers:
        - name: client
          image: dekcode/todo-app:v4
---
apiVersion: v1
kind: Service
metadata:
  name: client-service
spec:
  type: NodePort
  selector:
    app: client
  ports:
    - port: 80
      targetPort: 80
      nodePort: 30001
```

- for server

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: server-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: server
  template:
    metadata:
      name: server-pods
      labels:
        app: server
    spec:
      containers:
        - name: server
          image: dekcode/todo-api:v5
---
apiVersion: v1
kind: Service
metadata:
  name: server-service-nodeport
spec:
  type: NodePort
  selector:
    app: server
  ports:
    - port: 80
      targetPort: 80
      nodePort: 30002
---
apiVersion: v1
kind: Service
metadata:
  name: server-service
spec:
  type: ClusterIP
  selector:
    app: server
  ports:
    - port: 80
      targetPort: 80
```

- for mongo

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mongo-deployment
spec:
  replicas: 1
  selector:
    matchLabels:
      app: mongo
  template:
    metadata:
      name: mongo-pods
      labels:
        app: mongo
    spec:
      containers:
        - name: mongo
          image: mongo
---
apiVersion: v1
kind: Service
metadata:
  name: mongo-service
spec:
  type: ClusterIP
  selector:
    app: mongo
  ports:
    - port: 27017
      targetPort: 27017
```

- mongo for persistent storage

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: mongo-pvc
spec:
  accessModes:
    - ReadWriteMany
  resources:
    requests:
      storage: 1Gi
```

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mongo-deployment
spec:
  replicas: 1
  selector:
    matchLabels:
      app: mongo
  template:
    metadata:
      name: mongo-pods
      labels:
        app: mongo
    spec:
      containers:
        - name: mongo
          image: mongo
          volumeMounts:
            - name: mongo-storage
              mountPath: /data/db # this is the default path for mongo
      volumes:
        - name: mongo-storage # so it use the mongo-storage name to use pvc
          persistentVolumeClaim:
            claimName: mongo-pvc
---
apiVersion: v1
kind: Service
metadata:
  name: mongo-service
spec:
  type: ClusterIP
  selector:
    app: mongo
  ports:
    - port: 27017
      targetPort: 27017
```
