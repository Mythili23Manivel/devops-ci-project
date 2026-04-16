pipeline {
    agent any

    environment {
        IMAGE_NAME = "mythili23manivel/autotrigger"
    }

    triggers {
        githubPush()
    }

    stages {

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Run Container Test') {
            steps {
                sh 'docker rm -f test-container || true'
                sh 'docker run --name test-container $IMAGE_NAME'
            }
        }

        stage('Push Docker Image') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'docker-hub-cred',
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
            sh 'docker rm -f test-container || true'
        }
    }
}
