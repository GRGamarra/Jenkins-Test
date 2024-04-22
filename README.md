## Jenkins-Test
Meaning for the added files and folders:
+ `docker-files/` Contains all of the Dockerfiles that will be used either for Jenkins, testing or building containers;
+ `jenkins-data/` Contains the base content of the jenkins_home folder (used for data persistency);
+ `.mvn/wrapper/, .settings/, src/, .classpath, .project, mvnw, mvnw.cmd, pom.xml` All belong to the Springboot Rest API application project (this was the content after unzipping the demo.zip file);
+ `Jenkinsfile` Contains the Pipeline that the Pipeline Job will have to follow in order to build, test and deploy the Rest API;
+ `helloworld.py` Is a file used for testing commit responses, signatures, and so on.

### Setup
> Before proceeding with the Setup remember to store the `docker-files/` and `jenkins-data/` folders on your machine.

The following commands should be used in order to set up the base system from scratch: <br />
Building and running the provided **Jenkins Dockerfile**
```
docker build -t jenkins/master /docker-files/jenkins-master
```
```
docker run --name jenkins-master --restart=on-failure --detach -v /jenkins-data:/var/jenkins_home -v /var/run/docker.sock:/var/run/docker.sock -p 8080:8080 jenkins/master:latest
```
> [!CAUTION]
> It is required to look for the GID of Docker in your host machine, and change its value in the Dockerfile of Jenkins, otherwise it will not have the permission to run the Docker commands.

Building the provided **Java and Python3 Dockerfiles**
```
docker build -t java-base /docker-files/java-base
```
```
docker build -t python3-base /docker-files/python3-base
```

> [!NOTE]
> Remember to use the path to your jenkins-data folder and to your dockerfiles instead of leaving them as typed in the examples.
