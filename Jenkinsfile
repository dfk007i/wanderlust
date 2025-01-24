pipeline {
    agent any

    environment {
        // Define the SonarQube environment variable
        SONARQUBE_ENV = 'Sonar' // Replace 'SonarQube' with your actual SonarQube configuration name in Jenkins
    }

    stages {
        stage('Clone Repository') {
            steps {
                // Clone the GitHub repository
                git url: 'https://github.com/dfk007i/wanderlust.git', branch: 'devops'
            }
        }

        stage('Build') {
            steps {
                // Build the project (replace with your actual build command)
                sh 'echo "Building the project..."'
                // Example: sh './build.sh'
            }
        }

        stage('Test') {
            steps {
                // Run tests (replace with your actual test command)
                sh 'echo "Running tests..."'
                // Example: sh './test.sh'
            }
        }

        stage('SonarQube Analysis') {
            environment {
                // Inject SonarQube environment variables
                scannerHome = tool name: 'SonarQube Scanner', type: 'hudson.plugins.sonar.SonarRunnerInstallation'
            }
            steps {
                withSonarQubeEnv(SONARQUBE_ENV) {
                    // Run the SonarQube scanner
                    sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=wanderlust -Dsonar.projectName=wanderlust"
                }
            }
        }
    }

    post {
        always {
            // Clean up workspace
            cleanWs()
        }
        success {
            // Notify success
            echo 'Pipeline succeeded!'
        }
        failure {
            // Notify failure
            echo 'Pipeline failed!'
        }
    }
}
