pipeline {
    agent any

    environment {
        IMAGE_NAME = "food-delivery-app"
        IMAGE_TAG = "latest"
    }

    stages {

        stage('Clone Repository') {
            steps {
                git branch: 'master',
                url: 'https://github.com/Hema3507/DevOps-Project-Zomato-Kastro.git'
            }
        }

        stage('Verify Files') {
            steps {
                sh 'ls -la'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                docker build -t $IMAGE_NAME:$IMAGE_TAG .
                '''
            }
        }

        stage('Verify Docker Image') {
            steps {
                sh '''
                docker images
                '''
            }
        }
    }

    post {
        success {
            echo 'Docker Image Built Successfully!'
        }

        failure {
            echo 'Pipeline Failed!'
        }
    }
}
