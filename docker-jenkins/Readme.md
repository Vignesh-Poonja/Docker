# Jenkins in Docker

This repository contains a Dockerfile for running Jenkins inside a Docker container with additional dependencies such as Docker and Git pre-installed.

## Features
- Uses the latest official Jenkins image as the base.
- Installs necessary dependencies, including:
  - `docker.io` for running Docker commands inside Jenkins.
  - `git` for version control operations.
- Ensures the Jenkins user is added to the Docker group for executing Docker commands.
- Exposes Jenkins ports:
  - `8080` (Jenkins Web UI)
  - `50000` (JNLP agent communication)

## Prerequisites
- Docker installed on the host machine.
- Sufficient system resources to run Jenkins.

## Build the Docker Image
To build the custom Jenkins image, run:

```sh
 docker build -t custom-jenkins .
```

## Run the Container
To start a container using the built image:

```sh
 docker run -d --name jenkins-container -p 8080:8080 -p 50000:50000 --group-add 998 custom-jenkins
```

> **Note:** Ensure that the Docker group ID (`998`) matches the group ID of Docker on your system.

## Access Jenkins
Once the container is running, access Jenkins at:
```
http://localhost:8080
```

## Unlock Jenkins
To retrieve the initial admin password:

```sh
docker exec jenkins-container cat /var/jenkins_home/secrets/initialAdminPassword
```

## Customizing the Jenkins Setup
You can modify this Dockerfile to:
- Install additional plugins.
- Configure Jenkins settings using Groovy scripts.
- Include pre-installed tools and dependencies.

## Cleanup
To stop and remove the running container:

```sh
 docker stop jenkins-container && docker rm jenkins-container
```

To remove the built image:

```sh
 docker rmi custom-jenkins
```
