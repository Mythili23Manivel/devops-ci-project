pipeline {
    agent any
    stages {
        stage('Test') {
            steps {
                echo 'Pipeline is working 🚀'
            }
        }
        stage('Docker Test') {
    steps {
        sh 'docker --version'
        sh 'docker ps'
    }
}
    }
    
}
