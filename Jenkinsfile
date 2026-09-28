pipeline {
    agent any

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
                sh 'docker build -t jenkins-cicd-demo:${BUILD_NUMBER} .'
            }
        }

        stage('Docker Test') {
            steps {
                sh 'docker images | grep jenkins-cicd-demo'
            }
        }
    }
}
