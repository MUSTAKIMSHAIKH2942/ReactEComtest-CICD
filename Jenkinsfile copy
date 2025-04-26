pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'your-dockerhub-username/react-cicd-app'
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/your-username/react-cicd-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t $DOCKER_IMAGE ."
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    withDockerRegistry([credentialsId: 'dockerhub-creds', url: '']) {
                        sh "docker push $DOCKER_IMAGE"
                    }
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                script {
                    sh "kubectl apply -f react-deployment.yaml"
                    sh "kubectl apply -f react-service.yaml"
                }
            }
        }
    }
}
