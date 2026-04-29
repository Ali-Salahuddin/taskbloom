pipeline {
  agent any

  stages {
    stage('Docker Sanity Check') {
      steps {
        sh 'docker --version'
        sh 'docker ps'
      }
    }
  }
}
