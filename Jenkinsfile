pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        checkout scm
        echo '✅ Git checkout successful'
      }
    }

    stage('Docker Sanity Check') {
      steps {
        sh 'docker --version'
        sh 'docker ps'
      }
    }
  }
}