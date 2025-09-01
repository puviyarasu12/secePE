pipeline {
    agent any

    environment {
        IMAGE_NAME = "simple-webapp"
        CONTAINER_NAME = "webapp-container"
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/puviyarasu12/secePE.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t ${IMAGE_NAME}:latest ."
                }
            }
        }

        stage('Deploy Container') {
            steps {
                script {
                    // Stop and remove old container if running
                    sh """
                    docker rm -f ${CONTAINER_NAME} || true
                    docker run -d --name ${CONTAINER_NAME} -p 80:80 ${IMAGE_NAME}:latest
                    """
                }
            }
        }
    }
}
