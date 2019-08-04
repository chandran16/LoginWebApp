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
          sh "sudo docker build  $WORKSPACE/. -t saravananmoorthy/dockerdemo:${BUILD_NUMBER}"
        }
      }
    }
    stage('Deploy Image') {
      steps{
        script {
          withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'dockerhub', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD']]) {
          sh "sudo docker login --password=${PASSWORD} --username=${USERNAME} docker.io"
          sh "sudo docker push saravananmoorthy/dockerdemo:${BUILD_NUMBER}"
           
          }
        }
      }
    }
}
}
