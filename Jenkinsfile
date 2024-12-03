pipeline {
    agent any

    triggers {
        githubPush()
    }

    environment {
        DOCKER_IMAGE = 'springboot-hello-world'
        DOCKER_TAG = 'latest'
        JAVA_HOME = '/usr/lib/jvm/java-11-openjdk-amd64'  // Menetapkan JAVA_HOME
        PATH = "$JAVA_HOME/bin:$PATH"  // Menambahkan JAVA_HOME/bin ke PATH
    }
    stages {
        stage('Checkout') {
            steps {
                // Checkout source code dari repository Git
                git 'https://github.com/ridwan094/springboot-app.git'
            }
        }
        stage('Build with Maven') {
            steps {
                script {
                    // Menjalankan build menggunakan Maven (menggunakan perintah shell)
                    sh 'mvn clean package -DskipTests'  // Membuild aplikasi tanpa menjalankan unit tests
                }
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    // Membuat Docker Image
                    sh 'docker build -t ${DOCKER_IMAGE}:${DOCKER_TAG} .'
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    // Push image ke Docker Hub
                    sh 'docker push ${DOCKER_IMAGE}:${DOCKER_TAG}'
                }
            }
        }
        stage('Run Application') {
            steps {
                script {
                    // Menjalankan aplikasi menggunakan Docker
                    sh 'docker run -d -p 8080:8080 ${DOCKER_IMAGE}:${DOCKER_TAG}'
                }
            }
        }
    }
    post {
        always {
            // Membersihkan workspace setelah build selesai
            cleanWs()
        }
    }
}
