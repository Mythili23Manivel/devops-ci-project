pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "mythili23manivel/mythili-app"
    }

    stages {

        stage('Clone') {
    steps {
        git branch: 'main', url: 'https://github.com/Mythili23Manivel/devops-ci-project.git'
    }
}
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${DOCKER_IMAGE}")
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    docker.image("${DOCKER_IMAGE}").inside {
                        sh 'echo Test Successful'
                    }
                }
            }
        }

        stage('Push Image') {
            steps {
                script {
                    docker.withRegistry('', 'dockerhub-cred') {
                        docker.image("${DOCKER_IMAGE}").push("latest")
                    }
                }
            }
        }
    }
}
