# Pushing a Docker Image to Docker Hub

This guide explains how to push a custom Jenkins Docker image (`custom-jenkins-latest-with-docker-and-git`) to Docker Hub.

## Steps to Push an Image to Docker Hub

### 1️⃣ Log in to Docker Hub
Before pushing an image, log in to your Docker Hub account:
```sh
docker login -u "your_username"
```

If using AWS EC2 and need a non-interactive login:
```sh
echo "your_password" | docker login -u "your_username" --password-stdin
```
![image](https://github.com/user-attachments/assets/1555f5ec-d690-4ddf-9df9-37f24637f23d)

### 2️⃣ Tag the Docker Image
Docker Hub requires images to have a **namespace** (your Docker Hub username or organization). Tag the image accordingly:
```sh
docker tag custom-jenkins-latest-with-docker-and-git your-dockerhub-username/jenkins-latest:<tag>
```

For example:
```sh
docker tag custom-jenkins-latest-with-docker-and-git vk62/jenkins-latest:v1
```

### 3️⃣ Push the Image to Docker Hub
After tagging, push the image:
```sh
docker push your-dockerhub-username/jenkins-latest:<tag>
```
![image](https://github.com/user-attachments/assets/1ddaa2a6-8376-48b2-b383-3a5cdc3445ac)


Example:
```sh
docker push vk62/jenkins-latest:v1
```

### 4️⃣ Verify the Image on Docker Hub
1. Log in to [Docker Hub](https://hub.docker.com/)
2. Navigate to **Repositories**
3. You should see the `jenkins-latest` image listed under your account

![image](https://github.com/user-attachments/assets/f3d5ee98-ca03-439b-b3ea-cadc1774c7ce)


### 5️⃣ Pull the Image from Another Machine
To test the uploaded image, try pulling it from another machine:
```sh
docker pull your-dockerhub-username/jenkins-latest:<tag>
```
Example:
```sh
docker pull vk62/jenkins-latest:v1
```
![image](https://github.com/user-attachments/assets/4e5f2826-b201-448d-bd8a-c05f4b707942)


## 📌 Notes
- Ensure Docker is installed on your system before performing these steps.
- If using **private repositories**, ensure your authentication is correct before pushing.
- Replace `your-dockerhub-username` with your actual Docker Hub username.
- Replace `<tag>` with an appropriate version number (e.g., `v1`, `latest`).


🚀 Now your custom Jenkins Docker image is successfully pushed to Docker Hub and ready for use!

