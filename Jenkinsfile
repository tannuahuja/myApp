pipeline {
    agent any
    
    environment {
        DOCKER_REGISTRY_CREDENTIALS = 'docker-hub-credentials'
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
                        // Build the Docker image
                        sh 'docker build -t myapp-go .'
                    }
                }
            }
        }
        
        stage('Push Go Docker Image') {
            steps {
                script {
                    // Push the Docker image to Docker Hub
                    withDockerRegistry([credentialsId: 'docker-hub-credentials', url: '']) {
                        sh 'docker push myapp-go'
                    }
                }
            }
        }
    }
}

