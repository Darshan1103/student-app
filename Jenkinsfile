
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build and Test') {
            steps {
                bat '''
                set "JAVA_HOME=C:\\Program Files\\Eclipse Adoptium\\jdk-21.0.12.101-hotspot"
                set "MAVEN_HOME=C:\\Program Files\\apache-maven-3.10.0"
                set "PATH=%JAVA_HOME%\\bin;%MAVEN_HOME%\\bin;%PATH%"
                call mvn clean package
                '''
            }
        }

        stage('Build Docker Image') {
            steps {
                bat '''
                set "PATH=C:\\Users\\Darshan\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin;%PATH%"
                docker build -t student-app:1.0.0 .
                '''
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                bat '''
                kubectl apply -f k8s/deployment.yaml
                kubectl apply -f k8s/service.yaml
                kubectl rollout status deployment/student-app
                '''
            }
        }
    }
}
