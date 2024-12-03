pipeline {
    agent any

    environment {
        JAVA_HOME = '/usr/lib/jvm/java-11-openjdk-amd64'
        MAVEN_HOME = '/usr/share/maven'
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/ridwan094/springboot-app.git'
            }
        }

        stage('Build') {
            steps {
                script {
                    sh '${MAVEN_HOME}/bin/mvn clean install -DskipTests'
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    sh '${MAVEN_HOME}/bin/mvn test'
                }
            }
        }

        stage('Package') {
            steps {
                script {
                    sh '${MAVEN_HOME}/bin/mvn package'
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    sh 'docker build -t springboot-app .'
                    sh 'docker run -d -p 8080:8080 springboot-app'
                }
            }
        }
    }

    post {
        success {
            echo 'Build and Deploy successful!'
        }
        failure {
            echo 'Build or Deploy failed. Please check the logs!'
        }
    }
}
