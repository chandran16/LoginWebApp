pipeline{
    agent any
    stages{
        stage('Git - Checkout') {
            steps{
                git branch: 'dockersetup', credentialsId: '', url: 'https://github.com/Saravananmoorthy/LoginWebApp.git'
            }
       }
       stage('Build') {
            steps{
                sh "mvn clean install"
            }
        }
        stage('Build and Push Docker Image') {
            steps{
                whoami
                sh "docker build  $WORKSPACE/. -t saravananmoorthy/dockerdemo:${BUILD_NUMBER} ."
                sh "docker push saravananmoorthy/dockerdemo:${BUILD_NUMBER}"
            }
        }
}
}
