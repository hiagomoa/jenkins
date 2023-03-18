pipeline {
    agent any
        stages {
            stage('Param'){
                steps {
                    script {
                        def param = sh(script: "python3 test.py", returnStdout: true).toString()
                        echo "param: ${param}"
                    }
                }
            }
        }   
}