pipeline {
    agent any
    
    environment {
        DOCKER_REGISTRY_CREDENTIALS = 'dockerhub-credentials'
    }
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Build and Push Go Docker Image') {
            steps {
                script {
                    // Change directory to the 'go' folder
                    dir('go') {
                        // Build the Docker image
                        sh 'docker build -t myapp-go .'
                        
                        // Push the Docker image to Docker Hub
                        withDockerRegistry([credentialsId: DOCKER_REGISTRY_CREDENTIALS, url: 'https://index.docker.io/v1/']) {
                            sh 'docker push myapp-go'
                        }
                    }
                }
            }
        }
    }
}
