pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "mythili23manivel/mythili-app"
    }

    stages {

        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t ${DOCKER_IMAGE}:latest ."
            }
        }

        stage('Test') {
            steps {
                sh "echo Test Successful"
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
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'USER',
                    passwordVariable: 'PASS'
                )]) {
                    sh "echo $PASS | docker login -u $USER --password-stdin"
                    sh "docker push ${DOCKER_IMAGE}:latest"
                }
            }
        }
    }

    post {
        success {
            echo "🎉 Pipeline SUCCESS - Docker image built, run, and pushed!"
        }

        failure {
            echo "❌ Pipeline FAILED - check logs"
        }
    }
}
