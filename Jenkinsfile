pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "mythili23manivel/mythili-app"
    }

    stages {

        stage('Build Docker Image') {
            steps {
                sh "docker build -t ${DOCKER_IMAGE}:latest ."
            }
        }

        stage('Test') {
            steps {
                sh 'echo Test Successful'
            }
        }

        stage('Run Container') {
            steps {
                sh "docker rm -f myapp || true"
                sh "docker run -d --name myapp ${DOCKER_IMAGE}:latest"
                sh "docker ps"
            }
        }

        stage('Push Image') {
            steps {
                sh "echo YOUR_PASSWORD | docker login -u mythili23manivel --password-stdin"
                sh "docker push ${DOCKER_IMAGE}:latest"
            }
        }
    }
}
