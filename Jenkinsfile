pipeline {
    agent any
    environment {
        DOCKER_IMAGE = 'my-laravel-app'  // Docker image name
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm  // Check out the source code from your version control system
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image
                    docker.build env.DOCKER_IMAGE, "-f Dockerfile ."
                }
            }
        }

        }
    }
}
