---
date: 2024-10-22T00:00:00.000Z
tags:
  - kubernetes
hubs:
  - '[[]]'
urls:
  - null
---
# ingress

## nginx

- kubectl apply -f <https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.12.0-beta.0/deploy/static/provider/cloud/deploy.yaml>:
  - **to delete**: kubectl delete -f <https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.12.0-beta.0/deploy/static/provider/cloud/deploy.yaml>
  - **to view**: kubectl get all -n ingress-nginx
  - **to completely delete**: kubectl delete namespace ingress-nginx

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: igress-service
  annotations:
    kubernetes.io/ingress.class: nginx
    # nginx.ingress.kubernetes.io/use-regex: "true"
spec:
  ingressClassName: nginx
  rules:
    - host: todo.com
      http:
        paths:
          - path: /api/
            pathType: Prefix
            backend:
              service:
                name: server-service
                port:
                  number: 80 # use the port not target port
          - path: /
            pathType: Prefix
            backend:
              service:
                name: client-service
                port:
                  number: 80 # use the port not target port
```

- add 127.0.0.1 todo.com after the ::1 localhost to the /etc/hosts add use this command to keep change:
  - sudo dscacheutil -flushcache
    sudo killall -HUP mDNSResponder
