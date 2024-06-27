pipeline {
    agent {
        label 'Jenkins-slave'
    } 
    
    environment {
        ACR_SERVER = 'docker123456789.azurecr.io'
        ACR_USERNAME = credentials('ACR')
        ACR_PASSWORD = credentials('ACR')
    }
    
    stages { 
        stage('Code checkout') {
            steps {  
                git 'https://github.com/rutwikdadgal/TS-demo.git'
            }
        }
        
        stage('Build docker image') {
            steps {  
                sh "docker build -t $ACR_SERVER/nginx:$BUILD_NUMBER ."
            }
        }
        stage('Login to ACR and push image') {
            environment {
                DOCKER_CLI_HOME = "${workspace}"
            }
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'ACR', usernameVariable: 'ACR_USERNAME', passwordVariable: 'ACR_PASSWORD')]) {
                        sh """
                            echo \${ACR_PASSWORD} | docker login -u \${ACR_USERNAME} --password-stdin \${ACR_SERVER}
                            docker push ${ACR_SERVER}/nginx:${BUILD_NUMBER}
                        """
                    }
                }
            }
        }
    }
}
