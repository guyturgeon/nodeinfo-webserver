pipeline {
  environment {
    registry = "gwaines/nodeinfo-webserver"
    registryCredential = 'St8rlingX*'
    dockerImage = ''
  }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        git 'https://github.com/gwaines/nodeinfo-webserver'
      }
    }
    stage('Python Test') {
      steps {
        sh 'cat app.py'
      }
    }
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
    stage('Local Docker Image Test') {
      steps {
        sh 'docker images'
      }
    }
/*
    stage('Deploy Image') {
      steps{
         script {
            docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
          }
        }
      }
    }
*/
    stage('Remove Unused docker image') {
      steps{
        sh "docker rmi $registry:$BUILD_NUMBER"
      }
    }
  }
}

