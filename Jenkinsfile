pipeline {
    agent any
    
    parameters {
        string(name: 'username', defaultValue: 'hiagomoa', description: 'Nome de usuário do Github')
        string(name: 'token', defaultValue: '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', description: 'Token de autenticação do Github')
    }
    
    stages {
        stage('Listar repositórios') {
            steps {
                script {
                    def githubApiUrl = "https://api.github.com/users/${params.username}/repos"
                    def response = sh(script: "curl -s -H 'Authorization: token ${params.token}' $githubApiUrl", returnStdout: true)
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
                    
                    def branchesUrl = "https://api.github.com/repos/${params.username}/${chosenRepo}/branches"
                    response = sh(script: "curl -s -H 'Authorization: token ${params.token}' $branchesUrl", returnStdout: true)
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
