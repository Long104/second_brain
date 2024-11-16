---
date: 2024-10-23T00:00:00.000Z
tags:
  - tool
hubs:
  - '[[]]'
urls:
  - null
---
# command

❯ docker run -d --name kanchan-app --network my_network -p 8000:80 long104/kanchan-app:v14
❯ docker network create my_network
❯ docker build -f Dockerfile.node -t long104/kanchan-db:v22 .
