# Jenkins-Docker-Django


## Instruction to run
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