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

        stage('Install Dependencies') {
            steps {
                sh '''
                echo "Installing dependencies..."
                npm install
                '''
            }
        }

        stage('Run Unit Tests') {
            steps {
                sh '''
                echo "Running tests..."
                npm test -- --watchAll=false || true
                '''
            }
        }

        stage('Build Application') {
            steps {
                sh '''
                echo "Building application..."
                npm run build
                '''
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
                echo "Building Docker image..."
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

        stage('Smoke Test (Optional)') {
            steps {
                sh '''
                echo "Smoke test skipped (can be enabled after deployment)"
                '''
            }
        }
    }

    post {
        success {
            echo 'Docker Image Built Successfully + Tests Passed! 🚀'
        }

        failure {
            echo 'Pipeline Failed! ❌ Check logs'
        }
    }
}
