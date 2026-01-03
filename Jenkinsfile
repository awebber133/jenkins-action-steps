
pipeline {
    agent any

    environment {
        IMAGE_NAME = 'alexis441/jenkins-demo'
    }

    stages {

        stage('Checkout SCM') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/awebber133/jenkins-action-steps.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t "$IMAGE_NAME" .'
            }
        }

        stage('Push Docker Image') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    sh '''
                        echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                        docker push "$IMAGE_NAME"
                        docker logout
                    '''
                }
            }
        }
    }

    post {
        success {
            echo 'Docker image pushed successfully!'
        }
        failure {
            echo 'Something went wrong. Check console output for details.'
        }
    }
}










