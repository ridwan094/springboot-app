pipeline {
    agent {
        docker {
            image 'maven:3.8.6-openjdk-11'  // Menggunakan Docker image dengan Maven dan OpenJDK 11
            args '-v /var/jenkins_home:/var/jenkins_home'  // Agar volume Jenkins bisa digunakan di container
        }
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/ridwan094/springboot-app.git'
            }
        }
        stage('Build with Maven') {
            steps {
                sh 'mvn clean install'
            }
        }
        stage('Build Docker Image') {
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
