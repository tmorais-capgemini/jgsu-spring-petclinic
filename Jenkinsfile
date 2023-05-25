#!/usr/bin/env groovy
// shebang tells most editors to treat as groovy (syntax highlights, formatting, etc)

pipeline {
    agent any
    triggers { pollSCM('* * * * *') }
    
    stages {
        //Stages are for visualization and troubleshooting purposes
        
        //implicit checkout stage - because of SCM
        
        stage('Build') {
            steps {
                sh './mvnw clean package'
            }
         }
     }
    //post block is pulled out of stages
    post {
        // If Maven was able to run the tests, even if some of the test
        // failed, record the test results and archive the jar file.
        always {
            junit '**/target/surefire-reports/TEST-*.xml'
            archiveArtifacts 'target/*.jar'
        }
    }
}

