# Containers-on-Elastic-Beanstalk

Here’s a sample README file you can use for your project:

---

# Dockerized Nginx Web Application with AWS Elastic Beanstalk

This project demonstrates how to create a custom Docker image with Nginx, build and run it locally, and deploy the containerized app to AWS Elastic Beanstalk. The web application is served using a custom `index.html` file and deployed on the cloud for accessibility via a web browser.

## Project Overview

- **Docker** is used to build a custom container image containing Nginx.
- **Nginx** serves a custom HTML page (`index.html`) inside the container.
- **AWS Elastic Beanstalk** is used to deploy the Dockerized application in the cloud, where it can be accessed globally.

## Table of Contents

1. [Prerequisites](#prerequisites)
2. [Setting Up Docker](#setting-up-docker)
3. [Building and Running the Custom Docker Image](#building-and-running-the-custom-docker-image)
4. [Deploying to AWS Elastic Beanstalk](#deploying-to-aws-elastic-beanstalk)
5. [Troubleshooting](#troubleshooting)
6. [Conclusion](#conclusion)

---

## Prerequisites

Before you start, make sure you have the following tools installed:

- **Docker Desktop**: [Install Docker](https://www.docker.com/products/docker-desktop)
- **AWS CLI**: [Install AWS CLI](https://aws.amazon.com/cli/)
- **Elastic Beanstalk CLI**: [Install Elastic Beanstalk CLI](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/eb-cli3-install.html)

Additionally, ensure that you have an AWS account and the required permissions to create Elastic Beanstalk environments.

---

## Setting Up Docker

1. **Install Docker**:
   Follow the instructions on the official Docker website to install Docker Desktop for your operating system (Windows/macOS).

2. **Start Docker Desktop**:
   Open Docker Desktop after installation to ensure Docker is running locally.

---

## Building and Running the Custom Docker Image

1. **Create a new directory** for your project:

   mkdir nginx-docker
   cd nginx-docker
   

2. **Create the `index.html` file**:
   Inside the `nginx-docker` directory, create a custom `index.html` file:
 
   <!DOCTYPE html>
   <html lang="en">
     <head>
       <meta charset="UTF-8" />
       <meta name="viewport" content="width=device-width, initial-scale=1.0" />
       <title>My Dockerized Nginx App</title>
     </head>
     <body>
       <h1>Hello from my custom Nginx Docker container!</h1>
     </body>
   </html>
   

3. **Create the `Dockerfile`**:
   In the same directory, create a `Dockerfile` with the following contents:
   
   # Use the latest Nginx image
   FROM nginx:latest

   # Copy the custom index.html to the Nginx web server directory
   COPY ./index.html /usr/share/nginx/html/

   # Expose port 80 for the web server
   EXPOSE 80
   

4. **Build the Docker image**:
   In the terminal, run the following command to build the custom Docker image:
   
   docker build -t my-custom-nginx .
   

5. **Run the Docker container locally**:
   Once the image is built, run the container with the following command:
   
   docker run -d -p 80:80 my-custom-nginx
   

   This command will map port 80 on your local machine to port 80 inside the container and start the Nginx server to serve the custom `index.html`.

6. **Test Locally**:
   Open your browser and navigate to `http://localhost`. You should see the message "Hello from my custom Nginx Docker container!".

---

## Deploying to AWS Elastic Beanstalk

1. **Configure AWS CLI**:
   If you haven’t already, configure the AWS CLI with your credentials:
  
   aws configure
   

2. **Install Elastic Beanstalk CLI**:
   If you haven't already, install the EB CLI. This tool will help you interact with AWS Elastic Beanstalk from the command line.

3. **Initialize Elastic Beanstalk Environment**:
   In your project directory, run:
  
   eb init
   
   Follow the prompts to select your AWS region, application name, and platform (choose Docker).

4. **Create and Deploy the Elastic Beanstalk Environment**:
   Create an Elastic Beanstalk environment and deploy your application:
   
   eb create my-nginx-env
   eb deploy
  

   Elastic Beanstalk will take care of provisioning the necessary EC2 instances, load balancer, and auto-scaling groups.

5. **Access Your Application**:
   After deployment, you can access the application through the provided URL:
   
   eb open
   

   Your application should now be running on AWS Elastic Beanstalk and accessible via a public URL.

---

## Troubleshooting

- **Port Conflict**: If you encounter a port conflict (e.g., port 80 is already in use by another container), stop the conflicting container by running:
  
  docker stop <container_id>

- **Elastic Beanstalk Errors**: If Elastic Beanstalk fails to deploy the application, check the logs using:
 
  eb logs

---

## Conclusion

In this project, you’ve learned how to:

- **Install Docker** and manage containers locally.
- **Build a custom Docker image** for an Nginx web server serving a custom HTML page.
- **Deploy the Dockerized app to AWS Elastic Beanstalk**, making your application accessible from anywhere in the world.

With this knowledge, you can now create, deploy, and manage containerized applications in the cloud with ease!

---
