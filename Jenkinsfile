pipeline {
    agent any

    environment {
        REGISTRY = "alisalahuddin"
        BACKEND_IMAGE = "alisalahuddin/taskbloom-backend"
        FRONTEND_IMAGE = "alisalahuddin/taskbloom-frontend"
        TAG = "${BUILD_NUMBER}"
    }

    stages {

        stage('Build Docker Images') {
            steps {
                bat """
                docker build -t ${BACKEND_IMAGE}:${TAG} backend
                docker build -t ${FRONTEND_IMAGE}:${TAG} frontend
                """
            }
        }

        stage('Push Docker Images') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    bat """
                    echo %DOCKER_PASS% | docker login -u %DOCKER_USER% --password-stdin
                    docker push ${BACKEND_IMAGE}:${TAG}
                    docker push ${FRONTEND_IMAGE}:${TAG}
                    """
                }
            }
        }

        stage('Deploy to Kubernetes with Helm') {
    steps {
        bat """
        kubectl config current-context
        helm lint taskbloom-chart
        helm upgrade --install taskbloom taskbloom-chart ^
          --namespace taskbloom ^
          --create-namespace ^
          --atomic ^
          --timeout 5m ^
          --set backend.image.repository=${BACKEND_IMAGE} ^
          --set backend.image.tag=${TAG} ^
          --set frontend.image.repository=${FRONTEND_IMAGE} ^
          --set frontend.image.tag=${TAG}
        """
    }
}

    }

    post {
        always {
            cleanWs()
        }
        success {
            echo "✅ CI/CD pipeline completed successfully"
        }
        failure {
            echo "❌ CI/CD pipeline failed"
        }
    }
}