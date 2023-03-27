pipeline {
    agent any

    environment {
        GITHUB_API_URL = 'https://api.github.com/user/repos'
        AUTHORIZATION_HEADER = "Authorization: Bearer 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"
    }

    stages {
        stage('Listar repositórios') {
            steps {
                script {
                    def response = sh(script: "curl -s -H '${AUTHORIZATION_HEADER}' ${GITHUB_API_URL}", returnStdout: true)
                    def repos = readJSON text: response
                    
                    def repoOptions = []
                    for (def repo in repos) {
                        repoOptions << repo.name
                    }
                    
                    def chosenRepo = input(
                        message: 'Qual repositório você quer?',
                        parameters: [
                            [$class: 'ChoiceParameterDefinition', name: 'repoName', choices: repoOptions.join('\n')]
                        ]
                    )
                    
                    def branchesUrl = "https://api.github.com/repos/${env.GITHUB_USERNAME}/${chosenRepo}/branches"
                    response = sh(script: "curl -s -H '${AUTHORIZATION_HEADER}' ${branchesUrl}", returnStdout: true)
                    def branches = readJSON text: response
                    
                    def branchOptions = []
                    for (def branch in branches) {
                        branchOptions << branch.name
                    }
                    
                    def chosenBranch = input(
                        message: 'Qual branch você quer?',
                        parameters: [
                            [$class: 'ChoiceParameterDefinition', name: 'branchName', choices: branchOptions.join('\n')]
                        ]
                    )
                    
                    // O restante do pipeline continua aqui...
                }
            }
        }
    }
}
