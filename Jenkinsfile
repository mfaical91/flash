pipeline {
  agent any
  environment {
    IMAGE_NAME = "flask-app"
    DOCKER_REGISTRY = "localhost:5000"
  }
  stages {
    stage('Checkout') {
      steps {
        git 'https://github.com/utilisateur/flask-k8s.git'
      }
    }
    stage('Build Docker') {
      steps {
        sh 'docker build -t $DOCKER_REGISTRY/$IMAGE_NAME:latest .'
      }
    }
    stage('Push Docker Image') {
      steps {
        sh 'docker push $DOCKER_REGISTRY/$IMAGE_NAME:latest'
      }
    }
    stage('Deploy to Minikube') {
      steps {
        sh 'kubectl apply -f deployment.yaml'
      }
    }
  }
  post {
    success {
      echo 'Pipeline terminé avec succès.'
    }
    failure {
      echo 'Une erreur est survenue.'
    }
  }
}
