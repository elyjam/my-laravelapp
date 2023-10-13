pipeline {
    agent any

    environment {
        DOCKER_HOME = tool name: 'Docker', type: 'Tool Type Name' // Replace 'Tool Type Name'
    }

    stages {
        stage('Checkout SCM') {
            steps {
                // Add the checkout SCM steps here
            }
        }

    stage('Build Docker Image') {
      when {
        expression {
            currentBuild.resultIsBetterOrEqualTo('SUCCESS')
        }
          }
          steps {
            sh "docker build -t my-laravelapp ."
          }
       }
  stage('Install Composer Dependencies') {
            steps {
                // Add steps to install Composer dependencies
                sh 'composer install'
            }
        }

 stage('Run Tests') {
            steps {
                // Add steps to run tests
                sh 'phpunit'
            }
        }
    }
}
