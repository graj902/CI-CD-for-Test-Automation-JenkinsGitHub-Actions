pipeline {
    agent any 
    stages {
        stage ("unit-test backend") {
            steps {
                dir('bugtracker-backend') { // Fixed: added quotes
                    sh "go test -v ./..."
                }
            }
        }
        stage ("unit-test frontend") {
            steps {
                dir('bugtracker-frontend') { // Fixed: added quotes
                    sh "npm install"
                    sh "npm test"
                }
            }
            // Fixed: Moved post block inside the correct stage
            post {
                always {
                    junit 'bugtracker-frontend/test-results.xml'
                }
            }
        }       
    }
}
