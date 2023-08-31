pipeline {
    agent any

    environment {
        DOCKER_IMAGE_NAME = 'my-laravel-app:latest'
        DOCKERFILE_PATH = 'Dockerfile'
        DOCKER_COMPOSE_FILE = 'docker-compose.yml'
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
}
