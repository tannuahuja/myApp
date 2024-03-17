pipeline {
    agent any
    
    environment {
        DOCKER_REGISTRY_CREDENTIALS = 'dockerhub-credentials'
        DOCKER_IMAGE_TAG = 'latest' 
    }
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Build Go Docker Image') {
            steps {
                script {
                    // Change directory to the 'go' folder
                    dir('go') {
                        // Build the Docker image and tag it
                        sh "docker build -t myapp-go:${DOCKER_IMAGE_TAG} ."
                    }
                }
            }
        }
        
        stage('Push Go Docker Image') {
            steps {
                script {
                    // Push the Docker image to Docker Hub with the specified tag
                    withDockerRegistry([credentialsId: 'dockerhub-credentials', url: 'https://registry.hub.docker.com']) {
                        sh "docker push myapp-go:${DOCKER_IMAGE_TAG}"
                    }
                }
            }
        }
    }
}
