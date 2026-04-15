stage('Docker Build') {
    steps {
        sh 'docker build -t myapp:latest .'
    }
}

stage('Run Container') {
    steps {
        sh 'docker run -d --name myapp_container myapp:latest'
        sh 'docker ps'
    }
}

stage('Cleanup') {
    steps {
        sh 'docker stop myapp_container || true'
        sh 'docker rm myapp_container || true'
    }
}
