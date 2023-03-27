pipeline {
    agent any
    
    stages {
        stage('Escolher repositório') {
            steps {
                script {
                    def githubApiUrl = 'https://api.github.com/user/repos'
                    def githubToken = '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'
                    def repos = sh(script: "curl -H 'Authorization: token ${githubToken}' -s '${githubApiUrl}' | jq -r '.[].full_name'", returnStdout: true).trim().split('\n')
                    def chosenRepo = input message: 'Escolha um repositório', parameters: [choice(choices: repos, description: 'Escolha um repositório do Github')]
                    env.GITHUB_REPO = chosenRepo
                }
            }
        }
        
        stage('Escolher branch') {
            steps {
                script {
                    def githubApiUrl = "https://api.github.com/repos/${env.GITHUB_REPO}/branches"
                    def githubToken = 'TOKEN_AQUI'
                    def branches = sh(script: "curl -H 'Authorization: token ${githubToken}' -s '${githubApiUrl}' | jq -r '.[].name'", returnStdout: true).trim().split('\n')
                    def chosenBranch = input message: 'Escolha uma branch', parameters: [choice(choices: branches, description: 'Escolha uma branch do repositório selecionado')]
                    env.GITHUB_BRANCH = chosenBranch
                }
            }
        }
        
        stage('Build e deploy') {
            steps {
                echo "Repositório selecionado: ${env.GITHUB_REPO}"
                echo "Branch selecionada: ${env.GITHUB_BRANCH}"
                // Adicione aqui os comandos para construir e implantar o seu projeto
            }
        }
    }
}
