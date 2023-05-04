pipeline {
  agent any
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('mvsh1406-dockerhub')
  }
  stages {
    stage('Build') {
      steps {
        sh 'docker build -t mvsh1406/jenkins'
      }
    }
    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
    stage('Push') {
      steps {
        sh 'docker push mvsh1406/jenkins:latest'
      }
    }
  }
  post {
    always {
      sh 'docker logout'
    }
  }
}
