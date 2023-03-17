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
                    docker run -d -p 3000:3000 hiagomoa/golang-api:${BUILD_NUMBER}
                    curl localhost:3000
                    docker rm -f $(docker ps -aq)
                '''
            }
        }
    }
}
