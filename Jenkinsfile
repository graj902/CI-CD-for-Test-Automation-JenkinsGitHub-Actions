pipeline {
    agent any 
    stages {
        stage ("unit-test backend") {
            steps {
                dir(bugtracker-backend) {
                    sh "go test -v ./..."
                }
            }
        }
stage ("unit-test frontend") {
    steps {
        dir(bugtracker-frontend) {
            sh "npm install"
            sh "npm test"
        }
    }
}       
        post {
            always {
                junit 'bugtracker-frontend/test-results.xml'
            }
        }
    }
}
