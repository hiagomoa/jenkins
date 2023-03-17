pipeline {
    agent any
    parameters {
    gitParameter(
      branch: '',
      branchFilter: ".*",
      defaultValue: "",
      description: '',
      listSize: '10',
      name: 'Version',
      quickFilterEnabled: false,
      selectedValue: 'NONE',
      sortMode: 'ASCENDING_SMART',
      tagFilter: "*",
      type: 'PT_BRANCH_TAG',
      useRepository: 'https://github.com/hiagomoa/golang-api')
   }
    stages {
        stage('Clone') {
            steps {
                script {
                    echo "${params.Version}"
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
