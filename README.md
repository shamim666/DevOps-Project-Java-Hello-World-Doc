# CI/CD PipeLine For a Java Project

## Used Technology:

1. GitHub
2. Jenkins
3. Maven
4. Ansible
5. Docker
6. Kubernetes

## Step 1

Our Source Code of a java application is kept on a GitHub repository.First we have set up a jenkins server for CI/CD pipeline.
Then with the help of Java build tool Maven jenkins will build the artifacts of our application. 

default locations of artifacts in jenkins 

#### /var/lib/jenkins/workplace  

## Step 2

Then Ansible comes into the picture. It is integrated with jenkins server
by SSH Publishers plugin. Jenkins will send the artifacts to Ansible server
at /opt/docker location. Then Docker will be installed in ansible and have made a Dockerfile
which is consisted of artifacts and tomcat webserver. Then make a playbook which main job is to
create a image of application from that Dockerfile and push it to DockerHub.This is the ultimate image of our application.
and the whole process is configured on Jenkins CI part.

## Step 3

This is the deployment section. In this section we have deployed our application into kubernetes cluster.
To make a kubernetes cluster first we have to make a kubernetes bootstrap server from where we can controll the kubernetes cluster.
Ansible server is integrated with kubernetes bootstrap server by SSH-Keygen based authentication.
and now make two yaml files for our application in bootstrap server.

#### 1. deployment.yml
#### 2. service.yml

Then make a playbook which will automate the deployment process of our application by using those two yml files.
The main task of deployment.yml is to pull the application's image from DockerHub and run it as pods and
the service.yml task is to expose the application to users.This CD section is configured on Jenkins CD part. 

Now if someone make any changes in source code then it is automatically reflected on deployed application through CI/CD Pipeline.


