pipeline {
    agent any
    environment {
        DOCKER_IMAGE = 'springboot-hello-world'
        DOCKER_TAG = 'latest'
    }
    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/ridwan094/springboot-app.git'
            }
        }
        stage('Build JAR') {
            steps {
                script {
                    sh './mvnw clean package'
                }
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
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

