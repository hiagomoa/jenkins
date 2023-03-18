pipeline {
    agent any
        stages {
            stage('Param'){
                steps {
                    script {
                        def param = ['one', 'two', 'three']
                        echo "param: ${param}"
                        choice = input(id: 'choice', message: 'Choose one', parameters: [choice(name: 'CHOICE', choices: param, description: 'ddddddddd')])
                    }
                }
            }
        }   
}