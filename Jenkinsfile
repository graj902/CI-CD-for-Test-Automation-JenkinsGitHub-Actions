pipeline {
    agent any

    stages {
        stage ("Backend Unit Test") {
            steps {
                script { // 'script' block is required to use 'docker' pipeline syntax
                    // Navigate into the subdirectory where the Go code lives
                    dir ('bugtracker-frontend') { 
                        // Use the official Go Docker image to run the command inside a clean environment
                        docker.image('golang:1.22').inside {
                            echo "Running Go tests inside golang:1.22 container..."
                            
                            // 1. Download dependencies (important for a clean runner)
                            sh 'go mod tidy' 
                            
                            // 2. Run the tests
                            sh 'go test -v ./...'
                        }
                    }
                }
            }
        }
    }
}
