pipeline {
    agent any

    parameters {
        string(name: 'DOCKER_USER', defaultValue: 'alexis441', description: 'Docker Hub username')
        password(name: 'DOCKER_PASS', defaultValue: '', description: 'Docker Hub password')
    }

    environment {
        DOCKER_IMAGE = "alexis441/jenkins-demo"
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
                  echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                  docker push $DOCKER_IMAGE
                '''
            }
        }
    }
}
