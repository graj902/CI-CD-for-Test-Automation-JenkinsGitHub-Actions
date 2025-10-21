//pipeline for go backend bugtracker applications
pipeline {
    agent any
    stages { 
        stage ("unit tests-backend") {
            steps {
                dir('backend') {
                    sh 'go test -v ./...'
                }
        }
    }
}