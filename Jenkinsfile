pipeline {
    agent any

    environment {
        IMAGE_NAME = "mythili23manivel/autotrigger:latest"
        CONTAINER_NAME = "test-container"
    }

    triggers {
        githubPush()
    }

    stages {

        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Run Container Test') {
            steps {
                sh '''
                    docker rm -f $CONTAINER_NAME || true
                    docker run -d --name $CONTAINER_NAME -p 8081:8080 $IMAGE_NAME
                    sleep 5
                    docker ps
                '''
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
                        echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin
                        docker push $IMAGE_NAME
                    '''
                }
            }
        }
    }

    post {
        always {
            sh 'docker rm -f $CONTAINER_NAME || true'
        }
        success {
            echo '🚀 Pipeline Success! Image built, tested, and pushed to Docker Hub.'
        }
        failure {
            echo '❌ Pipeline Failed! Check logs.'
        }
    }
}
