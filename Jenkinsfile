pipeline {
    agent any
        stages {
            stage('Param'){
                steps {
                    script {
                        def param = sh(script: "python3 test.py", returnStdout: true).toString()
                        echo "param: ${param}"
                        choice = input(id: 'choice', message: 'Choose one', parameters: [choice(name: 'CHOICE', choices: ['a', 'b'], description: 'ddddddddd')])
                    }
                }
            }
        }   
}