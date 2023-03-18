pipeline {
    agent any
    parameters {
        sh 'echo "Hello World"'
        // choice(name: 'ENVIRONMENT', choices: ['https://github.com/hiagomoa/golang-api', 'QA', 'PROD'], description: 'Select the environment to deploy')
        // gitParameter(name: 'GIT_BRANCH', useRepository:"${params.ENVIRONMENT}", type: 'PT_BRANCH', defaultValue: 'main', description: 'Select the branch to deploy')
    }
    stages {
        stage('Clone') {
            steps {
                script {
                    echo "Cloning... ${params.GIT_BRANCH}"
                    echo "Cloning... ${params.ENVIRONMENT}"
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
