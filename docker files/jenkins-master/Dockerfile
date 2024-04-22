FROM jenkins/jenkins:lts-jdk17
USER root

# Add Docker's official GPG key:
RUN apt-get update
RUN apt-get install ca-certificates curl
RUN install -m 0755 -d /etc/apt/keyrings
RUN curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
RUN chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
RUN echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/debian \
  $(. /etc/os-release && echo "bookworm") stable" | \
  tee /etc/apt/sources.list.d/docker.list > /dev/null
RUN apt-get update

RUN apt-get install -y docker-ce

# Needed to allow jenkins to run docker comands without sudo, the GID needed may vary from 963
RUN groupmod -g 963 docker
RUN usermod -aG docker jenkins
# drop back to the regular jenkins user - good practice
USER jenkins