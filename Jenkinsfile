pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'docker build -t myapp:${BUILD_NUMBER} .'
      }
    }
    stage('Load into Minikube') {
      steps {
        sh 'minikube image load myapp:${BUILD_NUMBER}'
      }
    }
    stage('Deploy') {
      steps {
        sh 'sed "s|myapp:latest|myapp:${BUILD_NUMBER}|" deployment.yaml | kubectl apply -f -'
        sh 'kubectl rollout status deployment/myapp --timeout=120s'
      }
    }
  }
}
