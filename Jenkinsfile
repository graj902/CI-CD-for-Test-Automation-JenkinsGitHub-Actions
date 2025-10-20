pipeline {
    agent any

    stages {
        stage ("Backend Unit Test") {
            steps {
                script {
                    // Navigate to the Go code directory
                    dir ('bugtracker-backend') { 
                        
                        // Use the Docker sidecar pattern. 
                        // We use the 'inside' command to ensure we are running within a clean Go environment.
                        // We do NOT specify a user, letting the sidecar handle its own process, 
                        // but we rely on the previously fixed socket mount (-v /var/run/docker.sock) 
                        // and the successful installation of the Docker Pipeline plugin.
                        
                        docker.image('golang:1.20').inside {
                            echo "Running Go tests inside golang:1.20 container..."
                            
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
