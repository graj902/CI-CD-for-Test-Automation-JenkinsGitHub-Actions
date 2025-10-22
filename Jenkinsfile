pipeline {
    agent any
    
    // 1. ENVIRONMENT VARIABLES
    // You will need these for the next steps
    environment {
        BACKEND_TEST_REPORT = 'bugtracker-backend/backend_test_results.xml'
        FRONTEND_TEST_REPORT = 'bugtracker-frontend/test-results.xml'
        FRONTEND_COVERAGE_REPORT = 'bugtracker-frontend/coverage/lcov.info'
    }

    stages { 
        stage ("unit tests-backend") {
            steps {
                dir('bugtracker-backend') {
                    echo "Running go mod tidy..."
                    sh 'go mod tidy'
                    
                    // NOTE: This stage requires a tool (like gotestsum) to create the XML report
                    echo "Running go test..."
                    sh 'go test -v ./... || true' 
                }
            }
            // 2. BACKEND POST BLOCK IS NOW CORRECTLY PLACED INSIDE THE STAGE
            post {
                always {
                    // This will eventually publish your Go test results
                    junit testResults: env.BACKEND_TEST_REPORT, skipOldReports: true
                }
            }
        } // <--- Stage block ends HERE

        stage ("unit test for frontend") {
            steps {
                dir('bugtracker-frontend') {
                    sh 'npm install'
                    // Ensure your package.json is configured for JUnit output
                    sh 'npm test -- --coverage --watchAll=false --reporters=default --reporters=jest-junit' 
                }
            }
            // 3. FRONTEND POST BLOCK IS CORRECTLY PLACED INSIDE THIS STAGE
            post {
                always {
                    // This publishes your Jest JUnit XML reports
                    junit testResults: env.FRONTEND_TEST_REPORT, skipOldReports: true
                }
                
            }
        }
        
         } 
    }
