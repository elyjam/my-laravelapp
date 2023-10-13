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
        stage('Install Docker') {
           steps {
             script {
             def dockerTool = tool name: 'Docker', type: 'Tool Type Name' // Replace 'Tool Type Name'
             env.PATH = "${dockerTool}:${env.PATH}"
               }
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
        stage('Install Composer Dependencies') {
            steps {
                script {
                    // Install Composer dependencies in the Docker container
                    docker.image(env.DOCKER_IMAGE).inside('-v $(pwd):/var/www/html') {
                        sh 'composer install'
                    }
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
