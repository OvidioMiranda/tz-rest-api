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
                sh './gradlew check'
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
                sh './gradlew shadowJar'
                archiveArtifacts 'build/libs/*.jar'
                archiveArtifacts 'example.yml'
            }
        }
    }

    post {
        always {
            junit 'build/test-results/test/*'
        }
    }
}
