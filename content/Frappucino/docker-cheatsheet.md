---
tags:
  - cheatsheet
title: Docker Cheat Sheet
---
# Docker Cheat Sheet

> Docker is a tool that lets you package applications into **containers**: lightweight, portable environments that include everything needed to run your app.

---

# Basic Concepts

|Concept|Meaning|
|---|---|
|Image|Blueprint (read-only template)|
|Container|Running instance of an image|
|Dockerfile|Instructions to build an image|
|Volume|Persistent storage|
|Network|Communication between containers|

---

# Images

## Pull an image

```bash
docker pull nginx
```

## List images

```bash
docker images
```

## Remove image

```bash
docker rmi nginx
```

## Build image from Dockerfile

```bash
docker build -t my-app .
```

---

# Containers

## Run a container

```bash
docker run nginx
```

## Run in background (detached)

```bash
docker run -d nginx
```

## Name a container

```bash
docker run --name web nginx
```

## Map ports

```bash
docker run -p 8080:80 nginx
```

(host:container)

---

## List containers

```bash
docker ps        # running
docker ps -a     # all
```

---

## Stop / start / restart

```bash
docker stop container_id
docker start container_id
docker restart container_id
```

---

## Remove container

```bash
docker rm container_id
```

Force remove running container:

```bash
docker rm -f container_id
```

---

## Execute inside container

```bash
docker exec -it container_id bash
```

or:

```bash
docker exec -it container_id sh
```

---

# Logs & Inspection

## View logs

```bash
docker logs container_id
```

Follow logs live:

```bash
docker logs -f container_id
```

---

## Inspect container

```bash
docker inspect container_id
```

---

# Dockerfile Basics

Example:

```dockerfile
FROM node:18

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .

EXPOSE 3000

CMD ["npm", "start"]
```

---

## Build from Dockerfile

```bash
docker build -t my-node-app .
```

---

# Volumes

## Create volume

```bash
docker volume create mydata
```

## Run with volume

```bash
docker run -v mydata:/data nginx
```

## Bind mount (local folder)

```bash
docker run -v $(pwd):/app nginx
```

---

# Networks

## List networks

```bash
docker network ls
```

## Create network

```bash
docker network create mynet
```

## Run container in network

```bash
docker run --network mynet nginx
```

---

# Docker Compose (multi-container)

## Example file

```yaml
version: "3.9"

services:
  app:
    build: .
    ports:
      - "3000:3000"
    volumes:
      - .:/app

  db:
    image: postgres
    environment:
      POSTGRES_PASSWORD: example
```

---

## Commands

Start services:

```bash
docker compose up
```

Detached mode:

```bash
docker compose up -d
```

Stop services:

```bash
docker compose down
```

Rebuild:

```bash
docker compose up --build
```

---

# Cleanup

## Remove unused containers

```bash
docker container prune
```

## Remove unused images

```bash
docker image prune
```

## Full system cleanup (dangerous)

```bash
docker system prune -a
```

---

# Debugging

## View resource usage

```bash
docker stats
```

## Check disk usage

```bash
docker system df
```

---

# Useful Shortcuts

```text
docker ps -a          # all containers
docker images         # all images
docker exec -it       # enter container
docker logs -f        # live logs
docker stop $(docker ps -q)
docker rm $(docker ps -aq)
```

---

# Port Mapping Mental Model

```text
Host Machine        Container
------------        ----------
localhost:8080  →   80 (nginx)
localhost:3000  →   3000 (node)
```

---

# Key Idea

Docker isolates applications like:

> "Run everything as if it has its own computer"

But:

- shares kernel
    
- stays lightweight
    
- runs anywhere
    

---

# Most Used Commands

```text
docker pull
docker run
docker ps
docker stop
docker rm
docker build
docker exec
docker logs
docker compose up
docker compose down
```

---

# Golden Workflow

```bash
docker build -t my-app .

docker run -p 3000:3000 my-app

docker ps

docker logs -f container_id

docker stop container_id
```

---