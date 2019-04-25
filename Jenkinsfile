    
pipeline {
    agent any
    stages {
        stage('Clear workspace') {
            steps {
                cleanWs(patterns: [[pattern: 'cicd-pipeline-train-schedule-git/dist/*', type: 'INCLUDE']])
            }
        }
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, 
                          extensions: [[$class: 'CleanBeforeCheckout']], submoduleCfg: [], 
                          userRemoteConfigs: [[url: 'https://github.com/tdworowy/cicd-pipeline-train-schedule-git.git']]])
            }
        }    
        stage('Build') {
            steps {
                dir("cicd-pipeline-train-schedule-git") {
                    echo 'Running build automation'
                    sh './gradlew build --no-daemon'
                    archiveArtifacts artifacts: 'dist/*.zip'
                }
            }
        }
    }
}
