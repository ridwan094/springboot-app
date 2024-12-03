pipeline {
    agent any
    environment {
        DOCKER_HOST = 'tcp://localhost:2375'  // Mengatur DOCKER_HOST jika perlu (ini diperlukan untuk DinD)
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/ridwan094/springboot-app.git'
            }
        }
        stage('Build with Maven') {
            agent {
                docker {
                    image 'maven:3.8.6-openjdk-11'  // Menggunakan image Maven dengan JDK 11
                    args '-v /var/jenkins_home:/var/jenkins_home'  // Agar volume Jenkins bisa digunakan di container
                }
            }
            steps {
                sh 'mvn clean install'
            }
        }
        stage('Build Docker Image') {
            agent {
                docker {
                    image 'docker:20.10'  // Menggunakan Docker image yang menyediakan Docker
                    args '-v /var/jenkins_home:/var/jenkins_home -v /var/run/docker.sock:/var/run/docker.sock' // Mount Docker socket
                }
            }
            steps {
                sh 'docker build -t springboot-app .'
            }
        }
        stage('Push Docker Image') {
            steps {
                sh 'docker push springboot-app'
            }
        }
        stage('Run Application') {
            steps {
                sh 'docker run -d -p 8080:8080 springboot-app'
            }
        }
    }
}
