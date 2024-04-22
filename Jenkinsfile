pipeline {
    agent any
   
    stages {
        stage('SCM Checkout') {
            steps {
                retry(3) {
                    git branch: 'main', url: 'https://github.com/dilshanka/4144_Ranaweera-K.D'
                }
            }
        }
        stage('Build Docker Image') {
            steps {  
                bat 'docker build -t lubuntukavi/my-react-app:%BUILD_NUMBER% .'
            }
        }
        stage('Login to Docker Hub') {
            steps {
                withCredentials([string(credentialsId: 'test-dockerhubpassword', variable: 'test-dockerhubpass')]) {
                   
                   
                    bat "docker login -u lubuntukavi -p ${test-dockerhubpass}"
    
}
               
                       
                   
                }
            }
        }
        stage('Push Image') {
            steps {
                bat 'docker push lubuntukavi/my-react-app:%BUILD_NUMBER%'


            }
        }
    }
    post {
        always {
            bat 'docker logout'
        }
    }
}
