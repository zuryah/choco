pipeline {
    agent any 
    parameters {
        string(name: 'Docker_Image_Name', defaultValue: 'choco-image', description: 'Name of the Docker image')
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
    stage('Build Docker Image') {
    steps {
        script {
    // Build the Docker image
            sh "docker build -t ${params.Docker_Image_Name}:latest . -f Dockerfile"
            }
        }
    }
