pipeline {
    agent any 
    stages {
        stage ("unit-test backend") {
            steps {
                dir('bugtracker-backend') {
                    // FINAL FIX: We are now using the full, absolute path where 'go install'
                    // placed the binary for the 'ubuntu' user, bypassing all Jenkins PATH confusion.
                    sh "go test -v ./... 2>&1 | /home/ubuntu/go/bin/go-junit-report > test-results.xml"
                }
            }
            post {
                always {
                    // This now points to the file generated in the dir('bugtracker-backend')
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
