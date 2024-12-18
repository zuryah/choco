 pipeline {
    agent any 

    parameters {
        string(name: 'Docker_Image_Name', defaultValue: 'choco', description: 'Name of the Docker image')
    }
    environment {
        AWS_ACCESS_KEY_ID      = credentials('aws-access-key-id')
        AWS_SECRET_ACCESS_KEY  = credentials('aws-secret-access-key')
        AWS_DEFAULT_REGION     = 'us-west-2c'  // Set AWS region
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
                    withCredentials([ usernamePassword(credentialsId:'PAT_Docker', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PAT')]) {
                        sh "echo '${DOCKER_PAT}' | docker login -u ${DOCKER_USERNAME} --password-stdin"
                        
                        // Tag and push the built Docker image to Docker Hub
                        sh "docker tag ${params.Docker_Image_Name}:latest ${DOCKER_USERNAME}/${params.Docker_Image_Name}:latest"
                        sh "docker push ${DOCKER_USERNAME}/${params.Docker_Image_Name}:latest"
                    }
                }
                
            }
        }
    }
}   
