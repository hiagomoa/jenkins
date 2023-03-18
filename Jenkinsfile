pipeline {
    agent any
        stages {
            stage('Param'){
                steps {
                    script {
                        def param = sh(script: "python test.py", returnStdout: true).toString()
                        echo "param: ${param}"
                    }
                }
            }
        }   
}