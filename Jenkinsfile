//Jenkinsfile pipeline for the Backend bugtracker project

pipeline {
    agent any

    stages {
        stage ("unit test-build") {
            agent {
                docker {
                    image 'golang:1.20'
                    args '-v /go/pkg/mod:/go/pkg/mod'
                }
            }
            steps {
                dir ('bugtracker-backend') {
                    sh 'go test -v ./...'
                }
            }
        }
    }
}