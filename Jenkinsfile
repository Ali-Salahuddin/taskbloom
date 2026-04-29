pipeline {
  agent any

  environment {
    REGISTRY = "ali-salahuddin"
    BACKEND_IMAGE = "${REGISTRY}/taskbloom-backend"
    FRONTEND_IMAGE = "${REGISTRY}/taskbloom-frontend"
    TAG = "${BUILD_NUMBER}"
  }

  stages {
<<<<<<< HEAD

    stage('Build Docker Images') {
      steps {
        script {
          docker.build("${BACKEND_IMAGE}:${TAG}", "./backend")
          docker.build("${FRONTEND_IMAGE}:${TAG}", "./frontend")
        }
      }
    }

    stage('Push Docker Images') {
=======
    stage('Docker Sanity Check') {
>>>>>>> 1f889973eb1219df18dfa25729d281da065f63f6
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
<<<<<<< HEAD

  post {
    success {
      echo '✅ CI/CD pipeline completed successfully'
    }
    failure {
      echo '❌ CI/CD pipeline failed'
    }
  }
}
=======
}
>>>>>>> 1f889973eb1219df18dfa25729d281da065f63f6
