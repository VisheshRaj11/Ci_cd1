pipeline {

    agent any

    tools {
        maven 'Maven3'
    }

    environment {
        IMAGE_NAME = "maven-app"
        IMAGE_TAG = "latest"
        CONTAINER_NAME = "maven-container"
    }

    stages {

        stage('Checkout Source Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/VisheshRaj11/Ci_cd1.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('Build Application') {
            steps {
                sh 'mvn package'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t ${IMAGE_NAME}:${IMAGE_TAG} .'
            }
        }

        stage('Deploy Container') {
            steps {
                sh '''
                docker stop ${CONTAINER_NAME} || true
                docker rm ${CONTAINER_NAME} || true
                docker run -d --name ${CONTAINER_NAME} ${IMAGE_NAME}:${IMAGE_TAG}
                '''
            }
        }
    }

    post {
        success {
            echo "Application deployed successfully!"
        }

        failure {
            echo "Deployment failed!"
        }
    }
}
