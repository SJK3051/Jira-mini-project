pipeline {
    agent any

    environment {
        DOCKER_COMPOSE_FILE = "docker-compose.yml"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/SJK3051/Jira-mini-project'
            }
        }

        stage('Build Backend Image') {
            steps {
                script {
                    sh 'docker build -t backend-app ./backend'
                }
            }
        }

        stage('Build Frontend Image') {
            steps {
                script {
                    sh 'docker build -t frontend-app ./frontend'
                }
            }
        }

        stage('Start with Docker Compose') {
            steps {
                script {
                    sh "docker-compose -f ${DOCKER_COMPOSE_FILE} up -d --build"
                }
            }
        }
    }

    post {
        success {
            echo "✅ Application deployed successfully using Docker Compose!"
        }
        failure {
            echo "❌ Build or deployment failed. Please check the logs."
        }
    }
}
