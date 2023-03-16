pipeline {
    agent any
    stages {
        stage('Clone') {
            steps {
                script {
                    git branch: 'main', url: 'https://github.com/hiagomoa/golang-api'
                }
            }
        }
        stage('Build') {
            steps {
                sh '''
                    echo "Building..."
                    docker build -t hiagomoa/golang-api:${BUILD_NUMBER} .
                '''
            }
        }
        stage('Test') {
            steps {
                sh '''
                    echo "Testing..."
                    docker run -it hiagomoa/golang-api:${BUILD_NUMBER}
                    curl localhost:8080
                '''
            }
        }
    }
}
