pipeline {
    agent any

    environment {
       GITHUB_TOKEN = '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'
    }
    parameters {
        choice(
            name: 'REPO',
            choices: getGithubRepos(),
            description: 'Escolha o repositório do Github'
        )
        choice(
            name: 'BRANCH',
            choices: getGithubBranches("${params.REPO}"),
            description: 'Escolha a branch'
        )
    }

    stages {
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: "${params.BRANCH}"]], userRemoteConfigs: [[url: "https://github.com/${params.REPO}.git"]]])
            }
        }
        // Outras etapas do pipeline aqui...
    }
}

def getGithubRepos() {
    def url = "https://api.github.com/users/${username}/repos"
    def connection = new URL(url).openConnection() as HttpURLConnection
    connection.setRequestProperty('Authorization', "token ${env.GITHUB_TOKEN}")
    connection.setRequestMethod('GET')

    def response = connection.inputStream.text

    def jsonSlurper = new JsonSlurper()
    def repos = jsonSlurper.parseText(response)

    return repos.collect { repo -> repo.full_name }
}

def getGithubBranches(repo) {
    def response = httpRequest(url: "https://api.github.com/repos/${repo}/branches?access_token=${env.GITHUB_TOKEN}")
    def branches = []
    if (response.status == 200) {
        def json = readJSON(text: response.content)
        json.each {
            branches.add("${it['name']}")
        }
    }
    return branches
}
