pipeline {
    agent any 
    parameters {
        string(name: 'DOCKER_IMAGE_NAME', defaultValue: 'choco-image', description: 'Name of the Docker image')
    }
         
    
    stages {
            stage('Checkout Application Code') {
                steps {
                    script {checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'PAT_Docker', url: 'https://github.com/zuryah/choco.git']])
                }
                }
            }
         }
    }
