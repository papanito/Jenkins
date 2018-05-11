@Library('PipelineHelperPapanito') _

pipeline {
    agent any
    parameters {        
        booleanParam(defaultValue: false, description: 'This is a Release build', name: 'isRelease')
        booleanParam(defaultValue: false, description: 'Run powershell script', name: 'runPs')
    }

    stages {
        stage('Build') {
            steps {
                 script {
                     if ("${params.isRelease}" == "true") {
                          echo("This is a release")
                     }
                 }
                 replaceStringInFile("./resources/test.xml", "one", "two")
                
                 script {
                     if ("${params.runPs}" == "true") {
                          runPowershell(". './test.ps1' -param1 test", false)
                     }
                 }
            }
        }
    }
}
