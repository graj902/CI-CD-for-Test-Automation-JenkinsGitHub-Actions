pipeline {
    agent any
    stages { 
        stage ("unit tests-backend") {
            steps {
                // CRITICAL FIX: The module root (where go.mod lives) is bugtracker-backend.
                dir('bugtracker-backend') {
                    
                    echo "Running go mod tidy..."
                    sh 'go mod tidy'
                    
                    echo "Running go test..."
                    sh 'go test -v ./...'
                }
            }
        }
    post 
    {
        always {
            junit 'bugtracker-frontend/**/TEST-*.xml'
        }
        success {
            echo "Unit tests-backend stage finished successfully."
        }
        failure {
            echo "Unit tests-backend stage finished with errors."
        }
    }
 }

