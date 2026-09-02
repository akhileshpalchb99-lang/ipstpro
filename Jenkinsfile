pipeline {
    agent any

    stages {
        stage('Checkout GIT code') {
            steps {
                git branch: 'main',
                url: 'https://github.com/pramilagit/ipstpro.git'
            }
        }
        stage('Docker Build Image'){
            steps {
                sh '''
                docker build -t ipstpro:v1 .
                '''
            }
        }
        stage('Docker image check'){
            steps{
                sh '''
                docker images | grep ipstpro
                '''
            }
                
        }
        stage('Push image on NEXUS'){
            steps{
                script{
                    withCredentials([usernamePassword(
                    credentialsId: 'nexus-docker-cred',
                    usernameVariable: 'NEXUS_USER',
                    passwordVariable: 'NEXUS_PASS'
            )]) {

                sh '''
                docker login -u $NEXUS_USER -p $NEXUS_PASS 172.16.36.131:9070

                docker tag ipstpro:v1 172.16.36.131:9070/ipstpro/ipstpro:v1

                docker push 172.16.36.131:9070/ipstpro/ipstpro:v1
                '''

               }
            }
        }
     }
     
     stage('Deploy') {
    steps {
        script {
            sshPublisher(
                publishers: [
                    sshPublisherDesc(
                        configName: 'dockerserv',
                        transfers: [
                            sshTransfer(
                                execCommand: '''
        cd /opt/ipstpro

        docker pull 172.16.36.131:9070/ipstpro/ipstpro:v1

        docker compose down

        docker compose up -d
'''
                            )
                        ]
                    )
                ]
            )
        }
    }
}         
     
  }
}