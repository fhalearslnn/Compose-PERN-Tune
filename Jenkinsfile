pipeline {
    agent any
    stages {
        stage('Deploy the App') {
            steps {
                echo 'Deploy the App'
                sh 'ls -l'
                sh 'docker --version'
                sh 'docker-compose build' 
            }
        }
        stage('Destroy the infrastructure') {
            steps {
                timeout(time:5, unit:'DAYS') {
                    input message:'Approve terminate'
                }
                sh 'docker-compose down' 
            }
        }
    }

    post {
        success {
        script {
        slackSend channel: '#class-chat', color: '#439FE0', message: ':unicorn_face:', teamDomain: 'devops15tr', tokenCredentialId: 'jenkins-slack'
            }
    }
    }  

}
