pipeline {
    agent any
    stages { 
        stage ("unit tests-backend") {
            steps {
                // CRITICAL FIX: The module root (where go.mod lives) is bugtracker-backend.
                dir('bugtracker-backend') {
                    
                    // 1. Resolve dependencies (now runs correctly inside bugtracker-backend)
                    sh 'go mod tidy'
                    
                    // 2. Run tests on all packages in the current directory (bugtracker-backend) 
                    // and its subdirectories (like ./cmd or ./internal).
                    sh 'go test -v ./...'
                }
            }
        }
    post {
        always {
            junit 'bugtracker-frontend/**/TEST-*.xml'
        }
     }

    }
 } 
