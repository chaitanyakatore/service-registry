pipeline {
    agent any

    tools {
        maven 'my-maven'
        jdk 'my-jdk'
    }

    stages {
        stage('Clone') {
            steps {
                git url: 'https://github.com/chaitanyakatore/service-registry.git', branch: 'main'
            }
        }
        stage('Build') {
            steps {
                bat "mvn clean install -DskipTests"
            }
        }
        stage('Test') {
            steps {
                bat "mvn test"
            }
        }
        stage('Deploy') {
            steps {
                bat "docker rm -f service-registry-container"
                bat "docker rmi -f service-registry-image"
                bat "docker build -t service-registry-image ."
                bat "docker run -p 8761:8761 -d --name service-registry-container service-registry-image"
            }
        }
    }
}
