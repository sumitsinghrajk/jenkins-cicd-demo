pipeline {
    agent any

    environment {
        IMAGE_NAME = 'harshmit3190/jenkins-cicd-demo'
    }

    stages {

        stage('Build') {
            steps {
                echo 'Building application'
                sh 'ls -la'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests'
                sh 'test -f Dockerfile'
                sh 'test -f index.html'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t ${IMAGE_NAME}:${BUILD_NUMBER} .'
                sh 'docker tag ${IMAGE_NAME}:${BUILD_NUMBER} ${IMAGE_NAME}:latest'
            }
        }

        stage('Docker Push') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'DOCKER_USERNAME',
                    passwordVariable: 'DOCKER_PASSWORD'
                )]) {
                    sh '''
                        echo "$DOCKER_PASSWORD" | docker login -u "$DOCKER_USERNAME" --password-stdin
                        docker push ${IMAGE_NAME}:${BUILD_NUMBER}
                        docker push ${IMAGE_NAME}:latest
                        docker logout
                    '''
                }
            }
        }
    }
}
