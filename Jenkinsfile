pipeline {
  agent any

  environment {
    REGISTRY = "ali-salahuddin"
    BACKEND_IMAGE = "${REGISTRY}/taskbloom-backend"
    FRONTEND_IMAGE = "${REGISTRY}/taskbloom-frontend"
    TAG = "${BUILD_NUMBER}"
  }

  stages {

    stage('Build Docker Images') {
      steps {
        script {
          docker.build("${BACKEND_IMAGE}:${TAG}", "./backend")
          docker.build("${FRONTEND_IMAGE}:${TAG}", "./frontend")
        }
      }
    }

    stage('Push Docker Images') {
      steps {
        script {
          docker.withRegistry('', 'dockerhub-creds') {
            docker.image("${BACKEND_IMAGE}:${TAG}").push()
            docker.image("${FRONTEND_IMAGE}:${TAG}").push()
          }
        }
      }
    }

    stage('Deploy to Kubernetes with Helm') {
      steps {
        sh """
        helm upgrade --install taskbloom ./taskbloom-chart \
          --set backend.image=${BACKEND_IMAGE} \
          --set backend.tag=${TAG} \
          --set frontend.image=${FRONTEND_IMAGE} \
          --set frontend.tag=${TAG}
        """
      }
    }
  }

  post {
    success {
      echo '✅ CI/CD pipeline completed successfully'
    }
    failure {
      echo '❌ CI/CD pipeline failed'
    }
  }
}