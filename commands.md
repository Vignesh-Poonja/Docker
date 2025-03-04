# Docker Commands Cheat Sheet

This document provides a list of commonly used Docker commands to help you efficiently manage Docker containers, images, and networks.

## Table of Contents
- [Docker Images](#docker-images)
- [Docker Containers](#docker-containers)
- [Managing Containers](#managing-containers)
- [Managing Images](#managing-images)
- [Docker Volumes](#docker-volumes)
- [Docker Networks](#docker-networks)
- [Docker Compose](#docker-compose)
- [Other Useful Commands](#other-useful-commands)

---

## Docker Images

### **List available images**
```sh
docker images
```

### **Build an image from a Dockerfile**
```sh
docker build -t <image_name> .
```

### **Remove an image**
```sh
docker rmi <image_id>
```

### **Download an image from Docker Hub**
```sh
docker pull <image_name>
```

### **Push an image to Docker Hub**
```sh
docker push <image_name>
```

---

## Docker Containers

### **Run a new container**
```sh
docker run -d -p 8080:80 --name <container_name> <image_name>
```
- `-d` runs the container in detached mode (background).
- `-p 8080:80` maps port 8080 on the host to port 80 in the container.
- `--name` assigns a name to the container.

### **List running containers**
```sh
docker ps
```

### **List all containers (including stopped ones)**
```sh
docker ps -a
```

### **Stop a running container**
```sh
docker stop <container_id>
```

### **Start a stopped container**
```sh
docker start <container_id>
```

### **Restart a container**
```sh
docker restart <container_id>
```

### **Remove a stopped container**
```sh
docker rm <container_id>
```

### **Remove all stopped containers**
```sh
docker container prune
```

---

## Managing Images

### **Remove an image**
```sh
docker rmi <image_id>
```

### **Remove all unused images**
```sh
docker image prune
```

### **Remove all unused images, containers, and networks**
```sh
docker system prune -a
```

---

## Docker Volumes

### **List all volumes**
```sh
docker volume ls
```

### **Create a new volume**
```sh
docker volume create <volume_name>
```

### **Inspect a volume**
```sh
docker volume inspect <volume_name>
```

### **Remove a volume**
```sh
docker volume rm <volume_name>
```

### **Remove all unused volumes**
```sh
docker volume prune
```

---

## Docker Networks

### **List all networks**
```sh
docker network ls
```

### **Create a new network**
```sh
docker network create <network_name>
```

### **Connect a container to a network**
```sh
docker network connect <network_name> <container_name>
```

### **Disconnect a container from a network**
```sh
docker network disconnect <network_name> <container_name>
```

### **Remove a network**
```sh
docker network rm <network_name>
```

### **Remove all unused networks**
```sh
docker network prune
```

---

## Docker Compose

### **Start services defined in `docker-compose.yml`**
```sh
docker-compose up -d
```

### **Stop services**
```sh
docker-compose down
```

### **List services**
```sh
docker-compose ps
```

### **Restart services**
```sh
docker-compose restart
```

### **Rebuild services**
```sh
docker-compose build
```

---

## Other Useful Commands

### **Run a command inside a running container**
```sh
docker exec -it <container_id> bash
```

### **Copy files from container to host**
```sh
docker cp <container_id>:/path/to/file /host/destination
```

### **View container logs**
```sh
docker logs <container_id>
```

### **View resource usage of containers**
```sh
docker stats
```

### **Inspect container details**
```sh
docker inspect <container_id>
```

---

## Conclusion
This cheat sheet provides essential Docker commands for managing containers, images, networks, and volumes efficiently. Keep this handy while working with Docker to streamline your workflow. 🚀

