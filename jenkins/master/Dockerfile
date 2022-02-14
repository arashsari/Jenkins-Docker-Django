FROM jenkins/jenkins:lts-jdk11


RUN /usr/local/bin/install-plugins.sh git mstest matrix-auth workflow-aggregator docker-workflow blueocean credentials-binding

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

ENV JENKINS_USER admin
ENV JENKINS_PASS admin

# Skip initial setup
ENV JAVA_OPTS -Djenkins.install.runSetupWizard=false
# ENV JAVA_ARGS -Dhudson.security.csrf.DefaultCrumbIssuer.EXCLUDE_SESSION_ID=true
# ENV JAVA_ARGS "-Dhudson.security.csrf.DefaultCrumbIssuer.EXCLUDE_SESSION_ID=true"
COPY executors.groovy /usr/share/jenkins/ref/init.groovy.d/
COPY default-user.groovy /usr/share/jenkins/ref/init.groovy.d/

VOLUME /var/jenkins_home