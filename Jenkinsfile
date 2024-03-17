pipeline {
    agent any
    
    environment {
        DOCKER_REGISTRY_URL = 'https://index.docker.io/v1/'
        DOCKER_REGISTRY_CREDENTIALS = 'dockerhub-credentials'
        DOCKER_IMAGE_TAG = 'latest' // Define the tag for the Docker image
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
                        // Build the Docker image and tag it with the specified tag
                        sh "docker build -t myapp-go:${DOCKER_IMAGE_TAG} ."
                    }
                }
            }
        }
        
        stage('Push Go Docker Image') {
            steps {
                script {
                    // Push the Docker image to Docker Hub with the specified tag
                    withDockerRegistry([credentialsId: DOCKER_REGISTRY_CREDENTIALS, url: DOCKER_REGISTRY_URL]) {
                        sh "docker push myapp-go:${DOCKER_IMAGE_TAG}"
                    }
                }
            }
        }
    }
}
