pipeline {
    agent any
    
    stages {
        stage('Commit') {
            steps {
                sh './gradlew clean assemble'
            }
        }
        stage('Test') {
            steps {
                sh './gradlew clean check'
                publishHTML target: [
                    allowMissing: false,
                    alwaysLinkToLastBuild: false,
                    keepAll: true,
                    reportDir: 'build/reports/tests/test/',
                    reportFiles: 'index.html',
                    reportName: 'Unit Test Report'
                ]
                }
            }
        stage('Package') {
            steps {
                sh './gradlew clean shadowJar'
            }
        }
    }    
    post {
        always {
            junit 'build/test-results/test/*'
        }
    }
}
