pipeline {
    agent any
    parameters {
        choice(
            name: 'repo',
            choices: getGithubRepos('hiagomoa', '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'),
            description: 'Selecione o repositório para construir'
        )
        choice(
            name: 'branch',
            choices: getGithubBranches(params.repo,'hiagomoa', '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'),
            description: 'Selecione a branch para construir'
        )
    }
    stages {
        stage('Build') {
            steps {
                // execute aqui os passos da construção do seu projeto
            }
        }
    }
}

def getGithubRepos(String username, String token) {
    def url = "https://api.github.com/users/${username}/repos"
    def connection = new URL(url).openConnection() as HttpURLConnection
    connection.setRequestProperty('Authorization', "token ${token}")
    connection.setRequestMethod('GET')

    def response = connection.inputStream.text

    def jsonSlurper = new JsonSlurper()
    def repos = jsonSlurper.parseText(response)

    return repos.collect { repo -> repo.full_name }
}

def getGithubBranches(String repo, String username, String token) {
    def url = "https://api.github.com/repos/${repo}/branches"
    def connection = new URL(url).openConnection() as HttpURLConnection
    connection.setRequestProperty('Authorization', "token ${token}")
    connection.setRequestMethod('GET')

    def response = connection.inputStream.text

    def jsonSlurper = new JsonSlurper()
    def branches = jsonSlurper.parseText(response)

    return branches.collect { branch -> branch.name }
}
