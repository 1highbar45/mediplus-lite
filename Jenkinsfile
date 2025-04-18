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
        stage("Deploy"){
            steps{
                sshagent(['ubuntu-server']) {
                    // some block
                    sh """
                        ssh -o StrictHostKeyChecking=no ubuntu@54.151.249.93 << 'EOF'
                        sudo docker service update --image sigmaduck125/my-website:latest webserver
                    """                
                }            
            }
        }
    }
    post {
        always {
            mail bcc: '', body: 'jenkins server', cc: '', from: '', replyTo: '', subject: 'jenkins server', to: 'vuanh1228@gmail.com'
        } 
    }
}