pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "alexis441/jenkins-demo" // Change to your Docker Hub username/repo if needed
    }

    stages {
        stage('Checkout Code') {
            steps {
                // Checkout the repo
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE .'
            }
        }

        stage('Push Docker Image') {
            steps {
                // Use Jenkins stored credentials (Username + Password) with ID 'dockerhub-creds'
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh '''
                        echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                        docker push $DOCKER_IMAGE
                    '''
                }
            }
        }
    }

    post {
        success {
            echo "Docker image $DOCKER_IMAGE successfully built and pushed!"
        }
        failure {
            echo "Something went wrong. Check console output for details."
        }
    }
}

