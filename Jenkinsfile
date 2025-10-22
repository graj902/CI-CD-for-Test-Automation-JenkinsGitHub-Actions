pipeline {
    agent any 
    stages {
        stage ("unit-test backend") {
            steps {
                dir('bugtracker-backend') {
                    // This path is correct; we just needed directory permissions.
                    sh "go test -v ./... 2>&1 | /home/ubuntu/go/bin/go-junit-report > test-results.xml"
                }
            }
            post {
                always {
                    junit 'bugtracker-backend/test-results.xml' 
                }
            }
        }
        stage ("unit-test frontend") {
            steps {
                dir('bugtracker-frontend') {
                    sh "npm install"
                    sh "npm test"
                }
            }
            post {
                always {
                    junit 'bugtracker-frontend/test-results.xml'
                }
            }
        }       
    }
}
