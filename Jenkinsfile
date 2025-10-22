pipeline {
    agent any 
    stages {
        stage ("unit-test backend") {
            steps {
                dir('bugtracker-backend') {
                    // FIX: Use triple quotes to update the PATH environment variable
                    // This allows the shell to find the 'go-junit-report' executable.
                    sh '''
                        export PATH=$PATH:$HOME/go/bin
                        go test -v ./... 2>&1 | go-junit-report > test-results.xml
                    '''
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
