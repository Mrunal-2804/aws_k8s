pipeline {
    agent {
        label 'node'
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Mrunal-2804/aws_k8s.git'
            }
        }

        stage('Build Image') {
            steps {
                sh 'docker build -t mrunal2804/aws-k8s:latest .'
            }
        }

        stage('Login to Docker Hub') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'dockerhub-creds',
                        usernameVariable: 'DOCKER_USERNAME',
                        passwordVariable: 'DOCKER_PASSWORD'
                    )
                ]) {
                    sh '''
                        echo "$DOCKER_PASSWORD" | docker login -u "$DOCKER_USERNAME" --password-stdin
                    '''
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                sh 'docker push mrunal2804/aws-k8s:latest'
            }
        }

        stage('Deploy to K8s') {
            steps {
                sh 'kubectl apply -f deployment.yaml'
                sh 'kubectl apply -f service.yaml'
            }
        }

        stage('Verify') {
            steps {
                sh '''
                    kubectl get pods
                    kubectl get svc
                '''
            }
        }
    }
}