pipeline {
    agent any

    environment {
        IMAGE_NAME = "gammala/my-app"
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-credentials')
    }

    stages {
        stage('Clone repository') {
            steps {
                git 'https://github.com/gammala14/my-app.git'
            }
        }

        stage('Build Docker image') {
            steps {
                script {
                    sh "docker build -t ${IMAGE_NAME} ."
                }
            }
        }

        stage('Login to DockerHub') {
            steps {
                script {
                    sh "echo ${DOCKERHUB_CREDENTIALS_PSW} | docker login -u ${DOCKERHUB_CREDENTIALS_USR} --password-stdin"
                }
            }
        }

        stage('Push to DockerHub') {
            steps {
                script {
                    sh "docker push ${IMAGE_NAME}"
                }
            }
        }
    }
}

