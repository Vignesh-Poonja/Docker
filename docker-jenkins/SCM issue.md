# Troubleshooting Jenkins Git SCM Issue

## Issue:
Jenkins fails to connect to the Git repository with the error:
```
Failed to connect to repository: Error performing git command: ls-remote -h https://github.com/your-repo.git HEAD
```

## Root Cause:
Jenkins may not be using the correct Git executable path, or the container lacks the necessary permissions.

## Solution:

### 1. Verify Git is Installed in Jenkins Container
If Jenkins is running inside a Docker container, check whether Git is installed and accessible.
```sh
# Access the Jenkins container
docker exec -it jenkins bash

# Switch to Jenkins user (if not already)
su - jenkins

# Check Git version
git --version

# Verify Git can reach the repository
git ls-remote https://github.com/your-repo.git
```
If this command returns the repository details, Git is correctly installed and working inside the container.

### 2. Update Git Path in Jenkins SCM
1️⃣ Open the Jenkins job where the error occurs.
2️⃣ Scroll to **Source Code Management (SCM)**.
3️⃣ Under **Git**, expand **Advanced**.
4️⃣ In **Path to Git executable**, enter:
   ```
   /usr/bin/git
   ```
5️⃣ Click **Save** and **Build Now**.

### 3. Restart Jenkins
If the issue persists, restart the Jenkins container:
```sh
docker restart jenkins
```

### 4. Check Permissions on Jenkins Volume
Ensure Jenkins has the correct ownership and permissions:
```sh
docker exec -it jenkins bash
ls -ld /var/jenkins_home
```
Expected output:
```
drwxr-xr-x 16 jenkins jenkins 4096 Mar 17 11:36 /var/jenkins_home
```
If ownership is incorrect, fix it using:
```sh
chown -R jenkins:jenkins /var/jenkins_home
chmod -R 755 /var/jenkins_home
```

### 5. Ensure Proper Network Connectivity
Check if Jenkins can reach GitHub:
```sh
curl -v https://github.com
```
If this fails, ensure your container has internet access.

## Conclusion
After applying these steps, retry the Jenkins job. The Git repository should now be accessible without errors. 🚀

