pipeline { agent any

stages {
    stage ("Backend Unit Test") {
        steps {
            // IMPORTANT: This 'dir' must match the folder where your Go code is.
            // Assuming it is 'bugtracker-frontend' as per your earlier quote.
            dir ('bugtracker-frontend') { 
                sh 'go test -v ./...'
            }
        }
    }
}