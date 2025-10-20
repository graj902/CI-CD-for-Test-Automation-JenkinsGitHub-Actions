pipeline {
    agent any

    stages {
        stage ("Backend Unit Test") {
            steps {
                script {
                    // Navigate to the Go code directory
                    dir ('bugtracker-backend') { 
                        
                        // Use the Docker sidecar pattern. 
                        // CRITICAL FIX: The 'user: "0"' argument forces the Docker commands 
                        // to be run as the root user (UID 0) inside the Jenkins agent, 
                        // bypassing the persistent permission denied error on the socket.
                        docker.image('golang:1.20').inside(
                            // Adding the 'user' parameter here
                            options: '-u 0'
                        ) {
                            echo "Running Go tests inside golang:1.20 container as root..."
                            
                            // 1. Download dependencies
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
