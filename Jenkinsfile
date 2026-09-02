pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/akhileshpalchb99-lang/ipstpro.git'
            }
        }

        stage('Verify Code') {
            steps {
                sh 'ls -la'
                sh 'echo "IPSTPRO source code checkout successful"'
            }
        }
    }

    post {
        success {
            echo 'IPSTPRO CI Pipeline SUCCESS'
        }

        failure {
            echo 'IPSTPRO CI Pipeline FAILED'
        }
    }
}