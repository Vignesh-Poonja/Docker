# Attaching an Existing Docker Volume to Jenkins

This guide explains how to attach an existing Docker volume (`jenkins_home`) to Jenkins, ensuring persistent data storage and avoiding the need to reconfigure Jenkins on every restart.

## Prerequisites
- A running EC2 instance with Docker installed
- An existing Docker volume named `jenkins_home`
- No currently running Jenkins container

## Step 1: Verify the Existing Jenkins Volume
Run the following command to check if the `jenkins_home` volume exists:

```sh
docker volume ls
```

Expected output:
```
DRIVER    VOLUME NAME
local     jenkins_home
```

## Step 2: Stop and Remove Any Running Jenkins Container
If a Jenkins container is already running, stop and remove it:

```sh
docker ps
```
Find the Jenkins container ID and run:

```sh
docker stop <container_id>
docker rm <container_id>
```

## Step 3: Run Jenkins with the Existing Volume
Start a new Jenkins container while mounting the existing `jenkins_home` volume:

```sh
docker run -d --name jenkins \
  -p 8080:8080 -p 50000:50000 \
  -v jenkins_home:/var/jenkins_home \
  jenkins/jenkins:lts
```

### Explanation:
- `-d`: Runs the container in detached mode
- `--name jenkins`: Names the container as `jenkins`
- `-p 8080:8080 -p 50000:50000`: Maps necessary ports
- `-v jenkins_home:/var/jenkins_home`: Mounts the existing volume
- `jenkins/jenkins:lts`: Uses the latest Jenkins LTS image

## Step 4: Verify That Jenkins is Using the Correct Volume
Check if Jenkins is using the correct volume:

```sh
docker inspect jenkins | grep jenkins_home
```

Expected output:
```
"Destination": "/var/jenkins_home",
"Source": "/var/lib/docker/volumes/jenkins_home/_data",
```

Alternatively, list the contents of the volume:

```sh
docker run --rm -it -v jenkins_home:/var/jenkins_home ubuntu ls -l /var/jenkins_home
```

If you see files like `config.xml`, `jobs/`, and `plugins/`, Jenkins is correctly using the volume.

## Step 5: Access Jenkins
Open a web browser and navigate to:
```
http://<EC2-PUBLIC-IP>:8080
```
If using SSH port forwarding:
```
http://localhost:8080
```
Jenkins should load with your previous configurations, jobs, and plugins intact.

---
**Now, your Jenkins data will persist across container restarts!** 🚀

