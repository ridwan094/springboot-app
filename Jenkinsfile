pipeline {
    agent any
    environment {
        DOCKER_IMAGE = 'springboot-hello-world'
        DOCKER_TAG = 'latest'
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/ridwan094/springboot-app.git'
            }
        }
        stage('Check Maven Version') {
            steps {
                script {
                    // Mengecek apakah Maven terinstal dan versi yang digunakan
                    sh 'mvn -v'
                    sh 'java -version'
                }
            }
        }
        stage('Build JAR') {
            steps {
                script {
                    // Menjalankan build menggunakan Maven
                    sh 'mvn clean package'
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
                    // Pastikan Docker login sudah dilakukan sebelumnya
                    sh 'docker push ${DOCKER_IMAGE}:${DOCKER_TAG}'
                }
            }
        }
    }
    post {
        always {
            cleanWs()  // Membersihkan workspace Jenkins setelah proses selesai
        }
    }
}

