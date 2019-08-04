pipeline{
       environment {
    registry = "saravananmoorthy/dockerdemo"
    registryCredential = 'dockerhub'
    dockerImage = ''
  }
    agent any
    stages{
        stage('Git - Checkout') {
            steps{
                git branch: 'dockeritem', credentialsId: '', url: 'https://github.com/Saravananmoorthy/LoginWebApp.git'
            }
       }
       stage('Build') {
            steps{
                sh "mvn clean install"
            }
        }
         stage('Building image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
    stage('Deploy Image') {
      steps{
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
          }
        }
      }
    }
}
}
