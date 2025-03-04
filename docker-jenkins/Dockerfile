# Use the latest Jenkins image
FROM jenkins/jenkins:latest

# Install dependencies for Docker and Git
USER root
RUN apt-get update && \
    apt-get install -y \
    software-properties-common \
    apt-transport-https \
    curl \
    ca-certificates \
    gnupg \
    lsb-release \
    docker.io \
    git \
    && curl -fsSL https://get.docker.com | sh \
    && git --version

# Ensure Docker group exists, then add Jenkins user to Docker group
RUN getent group docker || groupadd -g 998 docker && \
    usermod -aG docker jenkins

# Expose ports
EXPOSE 8080
EXPOSE 50000

# Start Jenkins
USER jenkins
ENTRYPOINT ["/usr/local/bin/jenkins.sh"]

