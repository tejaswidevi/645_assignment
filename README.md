# 645_assignment
Introduction  : 

This assignment  details the containerization, deployment, and automation of the web application you created in Assignment 1 Part 2. We will achieve this by utilizing Docker for self-contained, portable application units, deploying them on the container orchestration platform Kubernetes with simplified management through Rancher. Finally, a CI/CD pipeline built with Jenkins will automate building and deployment for efficient development workflows. 

Repository Setup :

The foundation for this project was established by creating a GitHub repository. This repository stores all the source code and related files for the web application developed in Assignment 1 Part 2. Additionally, Dockerfile and Jenkinsfile were added to facilitate containerization and automate the build and deployment process through a CI/CD pipeline.

1.GitHub repository: Centralized storage for source code and related files.
2.Docker file: Instructions for building Docker containers.
3.Jenkins file: Script for automating the CI/CD pipeline.

Git repository link : https://github.com/tejaswidevi/645_assignment


Application Containerization :

1)WAR File Creation: We used the jar command to create a file named tej123.war.This file packages all the application's files for deployment on a Java server like Tomcat.
2)Building the Docker Image: A file called Dockerfile was created. This file contains instructions for building a Docker image specifically designed for our application. The image is based on Tomcat and incorporates the tej123.war file.
3)Creating the Docker Image: Once the Dockerfile was ready, we used the command docker build -t tejaswi251100/tejaswidevi . This command builds the Docker image based on the instructions in the Dockerfile.
4)Pushing the Image to Docker Hub: Finally, the created image was pushed to a public repository called Docker Hub using the command docker push tejaswi251100/tejaswidevi. This allows us to share and access the image from anywhere.

Building the Infrastructure: EC2 Instances:

Details the configuration of three EC2 instances to establish our deployment pipeline:

1.Rancher Server (Master Node): This instance serves as the central control point by running Rancher, a tool that simplifies Kubernetes cluster management.
2.Worker Node: This instance acts as a worker node within the Kubernetes cluster, responsible for running containerized applications like our web app.
3.Jenkins Server: This dedicated instance runs Jenkins, a popular automation tool that will manage the CI/CD pipeline for our application.

Configuring the Rancher Server:

Each EC2 instance requires Docker installation for containerized application management.  We'll use the command sudo apt install docker.io to achieve this.

Following Docker installation, the Rancher server requires a specific Docker image to run Rancher and Kubernetes. This image can be downloaded and deployed using the command sudo docker run --privileged -d --restart=unless-stopped -p 80:80 -p 443:443 rancher/rancher.

After successful deployment, access the Rancher UI through a web browser to create and manage your Kubernetes cluster.



Worker Node EC2:

To add an EC2 instance as a node to a Kubernetes cluster, use the command supplied in the Rancher UI. To build up a deployment workload in Rancher, use the docker image name as the input. This delivers the application to the Kubernetes cluster we established.

Jenkins Server Setup:

Installation: A dedicated EC2 instance will be configured as the Jenkins server. We'll install Jenkins on this instance.
 using the command  - sudo apt-get install jenkins.

Starting Jenkins: Following installation, the Jenkins service will be started using the command sudo systemctl start jenkins.

CI/CD Pipeline Creation: Within Jenkins, we'll define a pipeline that automates the deployment process. This pipeline will be triggered whenever a code commit is pushed to the GitHub repository.

 The Jenkins pipeline will consist of several automated stages:
1)Code Retrieval: The pipeline will automatically check out the latest code from the GitHub repository.
2)WAR File Building: The pipeline will execute commands to build a WAR file containing the application code.
3)Docker Image Creation: Based on the WAR file, the pipeline will construct a new Docker image for our application.
4)Docker Image Push: The newly created Docker image will be pushed to a public repository like Docker Hub.
5)Kubernetes Redeployment: Once the image is pushed, the pipeline will utilize kubectl commands to instruct Kubernetes to redeploy the application using the latest Docker image. This effectively updates the application running on the cluster.
