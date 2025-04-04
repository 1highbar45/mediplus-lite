pipeline {
    agent any
    stages{
        stage('Clone') {
            steps {
                git branch: 'main', 
                credentialsId: '1highbar45', 
                url: 'https://github.com/1highbar45/mediplus-lite.git'
            }
        }
    }
}