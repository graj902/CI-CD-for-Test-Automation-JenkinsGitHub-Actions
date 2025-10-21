pipeline {
    agent any
    stages { 
        stage ("unit tests-backend") {
            steps {
                // The workspace is the checkout root where go.mod should be.
                
                // 1. Resolve dependencies (Must run where go.mod is located)
                sh 'go mod tidy'
                
                // 2. Run tests, explicitly targeting the package path
                sh 'go test -v ./backend/...'
            }
        }
    }
}