FROM jenkins/ssh-agent:jdk11
# FROM ubuntu:18.04

# Install Docker CLI
RUN apt-get update && apt-get install -y apt-transport-https ca-certificates curl gnupg lsb-release software-properties-common

# RUN apt-get remove docker docker-engine docker.io containerd runc 
# RUN curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -
# RUN apt-key fingerprint 0EBFCD88
# RUN add-apt-repository \
#    "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
#    $(lsb_release -cs) \
#    stable"
# RUN apt-get update && apt-get -y install docker-ce


USER root

RUN apt-get update && \
    apt-get -y install \
    apt-transport-https \
    ca-certificates \
    gnupg2 \
    software-properties-common
RUN curl -fsSL https://download.docker.com/linux/$(. /etc/os-release; echo "$ID")/gpg | apt-key add -
RUN add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/$(. /etc/os-release; echo "$ID") \
   $(lsb_release -cs) \
   stable" 
RUN apt-get update && apt-get -y install docker-ce


# RUN apt-get update && apt-get install -y openjdk-8-jre curl python python-pip git
# RUN pip install jenkins-webapi 

# Get docker-compose in the agent container

RUN curl -L https://github.com/docker/compose/releases/download/1.21.2/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose && chmod +x /usr/local/bin/docker-compose
RUN mkdir -p /home/jenkins
RUN mkdir -p /var/lib/jenkins

# ADD slave.py /var/lib/jenkins/slave.py

WORKDIR /home/jenkins

ENV JENKINS_URL "http://jenkins:8080"
ENV JENKINS_SLAVE_ADDRESS ""
ENV JENKINS_USER "admin"
ENV JENKINS_PASS "admin"
ENV SLAVE_NAME ""
ENV SLAVE_SECRET ""
ENV SLAVE_EXECUTORS "1"
ENV SLAVE_LABELS "docker"
ENV SLAVE_WORING_DIR ""
ENV CLEAN_WORKING_DIR "true"

# ENV JAVA_ARGS "-Dhudson.security.csrf.DefaultCrumbIssuer.EXCLUDE_SESSION_ID=true"


# CMD [ "python", "-u", "/var/lib/jenkins/slave.py" ]

