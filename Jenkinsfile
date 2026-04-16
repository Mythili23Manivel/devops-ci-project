pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                git 'https://github.com/Mythili23Manivel/devops-ci-project.git'
            }
        }

        stage('Test Message') {
            steps {
                echo "🚀 Jenkins + GitHub integration is working!"
            }
        }
    }
}
