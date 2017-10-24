pipeline {
    agent any
    
    stages {
        stage('Commit') {
            steps {
                git 'https://github.com/OvidioMiranda/tz-rest-api'
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
        }
        stage('Package') {
            steps {
                sh './gradlew clean shadowJar'
            }
        }
    }
}
