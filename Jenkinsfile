pipeline {
    agent any 
    stages {
        stage ("unit-test backend") {
            steps {
                dir('bugtracker-backend') {
                    // This path is correct; we just needed directory permissions.
                    sh '''
                     go test -v ./... 2>&1 | /home/ubuntu/go/bin/go-junit-report > test-results.xml 
                     # generate coverage report
                     go test -coverprofile=coverage.out -covermode=atomic ./...
                     go tool cover -html=coverage.out -o coverage.html
                     mkdir -p reports
                     mv coverage.html reports/
                     '''
                }
            }
            post {
                always {
                    junit 'bugtracker-backend/test-results.xml' 
                    publishHTML (target: [
                        allowMissing: false,
                        alwaysLinkToLastBuild: true,
                        keepAll: true,
                        reportDir: 'bugtracker-backend/reports',
                        reportFiles: 'coverage.html',
                        reportName: 'Code Coverage Report'
                    ])
                }
            }
        }
        stage ("unit-test frontend") {
            steps {
                dir('bugtracker-frontend') {
                    sh ''' 
                    npm install
                    sh npm test
                    mkdir -p reports
                    mv coverage reports/
                    '''
                }
            }
            post {
                always {
                    junit 'bugtracker-frontend/test-results.xml'
                    publishHTML (target: [
                        allowMissing: false,
                        alwaysLinkToLastBuild: true,
                        keepAll: true,
                        reportDir: 'bugtracker-frontend/reports/coverage',
                        reportFiles: 'index.html',
                        reportName: 'Frontend Code Coverage Report'
                    ])
                }
            }
        }       
    }
}
