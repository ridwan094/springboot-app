pipeline {
    agent any
    environment {
        DOCKER_IMAGE = 'springboot-hello-world'
        DOCKER_TAG = 'latest'
        DOCKER_CREDENTIALS = 'rainover922'
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/ridwan094/springboot-app.git'
            }
        }
        stage('Build JAR') {
            steps {
                script {
                    echo 'Building JAR...'
                    sh 'mvn clean package'
                }
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    echo 'Building Docker Image...'
                    sh 'docker build -t ${DOCKER_IMAGE}:${DOCKER_TAG} .'
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    sh 'docker push ${DOCKER_IMAGE}:${DOCKER_TAG}'
                }
            }
        }
    }
    post {
        always {
            cleanWs()
        }
    }
}


