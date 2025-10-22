pipeline {
    agent any 
    stages {
        stage ("unit-test backend") {
            steps {
                dir('bugtracker-backend') {
                    // FIXED: Corrected the shell redirection syntax to generate XML report
                    sh "go test -v ./... 2>&1 | go-junit-report > test-results.xml"
                }
            }
            post {
                always {
                    // This now looks for the report file generated in the steps block
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
