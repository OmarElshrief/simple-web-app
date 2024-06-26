pipeline {
    agent any

    environment {
        DOCKER_IMAGE_NAME = 'omarelshrief/simple-web-app'
        DOCKERFILE_PATH =  '-f /var/jenkins_home/workspace/CICD_pipeline/Dockerfile /var/jenkins_home/workspace/CICD_pipeline'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image
                    docker.build(env.DOCKER_IMAGE_NAME, env.DOCKERFILE_PATH)
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    // Push the Docker image to a registry (if needed)
                    docker.withRegistry('https://index.docker.io/v1/', 'DockerhubCre') {
                        docker.image(env.DOCKER_IMAGE_NAME).push('latest')
                    }
                }
            }
        }

	    stage('Deploy to Minikube') {
            steps {
                script {
                    // Deploy the Docker image to Minikube
                    sh "kubectl apply -f deployment.yaml"
                }
            }
        }

        stage('Integration Test') {
            steps {
                script{
                    POD_NAME = sh(script: "kubectl get pods -l app=my-nginx -o jsonpath='{.items[0].metadata.name}'", returnStdout: true).trim()
                    sh "kubectl port-forward ${POD_NAME} 8099:80 &"
                    sh 'curl -s http://localhost:8099' // Example test for content verification
                }
            }
        }
    }
}
