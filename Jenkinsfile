pipeline {
    agent any
    
    environment {
        DOCKER_REGISTRY_CREDENTIALS = 'dockerhub-credentials'
        // KUBE_CONFIG = credentials('kubernetes-config')
    }
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Lint and Test Go') {
            steps {
                sh 'golangci-lint run ./go'
                sh 'go test ./go'
            }
        }
        
        stage('Build and Push Go Docker Image') {
            steps {
                script {
                    docker.build('myapp-go')
                    docker.withRegistry('', DOCKER_REGISTRY_CREDENTIALS) {
                        docker.image('myapp-go').push('latest')
                    }
                }
            }
        }
    }
}
