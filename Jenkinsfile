pipeline {
    agent any

    environment {
        IMAGE_NAME = 'bytesbuddy/ecommerce'
    }

    stages {
        stage('Clone Code') {
            steps {
                git 'https://github.com/MUSTAKIMSHAIKH2942/reactecomtestCICD.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t $IMAGE_NAME .'
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    withDockerRegistry([credentialsId: 'dockerhub-creds', url: '']) {
                        sh 'docker push $IMAGE_NAME'
                    }
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                script {
                    sh 'kubectl apply -f react-deployment.yaml'
                    sh 'kubectl apply -f react-service.yaml'
                }
            }
        }
    }
}
