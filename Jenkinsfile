pipeline {
    agent any
    
    environment {
        // Define Docker Hub credentials.
        DOCKER_HUB_CREDENTIALS = credentials('docker-hub-credentials')
        // Define Docker image name
        DOCKER_IMAGE_NAME = 'binod132/helloworld'
    }
    
    stages {
        stage('Checkout') {
            steps {
                // Check out the code from your version control system (e.g., Git)
                checkout scm
            }
        }
        
        stage('Build Docker Image') {
            steps {
                // Build Docker image
                script {
                    docker.build("${DOCKER_IMAGE_NAME}:${BUILD_NUMBER}")
                }
            }
        }
        
        stage('Push to Docker Hub') {
            steps {
                // Log in to Docker Hub
                script {
                    docker.withRegistry('https://index.docker.io/v1/', DOCKER_HUB_CREDENTIALS) {
                        // Push Docker image to Docker Hub
                        docker.image("${DOCKER_IMAGE_NAME}:${BUILD_NUMBER}").push()
                    }
                }
            }
        }
    }
}
