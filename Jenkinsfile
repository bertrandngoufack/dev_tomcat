pipeline {
    agent any
    environment {
        GIT_REPO_URL = 'https://github.com/bertrandngoufack/dev_tomcat.git'
    }
    stages {
        stage('Checkout') {
            steps {
                git url: "${GIT_REPO_URL}"
            }
        }
        stage('Build and Deploy with Docker Compose') {
            steps {
                script {
                    // Build the Docker image and bring up the container using Docker Compose
                    sh 'docker-compose up -d --build'
                }
            }
        }
    }
    post {
        always {
            script {
                // Bring down the Docker Compose services after the build
                sh 'docker-compose down'
            }
        }
    }
}
