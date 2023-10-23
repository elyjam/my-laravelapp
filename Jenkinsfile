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
       stage('Run Tests') {
            steps {
                script {
                    // Run Laravel tests in the Docker container
                    docker.image(env.DOCKER_IMAGE).inside('-v $(pwd):/var/www/html') {
                        sh 'php artisan test'  // Replace with your Laravel test command
                    }
                }
            }

        }
    }
}
