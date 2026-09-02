pipeline {
    agent any

    stages {

        stage('Checkout GIT Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/pramilagit/ipstpro.git'
            }
        }

        stage('Verify Code') {
            steps {
                sh 'ls -la'
            }
        }

        stage('Docker Build Image') {
            steps {
                sh 'docker build -t ipstpro:v1 .'
            }
        }

        stage('Docker Image Check') {
            steps {
                sh 'docker images | grep ipstpro'
            }
        }
    }

    post {
        success {
            echo 'IPSTPRO Docker Build SUCCESS'
        }

        failure {
            echo 'IPSTPRO Docker Build FAILED'
        }
    }
}