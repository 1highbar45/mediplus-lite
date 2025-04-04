pipeline {
    agent any
    stages{
        stage('Clone') {
            steps {
                echo 'clone start'
                git branch: 'main', credentialsId: '1highbar45', url: 'https://github.com/1highbar45/mediplus-lite.git'
                echo 'clone finish'
            }
        }
        stage('Build'){
            steps{
                echo 'build code'
            }
        }
        stage('Test'){
            steps{
                echo 'run unittest'
            }
        }
        stage('Docker'){
            steps{
                echo 'build image'
                echo 'tag'
                echo 'push docker hub'
            }
        }
    }
}