pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t my-k8s-app:4 .'
            }
        }

        stage('Start Minikube') {
            steps {
                sh '''
                minikube status || minikube start --driver=docker
                '''
            }
        }

        stage('Load Image into Minikube') {
            steps {
                sh 'minikube image load my-k8s-app:4'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f k8s.yaml'
            }
        }
    }
}
