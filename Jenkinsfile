pipeline {
    agent any 
         stages {
            stage('Checkout Application Code') {
                steps {
                    script {checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'PAT_Docker', url: 'https://github.com/zuryah/choco.git']])
                }
                }
            }
         }
    }