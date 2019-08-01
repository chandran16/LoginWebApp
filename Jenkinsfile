pipeline{
    agent any
    stages{
        stage('Git - Checkout') {
            steps{
                git branch: 'dockersetup', credentialsId: '', url: 'git@https://github.com/Saravananmoorthy/LoginWebApp.git'
            }
       }
       stage('Build') {
            steps{
                sh "mvn clean install"
            }
        }
        stage('Build and Push Docker Image') {
            steps{
                sh "sudo docker build --build-arg JAR_FILE_PATH=$WORKSPACE/target/LoginWebApp.jar Dockerfile -t cloud.docker.com/repository/registry-1.docker.io/saravananmoorthy/dockerdemo:${BUILD_NUMBER} ."
                sh "sudo docker push https://cloud.docker.com/repository/registry-1.docker.io/saravananmoorthy/dockerdemo:${BUILD_NUMBER}"
                sh "sudo rm -r $WORKSPACE/dockerfiles/service.jar"
            }
        }
}
}
