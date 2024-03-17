pipeline {
    agent any
    
    environment {
        DOCKER_REGISTRY_URL = 'https://index.docker.io/v1/'
        DOCKER_REGISTRY_CREDENTIALS = 'dockerhub-credentials'
        DOCKER_IMAGE_TAG = 'latest' // Define the tag for the Docker image
        DOCKER_USERNAME = 'tannuahuja14' // Your Docker Hub username
        DOCKER_IMAGE_NAME = 'myapp-go' // Your Docker image name
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
                        sh "docker build -t ${DOCKER_IMAGE_NAME}:${DOCKER_IMAGE_TAG} ."
                    }
                }
            }
        }
        
        stage('Push Go Docker Image') {
            steps {
                script {
                    // Push the Docker image to Docker Hub with the specified tag and your username
                    withDockerRegistry([credentialsId: DOCKER_REGISTRY_CREDENTIALS, url: DOCKER_REGISTRY_URL]) {
                        sh "docker tag ${DOCKER_IMAGE_NAME}:${DOCKER_IMAGE_TAG} ${DOCKER_USERNAME}/${DOCKER_IMAGE_NAME}:${DOCKER_IMAGE_TAG}"
                        sh "docker push ${DOCKER_USERNAME}/${DOCKER_IMAGE_NAME}:${DOCKER_IMAGE_TAG}"
                    }
                }
            }
        }
        
        stage('Deploy to Kubernetes') {
            steps {
                script {
                    // Apply Kubernetes deployment and service configurations
                    kubernetesDeploy(configs: 'deploymentservice.yaml', kubeconfigId: 'kubernetes')
                }
            }
        }
    }
}
