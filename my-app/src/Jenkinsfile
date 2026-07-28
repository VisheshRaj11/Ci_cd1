pipeline {
    agent any

    parameters {
        string(name: 'GIT_BRANCH', defaultValue: 'main', description: 'Git Branch Name')
        string(name: 'APP_VERSION', defaultValue: '1.0', description: 'Application Version')
    }

    environment {
        BUILD_DIR = "target"
        ARTIFACT_NAME = "demo-${params.APP_VERSION}.jar"
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: "${params.GIT_BRANCH}",
                    url: 'https://github.com/VisheshRaj11/Ci_cd1.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean compile'
            }
        }

        stage('Unit Testing') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Code Quality Check') {
            steps {
                sh 'mvn verify'
            }
        }

        stage('Package') {
            steps {
                sh 'mvn package'
            }
        }

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar',
                                 fingerprint: true
            }
        }
    }

    post {
        success {
            echo "Build Successful"
        }

        failure {
            echo "Build Failed"
        }
    }
}
