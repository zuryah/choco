pipeline {
    agent any 

    parameters {
        string(name: 'Docker_Image_Name', defaultValue: 'choco', description: 'Name of the Docker image')
    }

    
    stages {
        stage('Checkout Application Code') {
            steps {
                script {checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'PAT_Docker', url: 'https://github.com/zuryah/choco.git']])
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
        stage ('Push image to Docker Hub') {
            steps {
                script {
                    withCredentials([ usernamePassword(credentialsId:'PAT_Docker', variable: 'DOCKER_PAT')]) {
                        sh "echo '$(DOCKER_PAT)' | docker login -u surya215 --password-stdin"

                        sh "docker image tag ${params.Docker_Image_Name}:latest surya215/${params.Docker_Image_Name}:latest"
                        sh "docker push surya215/${params.Docker_Image_Name}:latest"
                       
                    }
                
                }
            }
        }
    }   
}
