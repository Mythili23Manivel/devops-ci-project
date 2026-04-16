pipeline {
    agent any

    stages {

        stage('Test Message') {
            steps {
                echo "GitHub + Jenkins working"
            }
        }

        stage('Docker Test') {
            steps {
                sh 'docker --version'
            }
        }
    }
}
