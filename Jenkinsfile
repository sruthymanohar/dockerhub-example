pipeline {
  agent { label 'linux' }
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('armia123')
  }
  stages {
    stage('Build') {
      steps {
        sh 'docker build -t armia123/myalpine:latest .'
      }
    }
    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
    stage('Push') {
      steps {
        sh 'docker push armia123/myalpine:latest'
      }
    }
  }
  post {
    always {
      sh 'docker logout'
    }
  }
}
