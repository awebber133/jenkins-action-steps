pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "alexis441/jenkins-demo"
        DOCKER_CREDS = credentials('dockerhub-creds')
    }

    stages {
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE .'
            }
        }

        stage('Push Docker Image') {
            steps {
                sh '''
                  echo "$DOCKER_CREDS_PSW" | docker login -u "$DOCKER_CREDS_USR" --password-stdin
                  docker push $DOCKER_IMAGE
                '''
            }
        }
    }
}
