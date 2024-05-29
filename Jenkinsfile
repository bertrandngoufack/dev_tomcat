pipeline {
    agent any
    environment {
        GIT_REPO_URL = 'https://github.com/bertrandngoufack/dev_tomcat.git'
        GIT_BRANCH = 'main'
    }
    stages {
        stage('Stop Existing Container') {
            steps {
                script {
                    try {
                        // Arrêter et supprimer le conteneur Tomcat existant s'il est en cours d'exécution
                        sh 'docker ps -q --filter "ancestor=tomcat:latest" | xargs -r docker stop'
                        sh 'docker ps -a -q --filter "ancestor=tomcat:latest" | xargs -r docker rm'
                    } catch (Exception e) {
                        echo "No running container to stop. Proceeding to the next step."
                    }
                }
            }
        }
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
}
