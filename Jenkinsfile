pipeline {
    agent any 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('docker-hub-passwd')
    }
    stages { 
        
         stage('Code checkout') {
            steps {  
                git 'https://github.com/rutwikdadgal/TS-demo.git'
            }
        }
        stage('Build docker image') {
            steps {  
                sh 'docker build -t rutwikd/nginx:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push rutwikd/nginx:$BUILD_NUMBER'
            }
        }
    }

}
