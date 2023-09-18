pipeline {
    agent any
    environment {
        DOCKER_IMAGE_NAME = 'my-laravel-app:latest'
        DOCKERFILE_PATH = 'Dockerfile'
        DOCKER_COMPOSE_FILE = 'docker-compose.yml'
    }
    tools {
    // Use the name you specified in the Git installation configuration
    git 'Git'
}
    node {
    stage('Check Docker Version') {
        try {
            def dockerVersion = sh(script: 'docker --version', returnStatus: true)
            if (dockerVersion == 0) {
                echo "Docker Version: "
                sh 'docker --version'
            } else {
                error "Docker is not installed or not accessible."
            }
        } catch (Exception e) {
            error "Error checking Docker version: ${e.message}"
        }
    }

    // Your existing stages here

    stage('Build and Test') {
        try {
            // Add your build and test steps here
        } catch (Exception e) {
            error "Error during build and test: ${e.message}"
        }
    }

    // Add more stages as needed
}

    stages {
    

        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image using the provided Dockerfile
                    docker.build("${DOCKER_IMAGE_NAME}", "-f ${DOCKERFILE_PATH} .")
                }
            }
        }

        stage('Push Docker Image to Registry') {
            steps {
                script {
                    // You can authenticate with your Docker registry here if needed

                    // Push the Docker image to the registry
                    docker.withRegistry('', '') {
                        docker.image("${DOCKER_IMAGE_NAME}").push()
                    }
                }
            }
        }

        stage('Deploy with Docker Compose') {
            steps {
                script {
                    // Deploy using docker-compose
                    sh "docker-compose -f ${DOCKER_COMPOSE_FILE} up -d"
                }
            }
        }
}
