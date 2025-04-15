pipeline {
    agent any
    stages{
        stage('Clone') {
            steps {
                git branch: 'main', credentialsId: '1highbar45', url: 'https://github.com/1highbar45/mediplus-lite.git'
            }
        }
        stage('Docker'){
            steps{
                // This step should not normally be used in your script. Consult the inline help for details.
                withDockerRegistry(credentialsId: 'cred-docker-hub', url: '') {
                    // some block
                    sh label: '', script: 'docker build -t sigmaduck125/my-website .'
                    sh label: '', script: 'docker push sigmaduck125/my-website'
                }
            }
        }
    }
}