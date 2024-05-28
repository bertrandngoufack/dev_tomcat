pipeline {
    agent any
    environment {
        GIT_REPO_URL = 'https://github.com/bertrandngoufack/dev_tomcat.git'
        GIT_BRANCH = 'main' // Assurez-vous que c'est la branche correcte
    }
    stages {
        stage('Checkout') {
            steps {
                script {
                    try {
                        git branch: "${GIT_BRANCH}", url: "${GIT_REPO_URL}"
                    } catch (Exception e) {
                        error "Failed to clone the repository. Please check the URL and branch name. Error: ${e.message}"
                    }
                }
            }
        }
        stage('Build and Deploy with Docker Compose') {
            steps {
                script {
                    sh 'docker-compose up -d --build'
                }
            }
        }
    }
    post {
        always {
            script {
                sh 'docker-compose down'
            }
        }
    }
}
