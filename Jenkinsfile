    
pipeline {
    agent any
    stages {
        stage('Clear workspace') {
            steps {
                cleanWs(patterns: [[pattern: 'dist/*', type: 'INCLUDE']])
            }
        }
        tage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, 
                          extensions: [[$class: 'CleanBeforeCheckout']], submoduleCfg: [], 
                          userRemoteConfigs: [[url: 'https://github.com/tdworowy/cicd-pipeline-train-schedule-git']]])
            }
        }    
        stage('Build') {
            steps {
                echo 'Running build automation'
                sh './gradlew build --no-daemon'
                archiveArtifacts artifacts: 'dist/*.zip'
            }
        }
    }
}
