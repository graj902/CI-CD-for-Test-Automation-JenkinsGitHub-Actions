//pipeline for go backend bugtracker applications
pipeline {
    agent any
    stages { 
        stage ("unit tests-backend") {
            steps {
                dir('backend') {
                    script {
                        if (fileExists('go.mod')) {
                            sh 'go mod tidy'
                            sh 'go test -v ./...'
                        } else {
                            error "go.mod file not found in the backend directory"
                        }
                    }
                }
            }
        }
    }
}
