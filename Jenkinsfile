    
pipeline {
    agent any
    stages {
        stage('Clear workspace') {
            steps {
                cleanWs(patterns: [[pattern: 'dist/*', type: 'INCLUDE']])
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
