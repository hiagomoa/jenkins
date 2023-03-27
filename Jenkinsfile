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
    def response = httpRequest(url: "https://api.github.com/user/repos?access_token=${env.GITHUB_TOKEN}")
    def repos = []
    if (response.status == 200) {
        def json = readJSON(text: response.content)
        json.each {
            repos.add("${it['full_name']}")
        }
    }
    return repos
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
