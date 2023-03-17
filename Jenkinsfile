pipeline {
    agent any
    parameters {
        choice(name: 'ENVIRONMENT', choices: ['DEV', 'QA', 'PROD'], description: 'Select the environment to deploy')
        gitParameter(name: 'GIT_BRANCH', useRepository:'https://github.com/hiagomoa/golang-api', type: 'PT_BRANCH', defaultValue: 'main', description: 'Select the branch to deploy')
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
