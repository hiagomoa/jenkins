pipeline {
    agent any
        stages {
            stage('Param'){
                steps {
                    script {
                        def param = sh(script: "python3 test.py", returnStdout: true).toString().split(',')
                        def p2 = ['one', 'two', 'three']
                        echo "param: ${param}/${p2}"
                        choice = input(id: 'choice', message: 'Choose one', parameters: [choice(name: 'CHOICE', choices: param, description: 'ddddddddd')])
                    }
                }
            }
        }   
}