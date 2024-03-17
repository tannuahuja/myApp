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
        
        // stage('Lint and Test Go') {
        //     steps {
        //         sh 'golangci-lint run ./go'
        //         sh 'go test ./go'
        //     }
        // }
        
        stage('Build Go Docker Image') {
            steps {
                script {
                    docker.build('myapp-go')
                }
            }
        }
    }
}
