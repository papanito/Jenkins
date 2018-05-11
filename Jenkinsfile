pipeline {
    agent any
    parameters {        
        booleanParam(defaultValue: false, description: 'This is a Release build', name: 'isRelease')
    }

    stages {
        stage('Build') {
            steps {
                 script {
                     if ("${params.isRelease}" == "true")) {
                          echo("This is a release")
                     }
                 }
            }
        }
    }
}
