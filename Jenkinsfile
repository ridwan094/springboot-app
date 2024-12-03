pipeline {
    agent any

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
