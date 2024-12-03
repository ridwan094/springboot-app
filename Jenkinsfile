pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/ridwan094/springboot-app.git'
            }
        }
        stage('Build with Maven') {
            agent {
                docker {
                    image 'maven:3.8.6-openjdk-11'  // Menggunakan image Docker dengan Maven dan OpenJDK 11
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
                    image 'docker:19.03.12-dind'  // Docker-in-Docker image
                    args '--privileged -v /var/jenkins_home:/var/jenkins_home'  // Menambahkan --privileged untuk DinD dan volume Jenkins
                }
            }
            steps {
                sh 'docker build -t springboot-app .'
            }
        }
        stage('Push Docker Image') {
            agent {
                docker {
                    image 'docker:19.03.12-dind'  // Docker-in-Docker image
                    args '--privileged -v /var/jenkins_home:/var/jenkins_home'  // Menambahkan --privileged untuk DinD dan volume Jenkins
                }
            }
            steps {
                sh 'docker push springboot-app'
            }
        }
        stage('Run Application') {
            agent {
                docker {
                    image 'docker:19.03.12-dind'  // Docker-in-Docker image
                    args '--privileged -v /var/jenkins_home:/var/jenkins_home'  // Menambahkan --privileged untuk DinD dan volume Jenkins
                }
            }
            steps {
                sh 'docker run -d -p 8080:8080 springboot-app'
            }
        }
    }
}
