pipeline {
    agent any
    environment {
        DOCKER_USER = 'alexis441'
        DOCKER_PASS = 'your-docker-password'
    }
    stages {
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t alexis441/jenkins-demo .'
            }
        }
        stage('Push Docker Image') {
            steps {
                sh '''
                echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin
                docker push alexis441/jenkins-demo
                '''
            }
        }
    }
}

