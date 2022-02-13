# Jenkins-Docker-Django
09121777151

jaber

## Instruction to run

cd jenkins/master/
docker build -t jenkins-master .

cd jenkins/build-agent/
docker build -t jenkins-build-agent .

docker-compose -f docker-compose.jenkins.yml up

d3557ef98b324a5eba01283147d3eb32

ab153cb3895247109a50dbe1f21def1e









1- run `ssh-keygen -t rsa -f jenkins_agent` and replace public key in docker-compose agent. 


run `docker-compose up -d`

run `docker ps`. It should be three COntainer running. 
Find Container Id for jenkins (image jenkins/jenkins:lts-jdk11 ) and use it in below command to get initialAdminPassword from log

run `docker logs jenkins-container-id`  

Hit "http://127.0.0.1:8080/" in browser 

- instll all suggested plagins 
- Create a admin login
- select default url and Jenkisn is ready to use

### Jenkins Config
- Add private key in "Manage Jenkins/Manage Credentials/Jenkins/Global credentials". 
-- Click on "Add Credentials" and then select 
--- Kind: "SSH Username with private key"
--- Id : jenkins_agent
--- Username : jenkins
--- paste the generated private key in Direct Entry of Private key

- run `docker-compose down` and then `docker-compose up -d` and then login 

- Add New Node in "Manage Jenkins/Manage Nodes and Clouds"
-- Remote root directory to /home/jenkins/agent.
-- Use this node as much as possible under Usage.
-- Under Launch method, select Launch agents via SSH.
-- For Host, enter "agent"
-- Select Previous created Credintial names "jenkins" in Credentials
-- select "Non verifying Verification Strategy" for "Host Key Verification Strategy"
-- Set java Path in Advanced
--- java Path : /opt/java/openjdk/bin/java 
--- Timeout : 60, retries: 10 and Wait : 15




Check log : `docker-compose logs -f`

`docker-compose up -d --build`
`docker-compose exec app python manage.py migrate --noinput`

`docker-compose exec db psql --username=postgres --dbname=postgres`



------ Auth with Githib