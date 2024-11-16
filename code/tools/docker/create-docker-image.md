---
date: 2024-10-23T00:00:00.000Z
tags:
  - docker
hubs:
  - '[[]]'
urls:
  - null
---
# create-docker-image

## step to create

- go the docker hub and create repository
- in docker run command **docker build . -t name:tag example v1**
- then we will do tag todo that we have to login to the docker account
- the command for tag is **docker tag (name of the image):tag username/repository:tag**
- then **docker push username/repository:tag**
- to detele use **docker rmi -f** and imageID name
- to use write command **docker pull name/repository:tag**
- **docker run -d --name anyname user/repository:tag**
- **docker run -d --name kanchan-container -p 8080:80 -v /host/path:/container/path long104/kanchan:v2**

## command

- **docker rmi -f $(docker images -q):**
  - This will forcefully remove all images, even if they are being used.
- **docker image prune -a:**
  - To remove all unused images (including those not referenced by any container):
- **docker container prune:**
  - Use the following command to remove all stopped containers in one go:
- **docker builder prune**:
  * this will remove all unused build cache. You can add -f to skip the confirmation prompt.
- **docker system prune**:
  * This command will prompt you to confirm the deletion of all unused resources.
- **docker volume prune**:
  * To remove all unused volumes
- **docker network prune**:
  * Clean Up Unused Networks
- **docker system prune -a --volumes**:
  * a will remove all unused images, not just dangling ones.
  * Be cautious, as this will delete many resources and might affect your running applications.
  

## language

```yaml
# Use the official PHP image with Apache
FROM php:8.0-apache

# Install necessary PHP extensions
RUN docker-php-ext-install mysqli && docker-php-ext-enable mysqli

# Enable Apache mod_rewrite
RUN a2enmod rewrite

# Set the document root
ENV APACHE_DOCUMENT_ROOT /var/www/html

# Copy the application source code to the container
COPY src/ /var/www/html/

# Set proper permissions
RUN chown -R www-data:www-data /var/www/html

# Expose port 80
EXPOSE 80
```

```yaml
FROM node:14 AS node-build

WORKDIR /usr/src/app

COPY package*.json ./

RUN npm install

COPY . .

RUN npm run dg && npm run dm && npm run insert

FROM mysql:5.7 AS mysql-db

ENV MYSQL_ROOT_PASSWORD=rootpassword
ENV MYSQL_DATABASE=mydatabase
ENV MYSQL_USER=myuser
ENV MYSQL_PASSWORD=mypassword

COPY init.sql /docker-entrypoint-initdb.d/

FROM node:14

COPY --from=node-build /usr/src/app /usr/src/app

EXPOSE 3000

CMD ["npm", "start"]
```

- example for node
```sql
CREATE DATABASE mydatabase;
USE mydatabase;

CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(50) NOT NULL,
    email VARCHAR(100) NOT NULL
);

INSERT INTO users (username, email) VALUES ('testuser', 'test@example.com');
```
