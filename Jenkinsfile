pipeline {
    agent any

    environment {
        IMAGE_NAME = "bhargavdas2005/myapp"
        TAG = "latest"
    }

    stages {

        stage('Clone Source') {
            steps {
                git branch: 'main',
                url: 'https://github.com/Bhargav-Das/DOCKER-JENKINS-PROJECT'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME:$TAG .'
            }
        }

        stage('Docker Login') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'USER',
                    passwordVariable: 'PASS'
                )]) {
                    sh 'echo $PASS | docker login -u $USER --password-stdin'
                }
            }
        }

        stage('Push Image') {
            steps {
                sh 'docker push $IMAGE_NAME:$TAG'
            }
        }
    }

    post {
        success {
            echo 'Build and Push Successful!'
        }

        failure {
            echo 'Pipeline Failed!'
        }
    }
}