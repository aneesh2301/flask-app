pipeline {
    agent any

    environment {
        DOCKER_HUB_CREDENTIALS = credentials('5bb70d65-0f3c-4b23-8b5c-ed39e2fb29e8') // Jenkins credential ID
        DOCKER_IMAGE_NAME = "aneeshyadav2302/flask-app"
        PATH = '/Users/aneeshyadav/.rd/bin/docker'
    }

    stages {
        stage('Checkout') {
            steps {
                // Clone the repository
               git branch: 'main', url: 'https://github.com/aneesh2301/flask-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Build Docker image
                    sh "docker build -t ${DOCKER_IMAGE_NAME} ."
                }
            }
        }

        stage('Login to Docker Hub') {
            steps {
                script {
                    // Login to Docker Hub
                    sh "echo ${DOCKER_HUB_CREDENTIALS_PSW} | docker login -u ${DOCKER_HUB_CREDENTIALS_USR} --password-stdin"
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    // Push Docker image to Docker Hub
                    sh "docker push ${DOCKER_IMAGE_NAME}"
                }
            }
        }

        stage('Clean Up') {
            steps {
                script {
                    // Remove Docker image to clean up space
                    sh "docker rmi ${DOCKER_IMAGE_NAME}"
                }
            }
        }
    }

    post {
        always {
            // Cleanup: Logout from Docker Hub
            sh "docker logout"
        }
    }
}
