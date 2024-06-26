# simple-nginx-web-application


## Preface
This repository is the sample of web application CI/CD using Jenkins.
This sample uses [Nginx](https://www.nginx.com/) as web server, [Minikube](https://minikube.sigs.k8s.io/docs/) as Container Orchestration Platform and [Docker](https://www.docker.com/) as Containerization platform.

This application contains the static contents such as html file, css file and javascript file to easily check the behavior of those functions.
So, you can check this application without starting a web server for front end.
Please refer to the 'services' section about checking the behavior of this application.

If you would like to develop a web application using Nginx, please feel free to use this sample.

## Services
This sample provides 3 services:   
    1- Jenkins follows GitHub repository for any updates.  
    2- Building Docker image for nginx server with the updates and pushing it to DockerHub.  
    3- Deployment of the web application using Minicube.

## Install
Perform the following steps:
1. Download and install Docker.
1. Download and install Minikube & Kubectl.

## Starting Server
1. Run Jenkins Container:
    ```bash
    #run jenkins as docker container:

    sudo docker run -p 8080:8080 -p 50000:50000 -d \
     -v jenkins_home:/var/jenkins_home \
     -v /var/run/docker.sock:/var/run/docker.sock \
     -v $(which docker):/usr/bin/docker jenkins/jenkins 

    #to make docker engine accessable
    sudo chmod 666 /var/run/docker.sock 
    ```
1. Integrate Jenkins with Minikube using secret file in jenkins gui:  
    ![Minikube_cloud](https://github.com/OmarElshrief/simple-web-app/blob/main/screenshots/Minikube_cloud.png)
   
1. Make you Credentials in Jenkins GUI:  
   ![Credentials](https://github.com/OmarElshrief/simple-web-app/blob/main/screenshots/Credentials.png)
   
1. Make new Pipeline Item:   
    ![Pipeline_item](https://github.com/OmarElshrief/simple-web-app/blob/main/screenshots/Pipeline_item.png)
   
1. Add github repo URL:   
    ![github_url](https://github.com/OmarElshrief/simple-web-app/blob/main/screenshots/github_url.png)
   
1. Save and Build the Pipeline:  
   note :: change ENV Variables and port in Integration Test stage.    
    ![pipeline_Run](https://github.com/OmarElshrief/simple-web-app/blob/main/screenshots/pipeline_Run.png)

### In your Server:  
Run :  
    ![kubectl_Run](https://github.com/OmarElshrief/simple-web-app/blob/main/screenshots/kubectl_Run.png)

### Congratulations your app up and running!  
Run:  
    ![web_page](https://github.com/OmarElshrief/simple-web-app/blob/main/screenshots/web_Page.png)

