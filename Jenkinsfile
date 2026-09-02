pipeline {
    agent any

    stages {

        stage('Checkout GIT Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/akhileshpalchb99-lang/ipstpro.git'
            }
        }

        stage('Verify Code') {
            steps {
                sh '''
                    echo "Checking IPSTPRO Project Files..."
                    ls -la
                '''
            }
        }

        stage('Docker Build Image') {
            steps {
                sh '''
                    echo "Building IPSTPRO Docker Image..."
                    docker build -t ipstpro:v1 .
                '''
            }
        }

        stage('Docker Image Check') {
            steps {
                sh '''
                    echo "Checking IPSTPRO Docker Image..."
                    docker images | grep ipstpro
                '''
            }
        }
    }

    post {
        success {
            echo 'IPSTPRO CI Docker Build SUCCESS'
        }

        failure {
            echo 'IPSTPRO CI Docker Build FAILED'
        }
    }
}